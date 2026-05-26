## Title

Reflected Cross-Site Scripting (XSS)

## Vulnerability Type

Reflected XSS

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability was identified in the following endpoint:

`http://www.kzlabs.com/21.php`

The application reflects user-supplied input directly into the response without proper sanitisation or output encoding. This allows execution of injected JavaScript in the victim’s browser when a crafted request is processed.

## Vulnerable Endpoint

`http://www.kzlabs.com/21.php`

## Steps to Reproduce

1. Navigate to the following URL:

```text
http://www.kzlabs.com/21.php?input=%3Cscript%3Ealert(%22rajvardhan%22)%3C/script%3E
```

2. Observe that a JavaScript alert box is triggered automatically.

3. This confirms that the application executes injected JavaScript from user input.

## Payload Used

```html
<script>alert("rajvardhan")</script>
```

## Proof of Concept

### Screenshot 1 — Payload injected into the vulnerable application

<img width="1911" height="819" alt="image" src="https://github.com/user-attachments/assets/79e709b5-09ac-41ec-afe5-881ff059e2e8" />


## Impact

- Session hijacking
- Account takeover
- Cookie theft
- Phishing attacks
- Execution of malicious scripts in the browser

## Recommendations for Fix

1. Validate and sanitise all user input before rendering it on the page.
2. Escape special characters such as: `<`, `>`, `"`, `'`, `&`
3. Avoid directly reflecting user input into HTML content.
4. Apply proper output encoding before rendering dynamic content.
