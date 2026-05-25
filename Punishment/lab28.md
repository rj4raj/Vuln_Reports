## Title
Reflected Cross-Site Scripting (XSS)

## Summary
I identified a reflected Cross-Site Scripting (XSS) vulnerability in the following endpoint:

## Vulnerable Endpoint
`https://kzlabs.com/punishment/28.php`

## Steps to Reproduce
 
1. Open:
https://kzlabs.com/punishment/28.php?cat=%3CIMg%20src=x%20onerror=\u0063onfirm(1)%3E

2. Observe execution of payload.

## Payload Used
`<img src=x onerror=\u0063onfirm(1)>`

## Proof of Concept

## Screenshot — Vulnerable application reflecting injected payload
<img width="1911" height="854" alt="image" src="https://github.com/user-attachments/assets/fd3f1e83-6a97-499e-98fa-2306023d1fdb" />


## Impact
- Cookie stealing  
- Session hijacking  
- Phishing attacks  
- JavaScript execution in the victim browser  

## Recommendations for Fix
1. Sanitise all user-controlled input before rendering it in the response.  
2. Escape special characters such as: `<`, `>`, `"`, `'`, `&`  
3. Avoid reflecting unsanitized input directly into HTML or JavaScript contexts.  
4. Block dangerous JavaScript functions such as: `alert()`, `confirm()`, `prompt()`  
5. If using PHP, use secure functions such as:  
```php
htmlspecialchars($input, ENT_QUOTES, 'UTF-8');
