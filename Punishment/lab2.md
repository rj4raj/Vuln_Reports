## Title
Reflected Cross-Site Scripting (XSS) in `fname` and `lname Parameters`

## Summary
Reflected XSS vulnerability in:
`https://kzlabs.com/punishment/2.php`

## Steps to Reproduce
1. Open:
`https://kzlabs.com/punishment/2.php?fname=rajvardhan1%22%3E%3CScRipt%3Ealert%28%22RAJVARDHAN%22%29%3C%2FScRipt%3E&lname=rajvardhan1%22%3E%3CScRipt%3Ealert%28%22RRAJVARDHAN%22%29%3C%2FScRipt%3E`

2. Observe execution.

## Payload Used
`rajvardhan1"><ScRipt>alert("RAJVARDHAN")</ScRipt>`

## Proof of Concept

## Screenshot — Vulnerable application confirming XSS execution
<img width="1920" height="946" alt="image" src="https://github.com/user-attachments/assets/9473f241-c349-4395-82df-1bd66b7c19c3" />


## Impact
- Session hijacking
- Cookie theft
- JavaScript execution

## Recommendations for Fix
- Encode output properly
- Validate input
- Use secure rendering functions
