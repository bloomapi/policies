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
| Google Cloud Platform / Google Cloud Armor | Primary infrastructure, hosting, network security, and HTTP/WAF traffic protection | Production infrastructure data, network/security logs, and Customer data processed by covered services | Approved/eligible for PHI only for covered GCP services under BloomAPI's executed Google Cloud BAA and approved configuration; Part 2 use depends on Customer identification and approved configuration | Verify current BAA and covered services list | Yes | Google Cloud | GCP / region to verify | Details should be tracked in BloomAPI's asset inventory and third-party inventory. |
| Sentry | Error monitoring and application diagnostics | Error events, stack traces, metadata, and possible identifiers depending on configuration | Not authorized for PHI/Part 2 pending contract and technical scrubbing review | Verify BAA/DPA and configuration | Yes | Sentry | To verify | Workforce and product telemetry must not intentionally send PHI, Part 2 records, identifiers, message bodies, patient names, or clinical content to Sentry until approval is documented. |
| PostHog | Product analytics | Product usage events and possible user/account metadata depending on configuration | Not authorized for PHI/Part 2 pending contract and technical routing review | Verify BAA/DPA and configuration | Yes | PostHog | To verify | Product analytics must not intentionally include PHI, Part 2 records, patient identifiers, message bodies, patient names, or clinical content until approval is documented. |
| Grafana | Monitoring dashboards and alerts | Metrics, operational alerts, and observability data | Self-hosted monitoring; PHI/Part 2 status depends on what metrics, logs, labels, and alert destinations contain | Self-hosted; verify any external alert delivery channels | No, if fully self-hosted; verify alert destinations | GCP or other hosting provider to verify | To verify | Grafana itself is not an external subprocessor if self-hosted, but alert delivery channels, authentication providers, and notification destinations may be subprocessors. |

## Review TODOs

* Confirm Google Cloud BAA status, covered services, hosting regions, Cloud Armor log retention, and approved configurations.
* Confirm Sentry BAA/DPA status, data residency, event retention, scrubbing rules, allowed fields, and whether any PHI/Part 2 data can reach Sentry.
* Confirm PostHog BAA/DPA status, data residency, event retention, allowed fields, and whether any PHI/Part 2 data can reach PostHog.
* Confirm Grafana hosting location, alert destinations, authentication provider, retention, and whether alert payloads contain regulated Customer data.
* Review this document at least annually and after any material vendor, data-flow, or configuration change.
