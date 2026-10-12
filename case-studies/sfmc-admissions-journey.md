# Case Study: SFMC Admissions Communication Journey

## Business problem
An admissions team needs timely communications as prospective students move through lifecycle stages. Messages should reflect current eligibility and avoid repeated or contradictory sends. This is a generic design pattern with no real audience data or production content.

## Objective
Document journey entry criteria, stage-to-template requirements, suppression, re-entry, QA, and monitoring.

## Illustrative lifecycle stages
Unverified • Verified • Application fee pending • Fee paid/application not submitted • Application submitted. Stakeholders must confirm stage definitions and transitions against the authoritative CRM.

## Requirements to confirm per stage
Trigger/source event • Audience eligibility and exclusions • Channel • Approved content and language • Send timing • Re-entry/repeat policy • Exit criteria • Consent and opt-out rules • Owner and approver.

## Example requirements matrix
| Stage | Requirement | Key control |
|---|---|---|
| Unverified | Verification reminder, if approved | Suppress once verified |
| Verified | Next-step guidance | Exclude contacts already beyond this stage |
| Application fee pending | Fee instructions | Suppress after confirmed payment |
| Fee paid/application not submitted | Application completion reminder | Suppress after submission |
| Application submitted | Confirmation and next steps | Prevent duplicate confirmations |

## Data design considerations
Assess stable contact/subscriber key, source record identifier, current stage, stage-change timestamp, eligible channel, email/mobile, locale, consent/suppression indicators, and last communication details. Document mappings, null handling, deduplication, refresh cadence, and retention. Do not publish personal records.

## Journey and automation controls
- Define entry source, filters, and re-entry policy.
- Re-check stage and suppression eligibility before send where supported.
- Prevent stale-stage content after progression.
- Test approved content, links, sender details, personalization, and fallback values.
- Define schedule, expected audience volume, and failure alerts.
- Monitor sends, exclusions, errors, and unexpected audience growth.
- Reconcile source, entry, exclusion, and send counts.

## User story
As an admissions communications owner, I want eligible prospects to receive the approved message for their current stage so they get relevant next steps without duplicate or outdated messages.

### Acceptance criteria
- Only records meeting approved entry and suppression rules enter.
- Contacts beyond a stage are excluded from stale-stage messages.
- Re-entry follows the agreed frequency policy.
- Invalid/missing contact data follows documented rules.
- QA validates personalization, links, sender details, and rendering.
- Monitoring identifies unexpected volume, failed sends, and count discrepancies.

## QA / UAT scenarios
| ID | Scenario | Expected result |
|---|---|---|
| SF-01 | Eligible contact enters | Correct journey path |
| SF-02 | Contact has advanced stage | Stale-stage message suppressed |
| SF-03 | Contact opted out/suppressed | Prohibited channel not used |
| SF-04 | Email/mobile invalid | Documented exclusion/fallback applied |
| SF-05 | Contact re-enters | Re-entry policy enforced |
| SF-06 | Personalization field null | Approved fallback renders |
| SF-07 | Audience unexpectedly high | Alert/investigation triggered |
| SF-08 | Journey/automation failure | Failure visible and recovery documented |
| SF-09 | Template/link changed | Regression checks pass before release |
| SF-10 | CRM stage changes mid-journey | Exit/re-check behavior follows design |

## Release checklist
Business sign-off • Field mapping review • Audience count reconciliation • Consent/suppression/deduplication validation • Content and link QA • Re-entry/exit/schedule confirmed • Monitoring and stop procedure documented • UAT evidence retained.

## Open questions
Which system is authoritative for stage/payment? What refresh delay is acceptable? Which consent rules apply? What send windows/frequency caps are allowed? Which volume thresholds trigger alerts? Who approves content and production release?

**Portfolio note:** Generic requirements-design example only; it does not claim the journey is configured or deployed.