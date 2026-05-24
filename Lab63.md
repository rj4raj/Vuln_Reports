## Title
Stored Blind Cross-Site Scripting (Blind XSS) via Company Name Field

## Vulnerability Type
Stored Blind XSS

## Summary
While testing the application, I found that the "Company Name" field does not properly sanitize or encode user-supplied input before storing and rendering it inside the admin dashboard.
By injecting a malicious payload into the Company Name field, arbitrary JavaScript gets stored in the application and executes when an administrator or another privileged user views the affected page.

The payload was successfully triggered on the following admin endpoint:

  https://kzlabs.com/63.php?view=dashboard

This confirms the presence of a Stored Blind XSS vulnerability affecting privileged users.


Since the payload is stored server-side and triggered later inside the admin dashboard, this vulnerability can be leveraged to compromise privileged accounts without requiring direct interaction from the attacker.

## Vulnerable Endpoint
https://kzlabs.com/63.php?view=dashboard

Vulnerable Parameter: Company Name field
## Steps to Reproduce

1. Navigate to the application registration/profile form containing the Company Name field.
2. In the Company Name field, enter the following payload: `<img src=x onerror=alert(document.cookie)>`
3. Submit the form/request.
4. Wait for an administrator or privileged user to access the admin dashboard.
5. Visit the following page as an administrator: `https://kzlabs.com/63.php?view=dashboard`
6. Observe that the JavaScript payload executes automatically and displays the session cookie.

## Payload Used
`<img src=x onerror=alert(document.cookie)>`

## Proof of Concept

## Screenshot 1 — Blind XSS payload stored successfully in the Company Name field

![Payload Submission](screenshots/lab63.png)

## Screenshot 2 — Payload execution triggered inside the admin dashboard

![Blind XSS Trigger](screenshots/lab63.1.png)

## Screenshot 3 — Administrator session cookie displayed through document.cookie

![Admin Cookie Access](screenshots/lab63.2.png)

## Impact

- Steal administrator session cookies
- Account takeover of privileged users
- Arbitrary JavaScript execution in admin context
- Phishing attacks targeting administrators


## Remediation
1. Sanitize all user-controlled input before rendering it in the response.
2. Escape special characters such as:
   `<`, `>`, `"`, `'`, `&`
3. Avoid reflecting unsanitized input directly into HTML or JavaScript contexts.
4. Block dangerous JavaScript functions such as:
   - `alert()`
   - `confirm()`
   - `prompt()`
5. If using PHP, use secure functions such as:
php,htmlspecialchars($input, ENT_QUOTES, 'UTF-8');
