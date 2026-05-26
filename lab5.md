## Title
Reflected Cross-Site Scripting (XSS)

## Summary
I identified a reflected Cross-Site Scripting (XSS) vulnerability in the following endpoint.

## Vulnerable Endpoint
`https://kzlabs.com/5.php`

## Steps to Reproduce

1. Open the following URL in a browser:

`https://kzlabs.com/5.php?fname=%22+autofocus+onfocus%3Dalert%281%29+x%3D%22&lname=%22+autofocus+onfocus%3Dalert%281%29+x%3D%22`

2. Observe that the injected payload is reflected into the page and automatically triggers JavaScript execution.

3. A JavaScript alert popup appears, confirming successful reflected XSS.

## Payload Used
`" autofocus onfocus=alert(1) x="`

## Proof of Concept

## Screenshot 1 — Payload reflected inside the application response
<img width="1920" height="1008" alt="image" src="https://github.com/user-attachments/assets/0c385ff2-1107-418f-bccb-daa4dffda9f9" />

## Impact
- Session hijacking
- Cookie theft
- Phishing attacks
- Client-side browser manipulation

## Recommendations for Fix
1. Sanitise and validate all user-controlled input before rendering it in the response.
2. Escape special characters such as:
   `<`, `>`, `"`, `'`, `&`
3. Avoid directly reflecting unsanitised input into HTML attribute contexts.
4. Implement Content Security Policy (CSP) to reduce XSS impact.
5. Apply proper output encoding for all dynamic user-supplied content rendered in the browser.
