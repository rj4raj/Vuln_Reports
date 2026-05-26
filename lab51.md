## Title

Reflected Cross-Site Scripting (XSS)

## Vulnerability Type

Reflected XSS

## Summary

A Reflected Cross-Site Scripting (XSS) issue was identified in the following endpoint:

`https://kzlabs.com/51.php`

The application reflects user input directly into the page without proper sanitisation, allowing JavaScript execution in the browser.

## Vulnerable Endpoint

`https://kzlabs.com/51.php`

## Steps to Reproduce

1. Open the following URL:

```text
https://kzlabs.com/51.php?input=%22%3E%3Cimg%20src=x%20onerror%3Dalert(1)%3E
```

2. Observe that the payload executes automatically.

## Payload Used

```html
"><img src=x onerror=alert(1)>
```

## Proof of Concept

### Screenshot 1 — Payload reflected in the application

<img width="1911" height="819" alt="image" src="https://github.com/user-attachments/assets/18e58bd8-9121-469e-8079-8758425037c8" />


## Impact

- Requires user interaction (manual input or paste)
- Cannot be exploited remotely without social engineering
- Limited real-world impact compared to reflected or stored XSS

## Recommendations for Fix

1. Treat all user input as plain text.
2. Do not allow HTML tags in input fields.
3. Escape input before displaying it on the page
