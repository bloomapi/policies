# Data Retention Policy

Despite not being a requirement within HIPAA, BloomAPI understand and appreciates the importance of health data retention. Acting as a subcontractor, and at times a business associate, BloomAPI is not directly responsible for health and medical records retention as set forth by each state. Despite this, BloomAPI has created and implemented the following policy to make it easier for BloomAPI Customers to support data retention laws.

## State Medical Record Laws

* [Listing of state requirements for medical record retention](http://www.healthit.gov/sites/default/files/appa7-1.pdf)

## Data Retention Policy

* Current BloomAPI Customers have data stored by BloomAPI as a part of the BloomAPI Service.
* Once a Customer ceases to be a Customer, as defined below, the following steps are followed:
	1. Customer is sent a notice via email of change of standing, and given the option to reinstate account.
	2. If no response to notice in #1 above within 7 days, or if Customer responds they do not want to reinstate account, Customer is sent directions for how to download their data from BloomAPI.
	3. If Customer downloads data or does not respond to notices from BloomAPI within 30 days, BloomAPI may remove data from BloomAPI systems and Customer is sent notice of removal of data.
	4. Customer data retained in backups, logs, legal holds, security records, or other systems where immediate deletion is infeasible remains protected under BloomAPI policies and applicable agreements until it is deleted or destroyed in the normal retention cycle.
	5. Part 2 records are retained, returned, or destroyed according to Customer instructions, applicable Part 2 agreements, legal holds, and applicable law.
	6. Cloud Spanner backups are retained for 30 days.

## Retention Verification TODOs

The following retention details must be verified before final retention periods are represented as completed controls:

* Google Cloud Armor log retention and export configuration.
* Server and machine log retention.
* Grafana alert history retention.
* Sentry event retention and whether PHI or Part 2 data can reach Sentry.
* Customer login history retention and whether the system stores full login history or only last activity.
* GCP Cloud Audit Logs retention and export configuration for IAM, administrative, and configuration changes.
* PostHog event retention and whether PHI or Part 2 data can reach PostHog.
