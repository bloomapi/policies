## Goal

Create the future implementation plan for strengthening BloomAPI/BloomText's HIPAA, Part 2, audit, retention, and vendor compliance program after the immediate documentation cleanup is implemented.

This future plan should not add aspirational claims to customer-facing policies until the operational controls are confirmed or implemented.

## Why

- The immediate policy cleanup will make the repository internally consistent, but several controls require operational confirmation before policies should claim them.
- HIPAA, Part 2, customer BAAs, and vendor management expectations require evidence: inventories, access reviews, logs, incident records, vendor agreements, and retention records.
- A future plan lets BloomAPI build the evidence program before adding stronger public or customer-facing claims.

## What

Implement an evidence-backed compliance expansion across six areas:

1. Operational audit logging and retention.
2. Subprocessor/vendor review and PHI/Part 2 approval status.
3. Customer onboarding classification for HIPAA and Part 2.
4. Access review and administrative activity logging.
5. Incident and breach evidence records.
6. Customer-facing compliance artifacts.

### Success Criteria

- [ ] BloomAPI has a verified log inventory with owner, source, retention, export/archive status, PHI exposure, and incident-use value.
- [ ] Subprocessors have verified BAA/DPA status, data categories, PHI/Part 2 approval status, and retention/security posture.
- [ ] Customer onboarding captures whether HIPAA, Part 2, SUD counseling notes, or other specially protected data is involved.
- [ ] Administrative/support access to customer accounts is logged or a gap is formally tracked.
- [ ] GCP Cloud Audit Logs/IAM/admin/config logs are confirmed and exported if needed.
- [ ] Retention tiers are approved by leadership/counsel and reflected in policy only after implementation.
- [ ] Customer-facing compliance docs are updated only after evidence exists.

## All Needed Context

### Documentation & References

```yaml
- url: https://www.hhs.gov/hipaa/for-professionals/security/laws-regulations/index.html
  why: HIPAA Security Rule administrative, physical, and technical safeguard context.

- url: https://www.hhs.gov/hipaa/for-professionals/compliance-enforcement/audit/protocol/index.html
  why: HHS audit protocol for evidence expectations.

- url: https://www.hhs.gov/hipaa/for-professionals/security/hipaa-security-rule-nprm/factsheet
  why: Proposed Security Rule cybersecurity readiness items; treat as readiness, not final law.

- url: https://www.hhs.gov/hipaa/for-professionals/regulatory-initiatives/fact-sheet-42-cfr-part-2-final-rule/index.html
  why: Part 2 final rule requirements and February 16, 2026 compliance date.

- file: tmp/done-plans/2026-06-02-immediate-hipaa-policy-cleanup.md
  why: This future plan assumes the immediate cleanup has been implemented first.

- file: auditing_policy.md
  why: Will be updated after log inventory is verified.

- file: data_retention_policy.md
  why: Will receive final retention tiers after operational verification.

- file: 3rd_party_policy.md
  why: Will be updated after subprocessor review is completed.

- file: part_2_sud_records_policy.md
  why: Will be updated after onboarding/customer classification process is implemented.

- file: shared_responsibility_matrix.md
  why: Shared responsibility matrix may get evidence links after controls are verified.
```

### Files Being Changed

```
.context/compliance/log-inventory.md             ← NEW
.context/compliance/subprocessor-review.md       ← NEW
.context/compliance/customer-onboarding-check.md ← NEW
.context/compliance/access-review-template.md    ← NEW
.context/compliance/incident-evidence-template.md← NEW
.context/compliance/policy-claim-register.md     ← NEW
auditing_policy.md                               ← MODIFIED
data_retention_policy.md                         ← MODIFIED
3rd_party_policy.md                              ← MODIFIED
part_2_sud_records_policy.md                     ← MODIFIED
systems_access_policy.md                         ← MODIFIED
policy_management_policy.md                      ← MODIFIED
subprocessors.md                                 ← MODIFIED
shared_responsibility_matrix.md                  ← MODIFIED
```

### File Classification

| File | Classification | Unverified facts allowed? | Notes |
| --- | --- | --- | --- |
| `.context/compliance/*.md` | Internal evidence | Yes | May contain `Needs verification`, artifact locations, reviewer notes, and internal gaps. |
| `policy_management_policy.md` | Internal/customer-visible policy | No | Add governance rule before publishing stronger claims. |
| `auditing_policy.md` | Internal/customer-visible policy | No | Only verified log sources, neutral capability statements, and approved limitations. |
| `data_retention_policy.md` | Internal/customer-visible policy | No | Final retention numbers only after operational verification and approval. |
| `subprocessors.md` | Customer-facing summary | Limited | May say `Not approved for PHI/Part 2 pending review`; must not expose contracts, sensitive configs, or unsupported approvals. |
| `shared_responsibility_matrix.md` | Customer-facing shared responsibility matrix | No | High-level customer-safe responsibilities only; no internal evidence paths. |
| `part_2_sud_records_policy.md` | Internal/customer-visible policy | No | Treat Part 2 compliance as current-state requirement as of February 16, 2026. |
| `systems_access_policy.md` | Internal/customer-visible policy | No | Only verified access review and admin logging practices. |

### Known Gotchas

```text
CRITICAL: Do not update public/customer-facing policies to say a control exists until the control is actually implemented or verified.

CRITICAL: PostHog and Sentry may be unacceptable for PHI depending on configuration and agreement status. Treat them as "not approved for PHI" until verified.

CRITICAL: GCP Cloud Audit Logs are not the same as application/user activity logs. Both may be needed for investigations.

CRITICAL: A database field containing "last activity" is not a complete login audit trail.

CRITICAL: Future Security Rule NPRM items are readiness controls unless finalized by HHS with a compliance date.

CRITICAL: `.context/compliance/*` may contain unverified facts. Customer-facing or mixed policy files may contain only verified controls, approved limitations, or neutral statements.

CRITICAL: Do not let internal evidence paths, ticket IDs, screenshots, vendor contract details, sensitive log locations, or known gaps leak into customer-facing files.

CRITICAL: Treat the Part 2 compliance date as current-state. Compliance was required by February 16, 2026; this plan is not future readiness for Part 2.
```

## Implementation Blueprint

### Architecture Overview

The future implementation builds an evidence layer around the policies. First create internal inventories/templates in `.context/compliance/` so the team can collect facts without prematurely changing customer-facing claims. After each operational control is verified, update the corresponding policy with specific retention, review cadence, owner, and evidence references.

### Key Pseudocode

```text
Phase A: Evidence collection
  create internal templates
  fill in current facts from engineering/compliance
  mark each item: Verified / Needs Work / Not Approved for PHI / Not Applicable
  Verified requires: source, date verified, verifier, artifact location, next review, and scope

Phase B: Control implementation
  for each Needs Work item:
    assign owner
    implement operational control or document compensating control
    record evidence location and review cadence

Phase C: Policy update
  only after verification:
    update public/internal policy with exact control
    add retention periods
    add owner and cadence
    add exception process
    Security Officer, Privacy Officer, and counsel/leadership approve customer-facing claims where relevant
```

### Data Models and Structure

Internal inventory files should be markdown tables:

```markdown
| Control/Source | Owner | Current State | PHI/Part 2 Exposure | Retention | Evidence Location | Status | Next Action |
| --- | --- | --- | --- | --- | --- | --- | --- |
```

Subprocessor review should use:

```markdown
| Vendor | Service | Data Categories | PHI Allowed | Part 2 Allowed | BAA/DPA | Retention | Region | Status | Owner | Next Review |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
```

Customer onboarding classification should use:

```markdown
| Question | Required? | Owner | Notes |
| --- | --- | --- | --- |
| Will customer use BloomText for PHI? | Yes | Sales/Compliance | Required before BAA |
| Is customer a Part 2 program or lawful holder? | Yes | Sales/Compliance | Required for SUD treatment customers |
| Will SUD counseling notes be stored/transmitted? | Yes | Customer/Compliance | Requires special handling |
```

Policy claim register should use:

```markdown
| Policy Claim | Customer-Facing File | Required Evidence | Evidence Status | Approved By | Published? | Notes |
| --- | --- | --- | --- | --- | --- | --- |
```

### Tasks

```yaml
Task 1:
MODIFY policy_management_policy.md:
  - Add a governance rule before other policy updates:
    "BloomAPI policies may not claim a security, privacy, retention, logging, vendor, or compliance control is operating unless implementation evidence exists or the policy clearly identifies the statement as a planned or under-review item in an internal-only document."
  - Add annual regulatory watch review for HIPAA, Part 2, FTC HBNR, and state breach laws.
  - Add approval requirement for customer-facing policy claims: Security Officer, Privacy Officer, and counsel/leadership where appropriate.

Task 2:
CREATE .context/compliance/log-inventory.md:
  - Include Cloud Armor HTTP/WAF logs.
  - Include server/machine logs.
  - Include login/account access events.
  - Include database last-activity records.
  - Include Grafana alerts.
  - Include Sentry alerts/errors.
  - Include GCP Cloud Audit Logs/IAM/admin/config logs as "Needs verification".
  - Include deploy/change logs as "Needs verification".
  - Include support/admin customer-account access as "Needs verification".
  - For each: owner, retention, searchable window, archive/export, PHI/Part 2 exposure, evidence location.
  - Each `Verified` row must include source, date verified, verifier, artifact location, next review, and scope.

Task 3:
CREATE .context/compliance/subprocessor-review.md:
  - Add GCP, Sentry, PostHog, Grafana/self-hosted.
  - Add fields for BAA/DPA, PHI allowed, Part 2 allowed, data categories, retention, region, security review date.
  - Mark Sentry/PostHog PHI/Part 2 as "Not approved until verified" unless evidence exists.
  - Require both contract and configuration evidence before approval: BAA/DPA status, scrubbing, event filters, sampling, allowed fields, data residency, retention, and proof PHI/Part 2 data is not routed there unless approved.

Task 4:
CREATE .context/compliance/customer-onboarding-check.md:
  - Add HIPAA/BAA required questions.
  - Add Part 2/SUD classification questions.
  - Add SUD counseling notes question.
  - Add patient consent/NPP/customer workforce responsibilities acknowledgement.
  - Add customer admin/user offboarding acknowledgement.
  - Separate customer classification evidence from customer legal compliance claims. Capturing that Part 2 applies does not mean BloomAPI has verified the customer's consents, notices, or workforce compliance.

Task 5:
CREATE .context/compliance/access-review-template.md:
  - Include production access.
  - Include cloud console/IAM.
  - Include source code and deployment systems.
  - Include monitoring/logging tools.
  - Include support/admin access to customer environments.
  - Include quarterly privileged review and annual general access review.

Task 6:
CREATE .context/compliance/incident-evidence-template.md:
  - Include incident timeline.
  - Include affected systems.
  - Include PHI/Part 2/reproductive health/special records assessment.
  - Include breach low-probability assessment factors.
  - Include customer notice timeline and supplemental updates.
  - Include logs/evidence reviewed.
  - Include root cause and corrective actions.

Task 7:
CREATE .context/compliance/policy-claim-register.md:
  - Track each customer-facing policy claim and required evidence.
  - Include Policy Claim, Customer-Facing File, Required Evidence, Evidence Status, Approved By, Published?, and Notes.
  - Use this register to decide whether a policy statement can be promoted from internal evidence to customer-facing documentation.

Task 8:
VERIFY operational logging:
  - Confirm Cloud Armor retention/export.
  - Confirm server log retention.
  - Confirm whether machine login logs can reconstruct customer-account login history.
  - Confirm database last-activity limitations.
  - Confirm Grafana alert retention.
  - Confirm Sentry retention and PHI scrubbing.
  - Confirm GCP Cloud Audit Logs are enabled for admin/IAM/config changes.
  - Confirm production deploy/change logs.
  - Confirm support/admin access logs.

Task 9:
IMPLEMENT or track logging gaps:
  - If explicit login history does not exist, create an engineering ticket before policy claims it.
  - If GCP Cloud Audit Logs are not exported/retained long enough, create an engineering ticket.
  - If support/admin customer-account access is not logged, create an engineering ticket.
  - If failed login/MFA events are not retained, create an engineering ticket.

Task 10:
APPROVE retention tiers:
  - Propose:
    raw machine logs: 30-90 days searchable
    security/auth/admin/customer-access logs: 1 year searchable or archived
    incident/breach/risk/access-review/policy records: 6 years
  - Review with counsel/leadership.
  - Implement operational retention before updating policy.

Task 11:
IMPLEMENT or create tickets for onboarding workflow changes:
  - Update CRM, sales forms, contract workflows, product admin, or other actual onboarding systems to capture HIPAA and Part 2 classification.
  - If those systems are outside this repo, create explicit implementation tickets before any policy claims onboarding classification is operating.
  - Include customer-owned acknowledgements without implying BloomAPI verified customer legal compliance.

Task 12:
MODIFY auditing_policy.md after verification:
  - Add verified log inventory categories and retention.
  - Add owner and review cadence.
  - Add evidence retention requirements.
  - Promotion criteria: every referenced log source must have source, owner, retention, searchable window, export/archive behavior, PHI/Part 2 exposure, verifier, and review cadence marked Verified in log-inventory.md.
  - Use neutral fallback language for unverified controls, such as "BloomAPI maintains audit logging appropriate to the service and reviews log coverage periodically," only if true.

Task 13:
MODIFY data_retention_policy.md after retention tiers are implemented:
  - Replace TODOs with final retention tiers.
  - Include backup deletion cycle, legal hold, customer deletion, and Part 2 handling.
  - Promotion criteria: retention tier is implemented or enforceable, owner is assigned, exception/legal hold process is documented, and counsel/leadership approval is recorded.

Task 14:
MODIFY 3rd_party_policy.md and subprocessors.md after vendor review:
  - Move vendors from TBD to approved/not approved.
  - Add review cadence.
  - Add requirement to re-review after material vendor/configuration change.
  - Keep `subprocessors.md` as customer-facing summary only. Detailed BAA/DPA terms, configuration proof, security review notes, and PHI/Part 2 routing evidence stay in `.context/compliance/subprocessor-review.md`.
  - Apply redaction/minimum-necessary rule before publishing vendor details.

Task 15:
MODIFY part_2_sud_records_policy.md after onboarding is implemented:
  - Reference the onboarding classification process.
  - Add owner and retention of Part 2 classification evidence.
  - Treat Part 2 as current-state compliance, not future readiness.
  - Promotion criteria: onboarding workflow actually captures Part 2/SUD status or an explicit implementation ticket exists and the policy does not claim it is operating.

Task 16:
MODIFY systems_access_policy.md after access review process is running:
  - Reference access-review evidence template.
  - Add support/admin customer-account access controls if implemented.
  - Promotion criteria: access-review cadence has evidence, privileged population is defined, reviewer is assigned, and exceptions are documented.

Task 17:
MODIFY shared_responsibility_matrix.md:
  - Keep customer-owned items explicit.
  - Keep the shared responsibility matrix high-level and customer-safe.
  - Do not add internal evidence references; maintain evidence mappings in `.context/compliance/policy-claim-register.md`.
```

### Integration Points

```yaml
INTERNAL_EVIDENCE:
  - .context/compliance/ files are gitignored collaboration/evidence planning docs.
  - Policy files should only cite stable evidence practices, not transient tickets.

VENDOR_MANAGEMENT:
  - subprocessors.md becomes public/internal policy inventory.
  - .context/compliance/subprocessor-review.md captures detailed review evidence.

CUSTOMER_ONBOARDING:
  - Future implementation likely requires changes outside this policy repo if onboarding lives in CRM, sales forms, contract workflow, or product admin.
  - Create explicit tickets before policies claim those processes are operating.
```

## Validation Loop

```bash
git diff --check
ruby -e 'Dir["*.md"].each { |f| File.read(f).scan(/\[[^\]]+\]\(([^)]+)\)/).flatten.each { |link| next if link.start_with?("http", "#", "mailto:"); path = link.split(":").first; puts "#{f}: missing #{link}" unless File.exist?(path) } }'
rg -n "TBD|Needs verification|Not approved until verified" .context/compliance *.md
# Customer-facing docs should not contain unapproved placeholders except explicit customer-safe "not approved pending review" vendor statuses:
rg -n "TBD|Needs verification|Not approved until verified" *.md
```

If the second command returns matches in customer-facing files, either move details to `.context/compliance/`, replace with approved neutral language, or document why the match is intentionally customer-safe.

Run no-overclaim scan:

```bash
rg -n "approved for PHI|HIPAA compliant|Part 2 compliant|inherit|inherits|certified|guarantee|all audit logs|all traffic|maximum retention|readily accessible" *.md *.txt
```

## Final Validation Checklist

- [ ] Future-facing policy claims are backed by operational evidence.
- [ ] Vendors have PHI/Part 2 status labels.
- [ ] Log inventory covers Cloud Armor, machine logs, login/access events, Grafana, Sentry, and GCP audit logs.
- [ ] Retention tiers are approved and implemented before policy claims are finalized.
- [ ] Customer onboarding captures HIPAA and Part 2 status.
- [ ] Access review evidence exists before policies claim quarterly reviews are operating.
- [ ] Policy claim register exists and customer-facing claims are approved.
- [ ] No internal evidence paths or sensitive details leak into customer-facing files.
- [ ] Customer-facing docs use redacted/minimum-necessary compliance descriptions.

## Anti-Patterns to Avoid

- Do not put unverified controls into customer-facing docs.
- Do not say "PHI allowed" for Sentry/PostHog without contractual and technical validation.
- Do not treat last-activity timestamps as full audit logs.
- Do not update retention policy with numbers that engineering cannot enforce.
- Do not blur BloomText-owned responsibilities with customer-owned legal/clinical obligations.
- Do not publish sensitive logging architecture, incident evidence, vendor contract terms, or internal control gaps in customer-facing artifacts.
- Do not use "Verified" without source, date verified, verifier, artifact location, next review, and scope.

## Deprecated Code / Docs To Remove

- Remove "TBD" and "Needs verification" placeholders from customer-facing files. Keep unverified detail in `.context/compliance/`.
- Remove or revise any claim that customers fully inherit controls that remain customer-owned.
- Remove vendor entries that are no longer used after subprocessor review.

## Confidence Score

8/10. This plan is intentionally evidence-first. Implementation success depends on engineering/compliance being able to verify actual log retention, vendor contracts, and onboarding workflows.
