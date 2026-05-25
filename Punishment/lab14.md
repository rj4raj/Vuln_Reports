## Title
Reflected Cross-Site Scripting (XSS)

## Summary
I identified a reflected Cross-Site Scripting (XSS) vulnerability in the following endpoint:

## Vulnerable Endpoint
`https://kzlabs.com/punishment/14.php`

## Steps to Reproduce
 
1. Open:
https://kzlabs.com/punishment/14.php?p=%3Ciframe%20src=javaScript:alert(1)%3E

2. Observe execution immediately.

## Payload Used
`<iframe src=javascript:alert(1)>`

## Proof of Concept

## Screenshot — Vulnerable application reflecting injected payload

<img width="1920" height="849" alt="image" src="https://github.com/user-attachments/assets/2650ffb0-1eb1-43f5-908b-74ddbc8f0155" />


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
