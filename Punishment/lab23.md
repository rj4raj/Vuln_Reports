## Title
Reflected Cross-Site Scripting (XSS)

## Summary
I identified a reflected Cross-Site Scripting (XSS) vulnerability in the following endpoint:

## Vulnerable Endpoint
`https://kzlabs.com/punishment/23.php`

## Steps to Reproduce
 
1. Open:
https://kzlabs.com/punishment/23.php?email=%3CiMg%20src=x%20onerror=conf\u0069rm(%22RJ%22)%3E

2. Observe execution of injected payload.

## Payload Used
`<img src=x onerror=conf\u0069rm("RJ")>`

## Proof of Concept

## Screenshot — Vulnerable application reflecting injected payload
<img width="1920" height="830" alt="image" src="https://github.com/user-attachments/assets/7e308879-9b62-44f5-a4ec-83ee70336e06" />


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
