# Case Study: Salesforce Admission Cancellation Workflow

## Business problem
An education provider needs a controlled way for eligible applicants or students to request admission cancellation, submit required information, and track review decisions. This is an anonymized portfolio scenario, not a live system specification.

## Objective
Define eligibility checks, role-based decisions, status transitions, notifications, duplicate prevention, and testable acceptance criteria.

## Example business rules
1. Eligibility criteria must be confirmed with business owners before implementation.
2. Required fields and documents are validated before submission.
3. One valid submission creates one request with a unique reference and initial status.
4. Only authorized roles can approve, reject, or request clarification.
5. Material status changes trigger approved notifications.
6. Duplicate active requests are blocked or handled idempotently.
7. Decisions, timestamps, and comments are retained under the agreed audit policy.

## User story: Submit a request
As an eligible applicant or student, I want to submit a cancellation request with a reason and required documents so the institution can review it.

### Acceptance criteria
- Given eligibility rules are met, when the user opens the cancellation action, then the request form is available.
- Given a required field or attachment is missing, when the user submits, then a clear validation message is shown and the incomplete request is not submitted.
- Given validations pass, when the user submits once, then one request is created and confirmation is shown.
- Given the user clicks repeatedly, then duplicate active requests are not created.

## Illustrative process
1. User opens cancellation action.
2. System checks eligibility and active duplicate requests.
3. User completes fields and uploads required documents.
4. System creates the request and sends confirmation.
5. Assigned reviewer checks the details.
6. Reviewer approves, rejects, or requests clarification.
7. System updates status and notifies relevant users.

## UAT scenarios
| ID | Scenario | Expected result |
|---|---|---|
| AC-01 | Eligible user submits complete request | One request with correct initial status |
| AC-02 | Required reason missing | Submission blocked with clear message |
| AC-03 | Mandatory attachment missing | Submission blocked |
| AC-04 | Repeated submission clicks | No duplicate active request |
| AC-05 | Unauthorized approval attempt | Action unavailable or access denied |
| AC-06 | Reviewer requests clarification | Status and notification updated |
| AC-07 | Reviewer rejects request | Decision and audit details saved; requester notified |
| AC-08 | Notification service fails | Failure logged with defined retry/escalation path |

## Open questions
Who is eligible? Which roles approve? Which documents are mandatory? Can requests be withdrawn or resubmitted? Are refunds handled in a separate finance process? What reporting, retention, and access rules apply?

## BA artefacts demonstrated
Problem statement • Scope • Business rules • User story • Acceptance criteria • Process outline • UAT scenarios • Dependencies and open questions

**Portfolio note:** This generic example demonstrates requirements analysis; it does not claim every proposed rule has been implemented or deployed.