## Title
Reflected Cross-Site Scripting (XSS) in `ll` Parameter

## Summary
I identified a reflected Cross-Site Scripting (XSS) vulnerability in the `ll` parameter of the following endpoint:

## Vulnerable Endpoint
`https://kzlabs.com/punishment/30.php?ll=Rajvardhan%27%22%3E%3Cimimgg%20src=x%20onerror=%22alalertert(1)%22%20onclick=%22confirconfirmm(1)%22%20onmouseover=%22propromptmpt(1)%22%3E`

## Steps to Reproduce
 
1. Open the following URL in a browser: `https://kzlabs.com/punishment/30.php`

2. Observe that a JavaScript confirmation pop-up is triggered immediately.

3. This confirms that arbitrary JavaScript supplied via the `search` parameter is executed in the browser.

## Payload Used
Rajvardhan<imimgg%20src=x%20onerror="alalertert(1)"%20onclick="confirconfirmm(1)"%20onmouseover="propromptmpt(1)">
## Proof of Concept


## Screenshot 1 — Vulnerable application reflecting the injected payload
<img width="1920" height="847" alt="image" src="https://github.com/user-attachments/assets/a2789641-d620-40dd-bfc1-042e371bae64" />



## Impact
- Cookie stealing
- Session hijacking
- Phishing attacks
- JavaScript execution in the victim browser

## Recommendations for Fix
1. Sanitise all user-controlled input before rendering it in the response.
2. Escape special characters such as:
   `<`, `>`, `"`, `'`, `&`
3. Avoid reflecting unsanitized input directly into HTML or JavaScript contexts.
4. Block dangerous JavaScript functions such as:
   - `alert()`
   - `confirm()`
   - `prompt()`
5. If using PHP, use secure functions such as:
php,htmlspecialchars($input, ENT_QUOTES, 'UTF-8');
