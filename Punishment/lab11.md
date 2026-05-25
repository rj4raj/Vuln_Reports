
## Title
Reflected Cross-Site Scripting (XSS)

## Summary
I identified a reflected Cross-Site Scripting (XSS) vulnerability in the following endpoint:

## Vulnerable Endpoint
`https://kzlabs.com/punishment/11.php`

## Steps to Reproduce
 
1. Open the following URL in a browser:  
https://kzlabs.com/punishment/11.php?fname=%3CiMg+src%3Dx+onerror%3Dconfirm%28111%29%3E&lname=%3CiMg+src%3Dx+onerror%3Dconfirm%2811%29%3E

2. Observe that JavaScript execution is triggered immediately.

3. This confirms that arbitrary JavaScript is executed due to improper input handling.

## Payload Used
`<iMg src=x onerror=confirm(111)>`

## Proof of Concept

## Screenshot — Vulnerable application reflecting injected payload
<img width="1920" height="836" alt="image" src="https://github.com/user-attachments/assets/8139ecfe-676d-4157-9836-8682c6f19596" />


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
