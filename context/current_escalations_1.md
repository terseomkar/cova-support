# Cova — Current Escalations
## Updated: March 11, 2024

## Active engineering incidents
<!-- Why: A ticket may already have a fix in progress. 
Claude should tell the customer that, not investigate from scratch. -->

INC-2024-112 (Active)
Issue: Automation rules not firing for some accounts
Customer message: "We're aware of an issue affecting automation 
rules and our engineering team is actively working on a fix. 
We'll update you as soon as it's resolved."
Do not promise a fix time.

INC-2024-108 (Monitoring)
Issue: Billing history showing only 3 months
Customer message: "Your billing data is safe — this is a 
display issue only. A fix is deploying tonight."

## Known bugs (no active incident)
<!-- Why: Claude should recognize these symptoms 
and not treat them as new unknown issues. -->
- Canned responses disappearing after workspace migration
- Report date ranges shifted by 7 days for accounts 
  updated March 9th — patch releasing Thursday

## Compliance queue
<!-- Why: Compliance tickets have legal implications. 
Claude must never handle them — always escalate same day. -->
- HIPAA BAA requests → Carlos Vega, same-day response required
- GDPR data deletion → compliance team, 
  72-hour regulatory deadline