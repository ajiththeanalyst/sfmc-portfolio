# Case Study: Salesforce Hostel Cancellation and Refund Workflow

## Business problem
A residential services team needs a consistent hostel-cancellation process. Routing may vary by room-allocation status, approval requirements, and finance processing. This is an anonymized requirements-design example, not a live specification.

## Objective
Clarify workflow stages, role permissions, duplicate prevention, financial review, and status communication.

## Example actors
Applicant/student • Hostel office • Warden • Chief warden • Finance • Support team. Confirm roles and responsibilities during discovery.

## Proposed high-level workflow
1. User requests cancellation.
2. System validates eligibility and checks for an active request.
3. System determines whether a room is allotted.
4. Route to the agreed reviewer and approval chain.
5. After operational approval, route eligible financial items to Finance.
6. Finance records refund, fee adjustment, or no-refund outcome according to approved policy.
7. System updates final status and notifies the requester.

## Business rules to validate
- Only one active cancellation request may exist per allocation.
- Approval actions depend on role and current status.
- Financial eligibility follows approved policy and dates.
- Accommodation fees and caution/security deposits may be treated differently.
- Exceptions, including admission-cancellation cases, must be documented.
- Operational approval and financial settlement use distinct statuses.
- Each transition records actor, timestamp, and required comments.

## User story
As a student, I want to request hostel cancellation and track progress so I know whether the allocation is cancelled and whether settlement remains.

### Acceptance criteria
- A valid request creates one active request.
- A repeated submission directs the user to the existing request or is blocked.
- Room-allocation status determines the configured approval path.
- Finance review starts only when required after operational approval.
- Finance completion records the outcome and notifies the requester.
- Unauthorized users cannot approve or process financial actions.

## Illustrative status model
Draft → Submitted → Pending Hostel Review → Pending Warden Approval (if applicable) → Pending Chief Warden Approval (if applicable) → Pending Finance → Processing → Completed. Rejected, Returned for Clarification, Withdrawn, or Closed may be added if approved.

## UAT scenarios
| ID | Scenario | Expected result |
|---|---|---|
| HC-01 | No room allotted | Request routes to agreed reviewer |
| HC-02 | Room allotted | Configured approval chain followed |
| HC-03 | Double submission | One active request only |
| HC-04 | Unauthorized approval | Action blocked |
| HC-05 | Rejection | Status/reason saved and requester notified |
| HC-06 | Approvals complete | Finance stage begins only if required |
| HC-07 | Fee ineligible, deposit review applies | Components evaluated independently under policy |
| HC-08 | Finance delayed | Clear pending status; no false completion |
| HC-09 | Notification failure | Failure logged and recovery path available |
| HC-10 | Linked admission cancellation | Documented exception policy applied |

## Reporting ideas
Requests by status and age • Pending approvals by team • Time in each stage • Rejection reasons • Finance backlog • Duplicate and notification failures.

## Open questions
What starts the refund eligibility clock? Which components are refundable? Who owns each approval/SLA? Can a request be withdrawn? How are exceptions audited? Which integration confirms settlement?

**Portfolio note:** Generic analysis example only; proposed design is not represented as deployed.