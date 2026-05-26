## Title

Reflected Cross-Site Scripting (XSS)

## Vulnerability Type

Reflected XSS

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability was identified in the following endpoint. The application reflects user-supplied input directly into the response without proper sanitisation or output encoding, allowing JavaScript execution in the victim’s browser.

## Vulnerable Endpoint

`https://kzlabs.com/19.php`

## Steps to Reproduce

1. Navigate to the following URL:

```text
https://kzlabs.com/19.php?search=%3CscRipt%3Ealer%5Cu0074%28%27XSS%27%29%3C%2FScrIpt%3E
```

2. Observe that a JavaScript popup is triggered automatically.

3. This confirms that arbitrary JavaScript supplied through user-controlled input is executed in the browser.

## Payload Used

```html
<scRipt>aler\u0074('XSS')</ScrIpt>
```

## Proof of Concept

### Screenshot 1 — Payload inserted into the vulnerable application
<img width="1911" height="819" alt="image" src="https://github.com/user-attachments/assets/e12bb690-7d61-420b-81d9-01d87072e087" />



## Impact

- Session hijacking
- Account takeover
- Cookie theft
- Phishing attacks
- Execution of malicious JavaScript in user browsers

## Recommendations for Fix

1. Validate and sanitise all user-controlled input before rendering it in the response.
2. Escape special characters such as: `<`, `>`, `"`, `'`, `&`
3. Avoid reflecting unsanitised input directly into HTML or JavaScript contexts.
4. Apply proper output encoding before rendering dynamic content in the browser.
