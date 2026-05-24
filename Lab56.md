## Title
Reflected Cross-Site Scripting (XSS) in "p" Parameter

## Summary
I identified a reflected Cross-Site Scripting (XSS) vulnerability in the `p` parameter of the following endpoint:

## Vulnerable Endpoint
https://labs.krazeplanet.com/56.php?p=


## Steps to Reproduce
1. Open the following URL in a browser:
https://labs.krazeplanet.com/56.php?p='><svg/onload=alert("RAJVARDHAN")>

2. Observe that a JavaScript alert box is triggered immediately.

3. This confirms that arbitrary JavaScript supplied via the "p" parameter is executed in the browser.


## Payload Used
`'><svg/onload=alert("RAJVARDHAN")>`

# Proof of Concept
This confirms the presence of a Reflected Cross-Site Scripting (XSS) vulnerability.

## Screenshot 1 — Malicious payload injected into the vulnerable parameter

![Payload Injection](screenshots/lab56.1.png)

## Screenshot 2 — JavaScript alert triggered successfully in the browser

![XSS Trigger](screenshots/lab56.2.png)


## Impact
- Cookie stealing
- Session hijacking
- Phishing attacks
- JavaScript execution in victim browser


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

