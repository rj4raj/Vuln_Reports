## Title
Reflected Cross-Site Scripting (XSS) via `cat` Parameter

## Vulnerability Type
Reflected XSS

## Summary
In `https://kzlabs.com/punishment/32.php`, the `cat` parameter is vulnerable to Reflected Cross-Site Scripting (XSS). The application reflects user input directly into the response without proper sanitization or encoding, allowing execution of malicious JavaScript in the victim’s browser when a crafted URL is visited.

## Vulnerable Endpoint
https://kzlabs.com/punishment/32.php?cat=

## Steps to Reproduce

1. Open the following URL in a browser: https://kzlabs.com/punishment/32.php?cat=Rajvardhan%3Cimimgg%20src=x%20onerror=%22alalertert(1)%22%20onclick=%22confirconfirmm(1)%22%20onmouseover=%22propromptmpt(1)%22%3E

2. Observe that a JavaScript alert box is triggered, confirming successful execution of injected payload.

## Payload Used 
`Rajvardhan<imimgg src=x onerror="alalertert(1)" onclick="confirconfirmm(1)" onmouseover="propromptmpt(1)">`


## Proof of Concept

Screenshot 1: Payload reflected in input parameter  
<img width="1920" height="830" alt="image" src="https://github.com/user-attachments/assets/bfd8ff49-61c0-4e33-9301-4effc6a2845c" />



## Impact

An attacker can exploit this vulnerability to:

It allows attackers to hijack user session
It potentially leads to full account takeover
It allows to perform unauthorized actions within the vulnerable application
It allows attacker to exfiltrate sensitive data

## Recommendations for Fix


 Validate and sanitise the redirectUrl parameter to ensure that it does not contain any malicious content. This can be done by:

1. Filter out HTML tags like: `<script>`, `<img>`, `<svg>` from the Report Name field before saving anything to the database
2. Filter out JavaScript methods like: `alert()`, `confirm()`, `prompt()` so even if a tag slips through the method won't execute
4. If you're using PHP then use `htmlspecialchars()` function before rendering any user input back to the page
5. Use Cloudflare as they have so many WAF rules that almost all XSS payloads will be blocked automatically before even reaching the server
