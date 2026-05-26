## Title

Reflected Cross-Site Scripting (XSS)

## Vulnerability Type

Reflected XSS

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability was identified in the following endpoint:

`http://www.kzlabs.com/22.php`

The application reflects user-supplied input directly into the response without proper sanitisation or output encoding. This allows injected HTML/JavaScript to execute in the victim’s browser.

## Vulnerable Endpoint

`http://www.kzlabs.com/22.php`

## Steps to Reproduce

1. Open the following URL in a browser:

```text
http://www.kzlabs.com/22.php?input=%3Cbody%20onload%3Dalert(%22hacker%22)%3E
```

2. Observe that a JavaScript alert box is triggered automatically.

3. This confirms that injected payload executes in the browser context.

## Payload Used

```html
<body onload=alert("hacker")>
```

## Proof of Concept

### Screenshot 1 — Payload injected into the vulnerable application

<img width="1911" height="819" alt="image" src="https://github.com/user-attachments/assets/5e9e55a6-af77-4066-902d-37266ae4c38e" />


## Impact

- Session hijacking
- Account takeover
- Cookie theft
- Phishing attacks
- Execution of malicious scripts in user browser

## Recommendations for Fix

1. Validate and sanitise all user input before rendering it on the page.
2. Escape special characters such as: `<`, `>`, `"`, `'`, `&`
3. Avoid directly reflecting user input into HTML content.
4. Apply proper output encoding before rendering dynamic content.
