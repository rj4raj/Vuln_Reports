## Title
Reflected Cross-Site Scripting (XSS)

## Summary
I identified a reflected Cross-Site Scripting (XSS) vulnerability in the following endpoint:

## Vulnerable Endpoint
`https://kzlabs.com/punishment/16.php`

## Steps to Reproduce
 
1. Open:
https://kzlabs.com/punishment/16.php?item=%3Ciframe%20src=javascripT:alert(1)%3E

2. Observe execution.

## Payload Used
`<iframe src=javascript:alert(1)>`

## Proof of Concept

## Screenshot — Vulnerable application reflecting injected payload

<img width="1920" height="847" alt="image" src="https://github.com/user-attachments/assets/058ced8f-af8e-4e1b-b933-f6ab61f71d5a" />


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
5. If using PHP, use secure functions such as:   ```php htmlspecialchars($input, ENT_QUOTES, 'UTF-8');```
