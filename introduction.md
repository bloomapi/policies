# Introduction

BloomAPI, Inc ("BloomAPI") is committed to ensuring the confidentiality, privacy, integrity, and availability of all electronic protected health information (ePHI) it receives, maintains, processes and/or transmits on behalf of its customers. BloomAPI operates BloomText, a secure messaging product that healthcare provider organizations use to communicate with patients and colleagues. BloomAPI acts as a HIPAA Business Associate for these Customers. BloomAPI strives to maintain compliance, proactively address information security, mitigate risk for its Customers, and assure known breaches are completely and effectively communicated in a timely manner. The following documents address core policies used by BloomAPI to maintain compliance and assure the proper protections of infrastructure used to store, process, and transmit ePHI for BloomAPI Customers.

## Shared Responsibility

BloomAPI provides software and infrastructure controls that support Customer compliance obligations.

BloomAPI signs business associate agreements (BAAs) with its Customers. These BAAs outline BloomAPI obligations and Customer obligations, as well as liability in the case of a breach. In providing infrastructure and managing security configurations that are part of HIPAA, HITRUST, and other compliance frameworks, BloomAPI manages certain technical and operational safeguards for Customers. Customers remain responsible for their own legal, clinical, administrative, workforce, patient notice, consent, and account administration obligations.

Certain aspects of compliance are Customer-owned. Because of this, BloomAPI Customers must implement their own organizational policies and procedures to meet obligations that fall outside of BloomAPI's services and agreements.

Below are mappings of HIPAA Rules to BloomAPI controls and a shared responsibility matrix describing which obligations BloomAPI supports and which obligations remain Customer-owned.

## BloomAPI Organizational Concepts

The physical infrastructure environment is hosted in Google Cloud Platform (GCP). Network components and supporting network infrastructure are contained within GCP infrastructure and managed by GCP. BloomAPI does not have physical access to the network components. The BloomAPI production environment runs in the GCP us-central1 region and uses a regional Google Kubernetes Engine (GKE) cluster for application services, Cloud Spanner as the primary database, Cloud Storage for file attachments and backups, Cloud SQL for the data warehouse, Google Cloud Armor and GCP firewall rules for network protection, and Google Cloud Logging and Grafana for logging and monitoring. Search indexing runs on Elastic Cloud. Infrastructure is defined in Terraform. Specific systems, third-party subprocessors, and data flows are tracked in BloomAPI's internal asset inventory and third-party inventory.

Within the BloomAPI Platform all data transmission is encrypted and all hard drives are encrypted so data at rest is also encrypted; this applies to all servers - databases, APIs, log servers, etc. BloomAPI assumes all data *may* contain ePHI, even though our Risk Assessment does not indicate this is the case, and provides appropriate protections based on that assumption.

## Version Control

Policies were last reviewed and updated November 16, 2026, by Tyler Brown, HIPAA Security Officer. They are reviewed at least annually (see the [Policy Management Policy](policy_management_policy.md)).
