## Title
Stored Cross-Site Scripting (XSS) via `Report Name Field` in Network Reports

## Vulnerability Type
Stored XSS

## Summary
While testing the application, I found that the `Report Name` field inside the `New Network Report` functionality does not properly sanitize or encode user-supplied input before storing and rendering it back to users.

By injecting a malicious payload into the Report Name field, arbitrary JavaScript gets stored in the application and automatically executes whenever the affected page or stored data is viewed.

Since the payload is persistent, every authenticated user visiting the affected page can trigger the payload execution, including administrators and potentially privileged users.

Since the payload is stored server-side, the attack automatically affects users viewing the page without requiring malicious links.


## Vulnerable Endpoint
https://kzlabs.com/60.php

Vulnerable Parameter: Report Name field inside the `New Network Report` form

# Steps to Reproduce
1. Navigate to: `https://kzlabs.com/60.php`
2. Log in with a valid account.
3. Open the `New Network Report` functionality.
4. In the `Report Name` field, enter the following payload: `"><img src=x onerror=alert("RAJVARDHAN")>`
5. Fill in the remaining required fields and submit the request.
6. After the report is created, revisit the Network Reports page.
7. Observe that a JavaScript alert box appears automatically.
8. The payload remains stored and executes whenever the affected page is viewed.

## Payload Used
`"><img src=x onerror=alert(1)>`

## Proof of Concept
This confirms the presence of a Stored Cross-Site Scripting (XSS) vulnerability.

## Screenshot 1 — Malicious payload submitted through the New Network Report functionality

![Payload Submission](screenshots/lab60.png)

## Screenshot 2 — Stored payload executing automatically when the reports page loads

![Stored XSS Execution](screenshots/lab60.2.png)

## Impact

- Steal session cookies of authenticated users
- Session hijacking
- Arbitrary JavaScript execution
- Phishing attacks



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
