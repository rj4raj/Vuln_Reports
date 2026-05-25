## Title
Reflected Cross-Site Scripting (XSS)

## Summary
I identified a reflected Cross-Site Scripting (XSS) vulnerability in the following endpoint:

## Vulnerable Endpoint
`https://kzlabs.com/punishment/19.php`

## Steps to Reproduce
 
1. Open:
https://kzlabs.com/punishment/19.php?categoryid=%3CScript%3Eprompt(%22raj%22)%3C/Script%3E

2. Observe execution.

## Payload Used
`<script>prompt("raj")</script>`

## Proof of Concept

## Screenshot — Vulnerable application reflecting injected payload
<img width="1917" height="723" alt="image" src="https://github.com/user-attachments/assets/ac07b0e0-4088-4e05-b6b0-57e39fcc347c" />


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





