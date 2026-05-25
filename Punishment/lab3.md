## Title
Reflected Cross-Site Scripting (XSS)

## Summary
XSS in:
`https://kzlabs.com/punishment/3.php`

## Steps to Reproduce
1. Open exploit URL
2. Observe execution

## Payload Used
`rajvardhan1"><ScRipt>alert(10)</ScRipt>`

## Proof of Concept

## Screenshot — Vulnerable application confirming XSS execution
<img width="1920" height="1013" alt="image" src="https://github.com/user-attachments/assets/67e9d4ae-5c45-4d94-9e08-8cf106531320" />


## Impact
- Cookie/session compromise
- Script execution

## Recommendations for Fix
- Output encoding
- Input sanitization
