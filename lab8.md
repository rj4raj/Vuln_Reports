## Title

Reflected Cross-Site Scripting (XSS)

## Vulnerability Type

Reflected XSS

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability was identified in the following endpoint:

`https://kzlabs.com/8.php?fname=&lname=`

The application reflects user-supplied input directly into the response without proper sanitisation or output encoding. An attacker can craft a malicious URL containing JavaScript code which executes in the victim’s browser when visited.

## Vulnerable Endpoint

`https://kzlabs.com/8.php?fname=&lname=`

## Steps to Reproduce

1. Navigate to the following URL:

```text
https://kzlabs.com/8.php?fname=rajvardhan&lname=%22%3E%3Cimg%20src=x%20onerror=prompt(1)%3E
```

2. Observe that a JavaScript popup is triggered automatically.

3. This confirms that arbitrary JavaScript supplied through user-controlled input is executed in the browser.

## Payload Used

```html
"><img src=x onerror=prompt(1)>
```

## Proof of Concept

### Screenshot 1 — Payload inserted into the vulnerable application

<img width="1920" height="1008" alt="image" src="https://github.com/user-attachments/assets/946b0e73-98c3-443b-8bbd-59d21c3cfde9" />


## Impact

An attacker may exploit this vulnerability to perform the following actions:

- Session hijacking
- Cookie theft
- Phishing attacks
- Account takeover possibilities
- Execution of malicious scripts within the victim's browser

## Recommendations for Fix

1. Validate and sanitise all user-controlled input before rendering it in the response.
2. Escape special characters such as: - `<` `>`  `"`  `'`  `&`
3. Avoid reflecting unsanitised input directly into HTML or JavaScript contexts.
4. Apply proper output encoding before rendering dynamic content in the browser.
5. If using PHP, use secure encoding functions such as: ```php htmlspecialchars($input, ENT_QUOTES, 'UTF-8');```
