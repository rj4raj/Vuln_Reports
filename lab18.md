## Title

Stored Cross-Site Scripting (Stored XSS)

## Vulnerability Type

Stored XSS

## Summary

A Stored Cross-Site Scripting (Stored XSS) vulnerability was identified in the following endpoint:

`http://www.kzlabs.com/18.php`

The application stores user-supplied input without proper sanitisation or output encoding. Malicious JavaScript payloads submitted by an attacker are permanently stored by the application and executed in the browsers of other users when the affected content is viewed.

## Vulnerable Endpoint

`http://www.kzlabs.com/18.php`

## Steps to Reproduce

1. Navigate to the following endpoint:

```text
http://www.kzlabs.com/18.php
```

2. Submit the following payload into the vulnerable input field:

```html
"><script>alert(document.cookie)</script>
```

3. Save or submit the payload.

4. Revisit the page or access the stored content.

5. Observe that the JavaScript payload executes automatically in the browser.

## Payload Used

```html
"><script>alert(document.cookie)</script>
```

## Proof of Concept

### Screenshot 1 — Malicious payload submitted into the application

<img width="1911" height="819" alt="image" src="https://github.com/user-attachments/assets/d3bfbead-8186-43ff-9927-e664908fed02" />


## Impact

An attacker can use this vulnerability to:

- Execute malicious JavaScript in other users’ browsers
- Steal user session cookies
- Hijack user accounts
- Redirect users to phishing or malicious websites
- Perform actions on behalf of logged-in users
- Modify or manipulate website content

## Recommendations for Fix

1. Validate and sanitise all user input before saving it to the database.
2. Escape special characters such as: `<`, `>`, `"`, `'`, `&`
3. Do not render raw user input directly into HTML pages.
4. Apply proper output encoding before displaying user-controlled content.
5. Restrict or filter dangerous HTML tags and JavaScript event handlers.
