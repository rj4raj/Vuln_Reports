## Title

Self Cross-Site Scripting (Self XSS)

## Vulnerability Type

Self XSS

## Summary

A Self Cross-Site Scripting (Self XSS) behavior was observed in the following endpoint:

`https://kzlabs.com/50.php`

The application allows user-controlled input to be reflected or executed when manually inserted into the page. However, the exploit requires the user to actively paste or inject the payload themselves, meaning it is not directly exploitable by a remote attacker without user interaction.

## Vulnerable Endpoint

`https://kzlabs.com/50.php`

## Steps to Reproduce

1. Navigate to the following URL:

```text
https://kzlabs.com/50.php
```

2. Enter the following payload manually into the input field:

```html
<script>alert("rajvardhan")</script>
```

3. Submit the input.

4. Observe that JavaScript executes in the browser.

## Payload Used

```html
<script>alert("rajvardhan")</script>
```

## Proof of Concept

### Screenshot 1 — Payload entered into the application

<img width="1911" height="819" alt="image" src="https://github.com/user-attachments/assets/ae7e88ad-56ad-4dfd-b4c2-a330a06cba32" />


## Impact

This issue has limited security impact because:

- It requires user interaction (copy-paste or manual injection)
- It cannot be triggered remotely by a normal attacker link
- It does not directly affect other users

However, it may still be abused in social engineering attacks where a victim is tricked into pasting malicious code.

## Recommendations for Fix

1. Avoid executing or evaluating any user input as code.
2. Display user input as plain text instead of rendering it as HTML.
3. Sanitize and encode all user input before displaying it on the page.
4. Educate users about not pasting unknown code into browser consoles or forms.
