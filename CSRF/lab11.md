# Two-Factor Authentication Can Be Disabled via Cross-Site Request Forgery
## Vulnerability Type
Cross-Site Request Forgery (CSRF)
## Summary
While testing the account security settings, I found that the functionality used to disable Two-Factor Authentication (2FA) is vulnerable to Cross-Site Request Forgery (CSRF).

The application processes the request without validating a CSRF token or requiring any additional confirmation from the user. As a result, an attacker can craft a malicious webpage that silently sends a request to disable 2FA using the victim's active session.
If a logged-in user visits the attacker's page, 2FA can be disabled without their knowledge or consent.

## Affected Endpoint
`https://kzlabs.com/1311.php?action=disable2fa`

## Steps to Reproduce
1. Log in to the application.
2. Navigate to the Security Settings page.
3. Disable Two-Factor Authentication while intercepting the request in Burp Suite.
4. Observe that the request contains no CSRF token.
5. Generate a CSRF PoC using Burp Suite or create a malicious HTML page.
6. Host the file on an attacker-controlled website.
7. Send the link to a logged-in victim.
8. When the victim opens the page, the request is automatically submitted.
9. Two-Factor Authentication is disabled on the victim's account.

## Proof of Concept
## Request
```html
<html>
<body>
<form action="https://kzlabs.com/1311.php?action=disable2fa" method="POST">
<input type="submit" value="Submit request" />
</form>

<script>
document.forms[0].submit();
</script>

</body>
</html>
```

## Observations
- No CSRF token is present in the request.
- The request is accepted solely based on the user's authenticated session.
- No password confirmation is required.
- No 2FA verification code is required before disabling 2FA.
- The action succeeds immediately after the forged request is submitted.

## Proof of concept
## Screenshot 1
Captured request showing the 2FA disable functionality.
<img width="1919" height="1079" alt="Screenshot 2026-06-07 173259" src="https://github.com/user-attachments/assets/dfeec6a3-4ab7-4e33-8826-32514226a02f" />


## Screenshot 2
Burp Suite generating a CSRF Proof of Concept.
<img width="1156" height="992" alt="Screenshot 2026-06-07 173309" src="https://github.com/user-attachments/assets/f35e8420-c778-41e5-81d5-6a986c80a6e7" />

### Screenshot 3
Generated malicious HTML page.
<img width="1919" height="578" alt="image" src="https://github.com/user-attachments/assets/767fd079-94d8-4d90-8257-ebfbb505956a" />


## Screenshot 4
Victim opens the malicious page while authenticated.

<img width="1917" height="444" alt="Screenshot 2026-06-07 173400" src="https://github.com/user-attachments/assets/3d0886ef-cae8-4920-be88-381b8ce2493e" />


## Screenshot 5
Two-Factor Authentication is successfully disabled without user interaction.

<img width="1919" height="940" alt="Screenshot 2026-06-07 173408" src="https://github.com/user-attachments/assets/bc947c2e-dcd7-41e7-bf1a-4821c5a27707" />


## Impact
An attacker can trick a logged-in user into visiting a malicious webpage and silently disable Two-Factor Authentication on their account.
As a result, the attacker removes an important layer of account security and significantly lowers the barrier for future account compromise. If the attacker later obtains valid credentials through phishing, credential reuse, password disclosure, or another vulnerability, the account can be accessed without the protection normally provided by 2FA.

## Remediation

- Add CSRF protection to all security-sensitive actions.-
- Validate CSRF tokens on the server before processing requests.
- Require password confirmation before disabling 2FA.
- Require a valid 2FA code before allowing 2FA to be disabled.
- Verify that requests originate from trusted application pages by checking the Origin or Referer headers.

