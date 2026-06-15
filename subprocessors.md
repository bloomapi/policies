# Subprocessors

BloomAPI reviews third-party services before they are permitted to create, receive, maintain, or transmit PHI or Part 2 records for BloomAPI. This document summarizes current subprocessor status for compliance review. It does not amend any signed agreement.

## Subprocessor Review Policy

1. New subprocessors must be reviewed before use with PHI or Part 2 records.
2. Review must consider data categories, PHI/Part 2 exposure, agreement status, security controls, retention, breach notice commitments, hosting location, and whether the service is an external recipient.
3. Services that are not authorized for PHI or Part 2 records may not intentionally receive PHI, Part 2 records, patient identifiers, message bodies, patient names, clinical content, or other regulated Customer data.
4. Existing signed agreements remain governed by their executed terms unless amended in writing by the parties.

## Current Subprocessors and Related Services

| Service | Purpose | Data Processed | PHI/Part 2 Status | Agreement Status | External Recipient? | Underlying Provider | Hosting/Region | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Google Cloud Platform / Google Cloud Armor | Primary infrastructure, hosting, network security, and HTTP/WAF traffic protection | Production infrastructure data, network/security logs, and Customer data processed by covered services | Approved/eligible for PHI only for covered GCP services under BloomAPI's executed Google Cloud BAA and approved configuration; Part 2 use depends on Customer identification and approved configuration | Verify current BAA and covered services list | Yes | Google Cloud | us-central1 (US) | Region confirmed; details should be tracked in BloomAPI's asset inventory and third-party inventory. |
| Twilio | SMS delivery and messaging services | Patient phone numbers and SMS delivery metadata; message content where used by Customer workflows | Authorized for PHI identifiers and related messaging data under approved configuration; Part 2 use depends on Customer identification and approved configuration | BAA signed - attach/verify in BAA register | Yes | Twilio | To verify | Limit data sent to Twilio to what is necessary for messaging delivery and related operations. |
| SendGrid (Twilio) | Email delivery | Patient email addresses and email delivery metadata; email content where used by Customer workflows | Authorized for PHI identifiers and related email delivery data under approved configuration; Part 2 use depends on Customer identification and approved configuration | BAA signed - attach/verify in BAA register | Yes | Twilio / SendGrid | To verify | Limit data sent to SendGrid to what is necessary for email delivery and related operations. |
| Elastic Cloud | Search infrastructure | Search index data, which may contain message content, identifiers, and operational metadata | Authorized for PHI under approved configuration; Part 2 use depends on Customer identification and approved configuration | BAA signed - attach/verify in BAA register | Yes | Elastic | To verify | Search index contents must be protected as regulated Customer data when they include PHI, identifiers, message content, or Part 2 records. |
| Talkbox | Video service; currently inactive | Video session data and related identifiers if used | Authorized if used under approved configuration; Part 2 use depends on Customer identification and approved configuration | BAA signed - attach/verify in BAA register | Yes | Talkbox | To verify | Currently inactive. Re-review configuration, data flows, and agreement status before renewed production use. |
| Sentry | Error monitoring and application diagnostics | Error events, stack traces, metadata, and possible identifiers depending on configuration | Not authorized for PHI/Part 2 pending contract and technical scrubbing review | Verify BAA/DPA and configuration | Yes | Sentry | To verify | No PHI or Part 2 records should reach Sentry by design. Workforce and product telemetry must not intentionally send identifiers, message bodies, patient names, clinical content, or other regulated Customer data to Sentry until approval is documented. |
| PostHog | Product analytics | Product usage events and possible user/account metadata depending on configuration | Not authorized for PHI/Part 2 pending contract and technical routing review | Verify BAA/DPA and configuration | Yes | PostHog | To verify | No PHI or Part 2 records should reach PostHog by design. Product analytics must not intentionally include patient identifiers, message bodies, patient names, clinical content, or other regulated Customer data until approval is documented. |
| Grafana | Monitoring dashboards and alerts | Metrics, operational alerts, and observability data | Self-hosted monitoring; PHI/Part 2 status depends on what metrics, logs, labels, and alert destinations contain | Self-hosted; verify any external alert delivery channels | No, if fully self-hosted; verify alert destinations | GCP or other hosting provider to verify | To verify | Grafana itself is not an external subprocessor if self-hosted, but alert delivery channels, authentication providers, and notification destinations may be subprocessors. |

## Review TODOs

* Maintain a BAA register for GCP, Twilio, SendGrid, Elastic Cloud, Talkbox, and any other service authorized to create, receive, maintain, or transmit PHI or Part 2 records. The register should include agreement location, signing date, renewal or review date, covered services, and owner.
* Confirm Cloud Armor, GCP Cloud Audit Logs, and Sentry log/event retention periods.
* Confirm Sentry DPA/BAA status, data residency, event retention, scrubbing rules, allowed fields, and continued technical controls preventing PHI or Part 2 records from reaching Sentry.
* Review this document at least annually and after any material vendor, data-flow, or configuration change.
