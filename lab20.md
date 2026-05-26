## Title

Reflected Cross-Site Scripting (XSS)

## Vulnerability Type

Reflected XSS

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability was identified in the following endpoint:

`https://kzlabs.com/20.php`

The application reflects user-supplied input directly into the response without proper sanitisation or output encoding. An attacker can inject malicious JavaScript that executes in the victim’s browser when the crafted URL is visited.

## Vulnerable Endpoint

`https://kzlabs.com/20.php`

## Steps to Reproduce

1. Open the following URL in a browser:

```text
https://kzlabs.com/20.php?cat="><script>alert(document.cookie)</script>
```

2. Observe that a JavaScript alert box is triggered automatically.

3. This confirms that user input is reflected and executed as JavaScript in the browser.

## Payload Used

```html
"><script>alert(document.cookie)</script>
```

## Proof of Concept

### Screenshot 1 — Payload injected into the vulnerable application

<img width="1911" height="819" alt="image" src="https://github.com/user-attachments/assets/75e772fb-5f81-49de-981e-2f167d286dcd" />


## Impact

An attacker can use this vulnerability to:

- Steal session cookies from users
- Hijack logged-in user accounts
- Redirect users to malicious or phishing pages
- Execute scripts in the victim’s browser
- Perform actions on behalf of the user without permission

## Recommendations for Fix

1. Validate and sanitise all user input before displaying it on the page.
2. Escape special characters such as: `<`, `>`, `"`, `'`, `&`
3. Avoid directly reflecting user input into HTML content.
4. Apply proper output encoding before rendering dynamic content.
