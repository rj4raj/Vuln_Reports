## Title

Reflected Cross-Site Scripting (XSS)

## Vulnerability Type

Reflected XSS

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability was identified in the following endpoint:

`https://kzlabs.com/10.php?fname=&lname=`

The application reflects user-supplied input directly into the response without proper sanitisation or output encoding. An attacker can craft a malicious URL containing JavaScript code which executes in the victim’s browser when visited.

## Vulnerable Endpoint

`https://kzlabs.com/10.php?fname=&lname=`

## Steps to Reproduce

1. Navigate to the following URL:

```text
https://kzlabs.com/10.php?fname=%22%3E%3Cobject+oneonerrorrror%3D%22alealertrt%281%29%22+data%3Dx%3E&lname=%22%3E%3Cobject+oneonerrorrror%3D%22alealertrt%281%29%22+data%3Dx%3E
```

2. Observe that the injected payload is reflected into the page.

3. This confirms that user-controlled input is reflected without proper sanitisation, potentially allowing script execution depending on browser parsing behavior and application context.

## Payload Used

```html
"><object oneonerrorrror="alealertrt(1)" data=x>
```

## Proof of Concept

### Screenshot 1 — Payload inserted into the vulnerable application

<img width="1920" height="1008" alt="image" src="https://github.com/user-attachments/assets/6135489a-951e-43ab-a7a1-2bc71ce5ff9a" />

## Impact

An attacker may exploit this vulnerability to perform the following actions:

- Injection of malicious HTML content
- Client-side manipulation of rendered content
- Potential execution of arbitrary JavaScript
- Phishing attacks
- Delivery of further browser-based payloads

## Recommendations for Fix

1. Validate and sanitise all user-controlled input before rendering it in the response.
2. Escape special characters such as: `<`, `>`, `"`, `'`, `&`
3. Avoid reflecting unsanitised input directly into HTML or JavaScript contexts.
4. Apply proper output encoding before rendering dynamic content in the browser.
5. If using PHP, use secure encoding functions such as:  ```php
htmlspecialchars($input, ENT_QUOTES, 'UTF-8');
```

