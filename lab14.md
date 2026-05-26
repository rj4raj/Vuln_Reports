## Title

Reflected Cross-Site Scripting (XSS)

## Vulnerability Type

Reflected XSS

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability was identified in the following endpoint:

`https://kzlabs.com/14.php?cat=`

The application reflects user-supplied input directly into the response without proper sanitisation or output encoding. An attacker can craft a malicious URL containing JavaScript code which executes in the victim’s browser when visited.

## Vulnerable Endpoint

`https://kzlabs.com/14.php?cat=`

## Steps to Reproduce

1. Navigate to the following URL:

```text
https://kzlabs.com/14.php?cat=%3CScRipT%3Ealer\u0074(1101)%3C/ScRipT%3E
```

2. Observe that a JavaScript popup is triggered automatically.

3. This confirms that arbitrary JavaScript supplied through user-controlled input is executed in the browser.

## Payload Used

```html
<ScRipT>aler\u0074(1101)</ScRipT>
```

## Proof of Concept

### Screenshot 1 — Payload inserted into the vulnerable application

<img width="1909" height="902" alt="image" src="https://github.com/user-attachments/assets/d9daf93e-ce23-4959-ba16-a6dbc696cd57" />

## Impact

An attacker may exploit this vulnerability to perform the following actions:

- Session hijacking
- Cookie theft
- Phishing attacks
- Account takeover possibilities
- Execution of malicious scripts within the victim browser
- Unauthorized actions performed on behalf of authenticated users

## Recommendations for Fix

1. Validate and sanitise all user-controlled input before rendering it in the response.
2. Escape special characters such as: `<`, `>`, `"`, `'`, `&`
3. Avoid reflecting unsanitised input directly into HTML or JavaScript contexts.
4. Apply proper output encoding before rendering dynamic content in the browser.
