## Title

Reflected Cross-Site Scripting (XSS)

## Vulnerability Type

Self XSS

## Summary

A Self Cross-Site Scripting (Self XSS) behavior was identified in the following endpoint:

`https://kzlabs.com/52.php`

The application reflects or executes user-controlled input in the browser when the payload is manually entered. However, the issue requires the user to actively input or paste the payload themselves, so it is not directly exploitable by a remote attacker without user interaction.

## Vulnerable Endpoint

`https://kzlabs.com/52.php`

## Steps to Reproduce

1. Open the following URL in a browser:

```text
https://kzlabs.com/52.php
```

2. Enter the following payload manually:

```html
"><img src=x onerror=alert(1)>
```

3. Submit or trigger the input processing.

4. Observe that the payload executes in the browser.

## Payload Used

```html
"><img src=x onerror=alert(1)>
```

## Proof of Concept

### Screenshot 1 — Payload entered into the application

<img width="1911" height="819" alt="image" src="https://github.com/user-attachments/assets/e057baf4-feec-48a4-8a49-ad0a1d319f8a" />


## Impact

- Requires user interaction (manual input or paste)
- Cannot be exploited remotely without tricking the user
- May be used in social engineering attacks to mislead users
- Limited real-world impact compared to stored or reflected XSS

## Recommendations for Fix

1. Treat all user input as plain text and do not render it as HTML.
2. Sanitize input before displaying it on the page.
3. Avoid allowing HTML tags inside user input fields.
4. If HTML is not required, completely disable HTML rendering for input fields.
