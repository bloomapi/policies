## Goal

Implement the immediate HIPAA policy cleanup decisions:

- Standardize BloomAPI/BloomText customer-facing BAA breach and security incident customer notice timelines to 10 business days.
- Preserve stricter downstream/subcontractor notice timelines unless counsel explicitly approves matching downstream and customer-facing timelines.
- Replace the stale HIPAA inheritance table with a practical shared responsibility matrix.
- Add a subprocessor policy/listing document covering GCP, Sentry, PostHog, and self-hosted Grafana at a level that does not overstate PHI/Part 2 readiness.
- Update audit logging and retention policy language to reflect current reality and capture retention TODOs that must be verified.
- Keep infrastructure language non-brittle and aligned with current GCP/Cloud Armor usage.

## Why

- Current BAA templates conflict: 4 hours, 3 business days, 5 business days, 10 business days, and the attached signed sample BAA says 30 calendar days.
- Customers need a clear shared responsibility model so BloomText does not imply customers inherit full HIPAA/Part 2 compliance.
- The policies should describe what BloomText actually logs today: Cloud Armor HTTP/WAF traffic, machine logs, login/access activity data, Grafana alerts, Sentry alerts, and related incident records.
- Subprocessors like Sentry and PostHog need explicit review status because PHI exposure depends on configuration and scrubbing.

## What

The repository will contain draft policy updates prepared for counsel review and operational verification. The plan does not require changing runtime systems. It updates documentation to match current intent, avoids unsupported compliance claims, and flags operational checks as TODOs where facts are not yet known.

### Success Criteria

- [x] Customer-facing BAA templates use 10 business days for Breach of Unsecured PHI, successful Security Incidents, and impermissible non-breach PHI uses/disclosures unless counsel later chooses a different distinction.
- [x] Downstream/subcontractor BAA templates either preserve stricter notice timelines or explicitly document the accepted operational risk of matching the customer-facing 10 business day deadline.
- [x] The markdown BAA typo “no less than fourteen business days” is removed.
- [x] `breach_policy.md` no longer promises 4-hour customer notice unless the business deliberately keeps that as an internal target.
- [x] `hipaa_inheritance.md` is replaced with `shared_responsibility_matrix.md`.
- [x] A subprocessor document exists and is linked from `README.md` and `3rd_party_policy.md`.
- [x] `auditing_policy.md` lists current log sources and separates current controls from retention TODOs.
- [x] `data_retention_policy.md` includes retention-check TODOs instead of unsupported retention claims.
- [x] Existing signed agreements disclaimer is present where readers could otherwise think repository updates amend executed contracts.
- [x] A no-overclaim scan has been run and each match is removed, softened, or justified.
- [x] `git diff --check` passes.
- [x] Local markdown links resolve.

## All Needed Context

### Documentation & References

```yaml
- url: https://www.hhs.gov/hipaa/for-professionals/breach-notification/index.html
  why: HIPAA breach notification baseline; BA notice is without unreasonable delay and no later than 60 days, but contracts can set shorter timelines.

- url: https://www.hhs.gov/ocr/privacy/hipaa/understanding/coveredentities/contractprov.html
  why: HHS sample BAA provisions and required BA contract topics.

- url: https://www.hhs.gov/hipaa/for-professionals/compliance-enforcement/audit/protocol/index.html
  why: Audit protocol categories for audit controls, information system activity review, and documentation evidence.

- url: https://www.hhs.gov/hipaa/for-professionals/regulatory-initiatives/fact-sheet-42-cfr-part-2-final-rule/index.html
  why: Part 2 final rule effective/compliance dates and HIPAA alignment.

- url: https://www.ftc.gov/node/78112
  why: FTC Health Breach Notification Rule amendments effective July 29, 2024.

- file: baa_covered_entity.txt
  why: Existing customer-facing BAA template currently uses 10 business days.

- file: baa_downstream.txt
  why: Existing downstream BAA currently uses 3/5 business day reporting windows.

- file: bloomapi_hipaa_business_associate_agreement.md
  why: Existing markdown BAA currently uses 4 hours and has an incorrect security incident sentence.

- file: breach_policy.md
  why: Internal breach policy currently says customer notice within 4 hours.

- file: shared_responsibility_matrix.md
  why: Replaces the former HIPAA inheritance table with a shared responsibility matrix.

- file: auditing_policy.md
  why: Needs current log sources and retention TODOs.

- file: data_retention_policy.md
  why: Needs retention-confirmation TODOs.

- file: introduction.md
  why: Already updated to non-brittle GCP/Cloud Armor infrastructure wording; verify it remains aligned.
```

### Files Being Changed

```
README.md                                      ← MODIFIED
introduction.md                                ← MODIFIED
baa_covered_entity.txt                         ← MODIFIED
baa_downstream.txt                             ← MODIFIED
bloomapi_hipaa_business_associate_agreement.md ← MODIFIED
breach_policy.md                               ← MODIFIED
shared_responsibility_matrix.md                ← NEW
3rd_party_policy.md                            ← MODIFIED
auditing_policy.md                             ← MODIFIED
data_retention_policy.md                       ← MODIFIED
subprocessors.md                               ← NEW
```

### Known Gotchas

```text
CRITICAL: Do not claim Sentry or PostHog are approved for PHI unless BloomAPI has verified configuration, scrubbing, and BAA/DPA status.

CRITICAL: Do not use "HIPAA inheritance" language in a way that implies customers become HIPAA compliant by using BloomText. Use "shared responsibility" framing.

CRITICAL: BAA timelines are contractual commitments. Existing signed agreements with different timelines remain binding unless amended.

CRITICAL: HIPAA permits up to 60 days for BA breach notice, but customer BAAs can require a shorter timeline. This plan uses the user's selected 10 business day default.

CRITICAL: Do not treat "successful Security Incident," "Breach of Unsecured PHI," and "impermissible non-breach use/disclosure" as interchangeable. Preserve separate definitions and align only the deadlines selected in this plan.

CRITICAL: For Breaches, use "after discovery" and keep discovery consistent with the breach policy. For impermissible non-breach uses/disclosures and successful Security Incidents, use "after BloomAPI becomes aware" unless counsel instructs otherwise.
```

## Implementation Blueprint

### Architecture Overview

This is a documentation-only cleanup. The immediate implementation should make the policy repository internally consistent and attorney-review-ready by aligning BAA timelines, replacing an overbroad inheritance table with shared responsibility language, and documenting current audit/subprocessor facts without overstating unverified controls.

### Key Pseudocode

```text
For each BAA/policy file:
  locate Breach/Security Incident reporting language
  replace customer-facing Breach notice window with "as soon as practicable, but no later than ten (10) business days after discovery"
  replace customer-facing successful Security Incident and impermissible non-breach use/disclosure windows with "as soon as practicable, but no later than ten (10) business days after BloomAPI becomes aware"
  preserve stricter downstream/subcontractor windows unless counsel approves matching 10 business days
  preserve blanket notice language for unsuccessful Security Incidents
  preserve "supplemental information as available" concept

For shared responsibility matrix:
  replace "Inherited: Yes/No/Partially" with:
    Area | BloomText Responsibility | Customer Responsibility | Evidence/Notes
  include HIPAA, Part 2, breach response, user management, audit logging, subprocessors, retention/deletion, legal requests

For subprocessors:
  create table with status labels:
    Approved/eligible for PHI under verified agreement and approved configuration
    Not approved for PHI
    Not approved for PHI/Part 2 pending review
  mark GCP as primary infrastructure eligible only for covered GCP services under BloomAPI's executed Google Cloud BAA and approved configuration
  mark Sentry/PostHog as not approved for PHI/Part 2 pending review
  treat self-hosted Grafana separately from external subprocessors and document any external alert recipients or underlying providers
```

### Data Models and Structure

No runtime data models. The new subprocessor document should use this markdown structure:

```markdown
# Subprocessors

## Subprocessor Review Policy

## Current Subprocessors

| Subprocessor | Service | Data Processed | PHI/Part 2 Status | Agreement Status | Hosting/Region | Notes |
| --- | --- | --- | --- | --- | --- | --- |

## Review TODOs
```

The shared responsibility matrix should use this markdown structure:

```markdown
# BloomText Shared Responsibility Matrix

## Scope

## Matrix

| Area | BloomText Responsibility | Customer Responsibility | Evidence/Notes |
| --- | --- | --- | --- |
```

### Tasks

```yaml
Task 0:
PRE-EDIT INVENTORY:
  - Run:
    `rg -n "Breach|Security Incident|impermissible|improper|notice|notification|subprocessor|retention|audit" *.md *.txt`
  - Review every affected clause before editing.
  - Pay attention to incident_response_policy.md, part_2_sud_records_policy.md, approved_tools_policy.md, and hipaa_mapping_to_bloomapi_controls.md even if the main edits are elsewhere.

Task 1:
MODIFY introduction.md:
  - VERIFY line 17 remains non-brittle and does not list obsolete technologies such as CockroachDB.
  - KEEP GCP, Google Cloud Armor, managed/self-managed databases, application servers, logging/monitoring, developer systems.
  - KEEP reviewed date as June 2, 2026.

Task 2:
MODIFY baa_covered_entity.txt:
  - CONFIRM breach, impermissible use/disclosure, and successful Security Incident notice use "no later than ten (10) business days".
  - USE "after discovery" for Breach notice.
  - USE "after BloomAPI becomes aware" for impermissible non-breach uses/disclosures and successful Security Incidents.
  - ADD supplemental notice language if missing:
    "Business Associate will supplement the notice as additional information becomes available."
  - PRESERVE unsuccessful Security Incident blanket notice.
  - ADD a short disclaimer:
    "Existing signed agreements remain governed by their executed terms unless amended."

Task 3:
MODIFY baa_downstream.txt:
  - PRESERVE downstream reporting as stricter than customer-facing reporting unless counsel explicitly approves otherwise.
  - Recommended default: keep Breach reporting at three (3) business days and improper disclosure/successful Security Incident reporting at five (5) business days so BloomAPI has buffer to meet the 10 business day customer-facing deadline.
  - If counsel directs downstream timelines to match the 10 business day customer-facing default, document that BloomAPI accepts the operational risk.
  - ADD supplemental notice language if missing.

Task 4:
MODIFY bloomapi_hipaa_business_associate_agreement.md:
  - FIX "on no less than fourteen business (14) days" to "without unreasonable delay and no later than ten (10) business days".
  - CHANGE breach reporting from four (4) hours to ten (10) business days.
  - USE "after discovery" for Breach notice.
  - USE "after BloomAPI becomes aware" for successful Security Incidents.
  - ADD supplemental notice language.
  - PRESERVE statement that unsuccessful Security Incidents are deemed noticed by the BAA.
  - ADD existing signed agreement disclaimer.

Task 5:
MODIFY breach_policy.md:
  - CHANGE customer breach notice from "no later than 4 hours" to "without unreasonable delay and no later than ten (10) business days".
  - OPTIONAL: keep an internal target sentence:
    "BloomAPI attempts to provide an initial operational heads-up sooner when practical, but the contractual notice deadline is governed by the applicable BAA."
  - Ensure Part 2 breach handling remains.

Task 6:
REWRITE shared_responsibility_matrix.md:
  - RENAME heading to "BloomText Shared Responsibility Matrix".
  - Replace inherited yes/no table with:
    Area | BloomText Responsibility | Customer Responsibility | Evidence/Notes.
  - INCLUDE rows:
    BAA
    Permitted PHI use
    Part 2/SUD identification
    Patient consent and authorization
    NPP/Part 2 patient notices
    Customer user provisioning/offboarding
    Customer workforce training
    Infrastructure security
    Encryption
    Audit logging
    Breach response
    Subprocessors
    Data retention/deletion
    Legal/law-enforcement requests
    Customer devices/networks
    Approved tools/data export
    Part 2 record identification/flagging
    Part 2 redisclosure restrictions
    Part 2 law-enforcement/court-order review
    SUD counseling notes if applicable
  - USE "BloomText supports" where the customer owns the legal/clinical decision.
  - AVOID "inherits full compliance" framing.

Task 7:
CREATE subprocessors.md:
  - Add review policy and current subprocessor table.
  - Include:
    Google Cloud Platform / Google Cloud Armor: primary infrastructure, approved/eligible for PHI only for covered GCP services under BloomAPI's executed Google Cloud BAA and approved configuration; details tracked in asset inventory.
    Sentry: error monitoring, not approved for PHI/Part 2 pending contract and technical scrubbing review.
    PostHog: analytics, not approved for PHI/Part 2 pending contract and technical routing review.
    Grafana: self-hosted monitoring; not itself an external subprocessor if truly self-hosted, but document external alert recipients and underlying provider.
  - Add TODOs to verify BAA/DPA, PHI scrubbing, regions, and data categories.
  - Add explicit rule that workforce and product telemetry must not intentionally send PHI, Part 2 records, identifiers, message bodies, patient names, or clinical content to Sentry/PostHog until approval is documented.
  - Include columns for "External recipient?" and "Underlying provider".

Task 8:
MODIFY README.md:
  - Link shared responsibility matrix with current filename `shared_responsibility_matrix.md`.
  - Add Subprocessors link.
  - Avoid adding "HIPAA compliant" or "Part 2 compliant" claims. Prefer "supports customer compliance obligations" and "shared responsibility".

Task 9:
MODIFY 3rd_party_policy.md:
  - Link to subprocessors.md.
  - Add requirement that new subprocessors must be reviewed for PHI/Part 2 exposure, BAA/DPA status, data categories, retention, and breach notice commitments before use.
  - State unapproved tools may not receive PHI/Part 2 records.

Task 10:
MODIFY auditing_policy.md:
  - Rewrite broad promises like "BloomAPI shall log all incoming and outgoing traffic" into current capability statements where appropriate.
  - Add "Current Audit and Security Event Sources" section listing:
    Google Cloud Armor HTTP/WAF logs
    server/machine logs
    customer account login/access events where available
    database last-activity records
    Grafana alerts
    Sentry alerts/errors
    incident tickets/investigation notes
  - Add "Recommended Audit Log Gaps/TODOs" section:
    confirm GCP Cloud Audit Logs for IAM/admin/config changes
    confirm explicit login history vs last activity only
    confirm support/admin customer-account access logs
    confirm failed login/MFA event logging
    confirm production deploy/change logs
  - Clean encoding artifact "45 CFR ¬ß" to "45 CFR §".
  - Fix confusing retention numbering in current policy.
  - Keep raw operational log retention separate from legal/compliance records. Do not collapse the six-year breach investigation retention requirement into all raw logs.

Task 11:
MODIFY data_retention_policy.md:
  - Add "Retention Verification TODOs" section:
    Cloud Armor retention/export
    server machine log retention
    Grafana alert retention
    Sentry event retention
    login history retention
    GCP Cloud Audit Logs retention/export
    database backup retention
    PostHog data retention and PHI exposure
  - Do not set final numbers unless verified.

Task 12:
VALIDATE:
  - Run `git diff --check`.
  - Run markdown link check:
    `ruby -e 'Dir["*.md"].each { |f| File.read(f).scan(/\[[^\]]+\]\(([^)]+)\)/).flatten.each { |link| next if link.start_with?("http", "#", "mailto:"); path = link.split(":").first; puts "#{f}: missing #{link}" unless File.exist?(path) } }'`
  - Run targeted stale phrase scan and review expected downstream/access-request matches manually:
    `rg -n "4 hours|four \\(4\\)|no less than fourteen|CockroachDB|45 CFR ¬ß|201_|three \\(3\\) business|five \\(5\\) business" *.md *.txt`
  - Run no-overclaim scan and remove, soften, or justify each match:
    `rg -n "approved for PHI|HIPAA compliant|Part 2 compliant|inherit|inherits|certified|guarantee|all audit logs|all traffic|maximum retention|readily accessible" *.md *.txt`
  - Manually verify README links, 3rd_party_policy.md link to subprocessors.md, and no old display text says "HIPAA Inheritance for BloomText Customers".
```

### Integration Points

```yaml
POLICY_INDEX:
  - README.md must link subprocessors.md and the shared responsibility matrix.

BAA_CONTRACTS:
  - Existing signed customer agreements remain authoritative.
  - This plan standardizes repo templates for future outbound agreements.
  - Customer-facing templates use 10 business days.
  - Downstream templates remain stricter unless counsel approves otherwise.

THIRD_PARTY_REVIEW:
  - subprocessors.md becomes the table referenced by 3rd_party_policy.md.
```

## Validation Loop

```bash
git diff --check
ruby -e 'Dir["*.md"].each { |f| File.read(f).scan(/\[[^\]]+\]\(([^)]+)\)/).flatten.each { |link| next if link.start_with?("http", "#", "mailto:"); path = link.split(":").first; puts "#{f}: missing #{link}" unless File.exist?(path) } }'
rg -n "4 hours|four \\(4\\)|no less than fourteen|CockroachDB|45 CFR ¬ß|201_|three \\(3\\) business|five \\(5\\) business" *.md *.txt
rg -n "approved for PHI|HIPAA compliant|Part 2 compliant|inherit|inherits|certified|guarantee|all audit logs|all traffic|maximum retention|readily accessible" *.md *.txt
```

## Final Validation Checklist

- [ ] Customer-facing BAA notice windows are intentionally 10 business days.
- [ ] Downstream/subcontractor windows are intentionally stricter or counsel-approved to match.
- [ ] `breach_policy.md` aligns with BAA timeline.
- [ ] Shared responsibility matrix does not overstate customer inheritance.
- [ ] Subprocessor table clearly marks TBD/unapproved PHI status.
- [ ] Audit policy reflects current actual log sources.
- [ ] Retention TODOs are visible and not represented as completed controls.
- [ ] `git diff --check` passes.
- [ ] Markdown link check passes.

## Anti-Patterns to Avoid

- Do not represent TBD vendors as approved for PHI.
- Do not promise faster notice than operations can support.
- Do not remove downstream notice buffer accidentally.
- Do not hide customer-owned compliance responsibilities under "inherited" language.
- Do not add final retention numbers without verifying actual platform settings.

## Deprecated Code / Docs To Remove

- Remove obsolete CockroachDB mention from policy text if any remains.
- Remove `4 hours` customer breach deadline unless retained as non-contractual internal target.
- Remove old `45 CFR ¬ß` encoding artifacts.
- Remove legacy "inheritance" framing that implies customers fully inherit HIPAA compliance.

## Confidence Score

9/10. The implementation is documentation-only and the user's decisions are clear. Remaining risk is legal preference around whether downstream subprocessors should report faster than BloomAPI reports to customers.
