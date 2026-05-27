## Title

Reflected Cross-Site Scripting (XSS) in `s` Parameter

## Vulnerability Type

Reflected XSS

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability was identified in the `s` parameter of the following endpoint:

`https://zeals.ai/jp/case/blog/`

The application reflects user-supplied input directly into the response without proper sanitisation or output encoding. This allows attackers to inject malicious JavaScript that executes in the victim’s browser when a crafted URL is opened. Reflected XSS vulnerabilities can allow attackers to steal cookies, hijack sessions, or perform phishing attacks. :contentReference[oaicite:0]{index=0}

## Vulnerable Endpoint

`https://zeals.ai/jp/case/blog/?s=`

## Steps to Reproduce

1. Open the following URL in a browser:

```text
https://zeals.ai/jp/case/blog/?s=rj%27%22%3E%3Cbody+onload%3Dalert%281%29%3E+%3Cbody+onload%3Dalert%28%22hacker%22%29%3E&search_industry=&search_product=
```

2. Observe that a JavaScript popup appears automatically.

3. This confirms that user-controlled input is reflected and executed in the browser.

## Payload Used

```html
rj"><body onload=alert(1)> <body onload=alert("hacker")>
```

## Proof of Concept

### Screenshot 1 — Successful JavaScript execution confirming Reflected XSS

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/83480174-cdbe-46a0-8cd5-a6f9d8d95890" />


## Impact

- Execution of malicious JavaScript in user browsers
- Session hijacking
- Cookie theft
- Phishing attacks
- Unauthorized actions performed as the victim user

## Recommendations for Fix

1. Validate and sanitise all user input before rendering it in the response.
2. Escape special characters such as: `<`, `>`, `"`, `'`, `&`
3. Avoid reflecting raw user input directly into HTML content.
4. Apply proper output encoding before displaying dynamic content.
