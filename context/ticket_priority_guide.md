# Cova — Ticket Priority Guide
## How to categorize and format triage output

## Priority Definitions
- **Critical**: System down, data loss, security/compliance 
  issue, or complete business process blocked for Enterprise customer
- **High**: Major feature broken, significant customer impact, 
  time-sensitive business consequence
- **Medium**: Feature degraded, workaround available, 
  moderate customer impact
- **Low**: How-to question, feature request, 
  cosmetic issue, general inquiry

## Output Format
Always respond in this format unless instructed otherwise:

**Priority**: [Critical / High / Medium / Low]
**Issue type**: [Bug / Account / Billing / How-to / Feature request / Compliance]
**Plan tier**: [from ticket]
**SLA target**: [based on tier and priority]
**What's happening**: [1 sentence, plain English]
**Customer impact**: [what this is costing them right now]
**Immediate action**: [specific next step, assigned to a role]
**Draft first response**: [2-3 sentences to send to the customer]

## Pattern recognition
<!-- Why: Multiple similar tickets in one batch may 
mean a platform-wide incident, not individual problems. -->
- Two or more Critical/High tickets with the same symptom 
  → flag as possible incident, escalate to engineering
- Same customer appearing twice → consolidate into one ticket

## Summary reports
- Every time I ask for a summary, write those files in the @reports folder as a .md file