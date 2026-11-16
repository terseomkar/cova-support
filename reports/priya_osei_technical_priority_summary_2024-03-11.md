# Technical Ticket Priority Summary — Priya Osei

**Source:** `data/tickets_batch1.md` (Batch 1, 2024-03-11)
**Scope:** Technical issues: bugs, integrations, API (per `context/agent_role.md`)
**Cross-referenced against:** `context/current_escalations_1.md`, `context/ticket_priority_guide.md`

---

## At a glance

| # | Ticket | Customer (tier) | Issue | Priority | SLA due (UTC) | Escalations status |
|---|--------|-----------------|-------|----------|---------------|--------------------|
| 1 | TICKET-001 | TechFlow Inc (Enterprise, 240) | Bulk CSV user import: success shown, only 12/180 created | **Critical** | **09:14** | New, no match |
| 2 | TICKET-008 | Granite Financial (Enterprise, 195) | SSO / SAML assertion error after Azure AD policy change | **Critical** | **12:20** | New, no match |
| 3 | TICKET-004 | Cascade Retail (Growth, 78) | All 14 automation rules stopped firing ~02:00 | High | 13:30 | **Active incident INC-2024-112** |
| 4 | TICKET-007 | BlueWave Marketing (Growth, 55) | ~40 canned responses disappeared | High | 14:44 | **Known bug** (canned responses lost after workspace migration) |
| 5 | TICKET-010 | Harbor Logistics (Growth, 67) | Report "last 7 days" returns data from 8–14 days ago | High | 18:30 | **Known bug** (date ranges shifted 7 days; patch Thursday) |
| 6 | TICKET-005 | NorthPoint Consulting (Professional, 32) | Hitting API rate limits below documented threshold | Medium | Same day (not covered by the 4h SLA) | New, no match |

**Two new Critical Enterprise issues need engineering today.** TICKET-001's 1-hour SLA had already passed when this batch came in. The other High tickets already match work in progress, so for those the job is confirming the match, not starting a new investigation.

---

## Critical: escalate to the engineering lead now

### 1. TICKET-001: Bulk user import failing silently
- **Customer:** TechFlow Inc, Enterprise (240 seats). Contact: Sarah Okonkwo, IT Manager
- **Submitted:** 08:14 UTC · **SLA:** 1 hour (Critical, Enterprise), due **09:14 UTC**
- **Why Critical:** Possible data loss (users the import reported as created don't exist) and a fully blocked business process for an Enterprise customer. Their company-wide rollout is **Thursday**.
- **Reported behavior:**
  - CSV upload of 180 users (done 2024-03-10)
  - The UI showed a success message
  - Only 12 users were actually created
  - No error log in the admin panel
- **Info to collect from the customer:** the CSV file (or a sanitized sample), the upload timestamp, the account/workspace ID, and the IDs of the 12 users that were created (to see where processing stopped).
- **Engineering focus:** Why the import reports success after a partial result, and why nothing is logged. Root cause isn't confirmed yet.
- **Also:** Flag to the account manager as an Enterprise churn risk because of the Thursday deadline.

### 2. TICKET-008: SSO broken, 195 users locked out
- **Customer:** Granite Financial, Enterprise (195 seats). Contact: Thomas Nguyen, IT Director
- **Submitted:** 11:20 UTC · **SLA:** 1 hour (Critical, Enterprise), due **12:20 UTC**
- **Why Critical:** System down for an Enterprise customer. All 195 employees can't log in.
- **Reported behavior:**
  - The customer changed its Azure AD password policy the night of 2024-03-10 (security audit)
  - Since then, SSO logins fail with a SAML assertion error
- **Info to collect from the customer:** the full SAML error text or a SAML trace, the exact policy change made in Azure AD, the time of the change, and whether *any* users can still log in.
- **Note:** The timing points to the customer-side policy change, but that isn't confirmed. Don't present it to the customer as the cause until the SAML response has been examined.
- **Also:** Flag to the account manager as an Enterprise churn risk. If engineering approves, consider a temporary non-SSO login path for admins.

---

## High: these match known work, so confirm and link

### 3. TICKET-004: Automation rules not firing → INC-2024-112 (Active)
- **Customer:** Cascade Retail, Growth (78 seats). Contact: Marcus Webb, Head of Operations
- **Submitted:** 09:30 UTC · **SLA:** 4 hours (High, Growth), due **13:30 UTC**
- **Reported behavior:** All 14 active routing rules stopped firing around 02:00. Every ticket lands in the general queue. Volume is 300+ tickets/day.
- **Action:** Attach to **INC-2024-112**. Add Cascade Retail to the list of affected accounts, along with the ~02:00 start time and the "all 14 rules" scope.
- **Customer message:** Use the approved incident message. Don't give a fix time.

### 4. TICKET-007: Canned responses disappeared → known bug
- **Customer:** BlueWave Marketing, Growth (55 seats). Contact: Alicia Torres, Team Lead
- **Submitted:** 10:44 UTC · **SLA:** 4 hours (High, Growth), due **14:44 UTC**
- **Reported behavior:** About 40 saved canned responses vanished the morning of 2024-03-11. The customer says they didn't delete them.
- **Known bug:** "Canned responses disappearing after workspace migration." **Need to confirm** BlueWave had a workspace migration before treating this as the same bug.
- **Watch:** If the responses can't be recovered, this is data loss and should go up to **Critical**.

### 5. TICKET-010: Report date ranges wrong → known bug
- **Customer:** Harbor Logistics, Growth (67 seats). Contact: Frank Deluca, Support Manager
- **Submitted:** 14:30 UTC · **SLA:** 4 hours (High, Growth), due **18:30 UTC**
- **Reported behavior:** The "last 7 days" filter returns data from 8–14 days ago. Started after the March 9 update. Affects all 4 report templates.
- **Known bug:** "Report date ranges shifted by 7 days for accounts updated March 9th." Patch releases Thursday. The symptoms match exactly.
- **Customer message:** Confirm the issue is known and a fix is in progress. Per support constraints, don't promise Thursday to the customer unless that date is confirmed.

---

## Medium: route to the technical support tier

### 6. TICKET-005: API rate limit question
- **Customer:** NorthPoint Consulting, Professional (32 seats). Contact: Jennifer Lau, Operations Lead
- **Submitted:** 09:55 UTC · **SLA:** The 4-hour SLA covers only Critical/High, but answer the same day.
- **Reported behavior:** They're hitting rate limits during an integration build even though they believe they're within the documented limits.
- **Questions to answer:**
  1. What's the actual enforced rate limit for the Professional plan?
  2. Is there an account-specific limit that differs from the docs?
  3. Are higher limits available, and how?
- **Status:** A customer response has been drafted. It asks for the endpoints, request rate, error text and timestamps.

---

## Patterns and notes
- **No new incident cluster.** No two new Critical/High tickets share a symptom. TICKET-004 is already covered by INC-2024-112.
- **Enterprise exposure:** Both Critical tickets (001, 008) are Enterprise and need account manager flags.
- **Out of scope for Priya:** These belong to other owners:
  - TICKET-002 (billing history, INC-2024-108) and TICKET-006 (HIPAA BAA, same-day) → Carlos Vega
  - TICKET-003 (how-to) → frontline agent
  - TICKET-009 (dark mode request) → product feedback
- **Housekeeping:** `CLAUDE.md` points to `context/current_escalations.md`, but the actual file is `current_escalations_1.md`.
