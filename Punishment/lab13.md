## Title
Reflected Cross-Site Scripting (XSS)

## Summary
I identified a reflected Cross-Site Scripting (XSS) vulnerability in the following endpoint:

## Vulnerable Endpoint
`https://kzlabs.com/punishment/13.php`

## Steps to Reproduce
 
1. Open the following URL in a browser:  
https://kzlabs.com/punishment/13.php?fname=%3CiMg%20src=x%20onerror=%26%2397%3Blert%281%29%3E&lname=%3CiMg%20src=x%20onerror=%26%2397%3Blert%2811%29%3E

2. Observe execution immediately.

## Payload Used
`<img src=x onerror=&#97;lert(11)>`

## Proof of Concept

## Screenshot — Vulnerable application reflecting injected payload

<img width="1920" height="721" alt="image" src="https://github.com/user-attachments/assets/34b896e5-0ce5-4167-82cc-f8aeedbbd99d" />


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
