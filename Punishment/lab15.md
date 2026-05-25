## Title
Reflected Cross-Site Scripting (XSS)

## Summary
I identified a reflected Cross-Site Scripting (XSS) vulnerability in the following endpoint:

## Vulnerable Endpoint
`https://kzlabs.com/punishment/15.php`

## Steps to Reproduce
 
1. Open:
https://kzlabs.com/punishment/15.php?project=%3Cdetails+open+ontoggle%3Dalert(1)%3E

2. Observe execution immediately.

## Payload Used
`<details open ontoggle=alert(1)>`

## Proof of Concept

## Screenshot — Vulnerable application reflecting injected payload

<img width="1919" height="855" alt="image" src="https://github.com/user-attachments/assets/779550b7-8b45-41f0-90b6-b3dcf3bf06f5" />


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
