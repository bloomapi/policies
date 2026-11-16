# Disaster Recovery Policy

The BloomAPI Contingency Plan establishes procedures to recover BloomAPI following a disruption resulting from a disaster. This Disaster Recovery Policy is maintained by the BloomAPI HIPAA Security & Privacy Officer.

The following objectives have been established for this plan:

1. Maximize the effectiveness of contingency operations through an established plan that consists of the following phases:
	* *Notification/Activation phase* to detect and assess damage and to activate the plan;
	* *Recovery phase* to restore temporary IT operations and recover damage done to the original system;
	* *Reconstitution phase* to restore IT system processing capabilities to normal operations.
2. Identify the activities, resources, and procedures needed to carry out BloomAPI processing requirements during prolonged interruptions to normal operations.
3. Identify and define the impact of interruptions to BloomAPI systems.
4. Assign responsibilities to designated personnel and provide guidance for recovering BloomAPI during prolonged periods of interruption to normal operations.
5. Ensure coordination with other BloomAPI staff who will participate in the contingency planning strategies.
6. Ensure coordination with external points of contact and vendors who will participate in the contingency planning strategies.

This Contingency Plan implements the HIPAA Security Rule contingency plan standard, §164.308(a)(7), which requires the establishment and implementation of procedures for responding to events that damage systems containing electronic protected health information. Its structure follows the guidance in National Institute of Standards and Technology (NIST) Special Publication (SP) 800-34, "Contingency Planning Guide for Federal Information Systems".

Example of the types of disasters that would initiate this plan are natural disaster, political disturbances, man made disaster, external human threats, internal malicious activities, and extended outages of a critical vendor.

BloomAPI defined two categories of systems from a disaster recovery perspective.

1. *Critical Systems*. These systems host application servers and database servers or are required for functioning of systems that host application servers and database servers. These systems, if unavailable, affect the integrity of data and must be restored, or have a process begun to restore them, immediately upon becoming unavailable.
2. *Non-critical Systems*. These are all systems not considered critical by definition above. These systems, while they may affect the performance and overall security of critical systems, do not prevent Critical systems from functioning and being accessed appropriately. These systems are restored at a lower priority than critical systems.

## Applicable Standards from the HITRUST Common Security Framework

* 12.c - Developing and Implementing Continuity Plans Including Information Security

## Applicable Standards from the HIPAA Security Rule

* 164.308(a)(7)(i) - Contingency Plan

## Production Environment and Recovery Objectives

* BloomText production runs in Google Cloud Platform (GCP) in the us-central1 region. Application services run on a regional Google Kubernetes Engine (GKE) cluster, whose nodes span multiple zones in the region. Cloud Spanner is the primary datastore and Cloud Storage holds file attachments.
* Infrastructure is defined in Terraform and application workloads in Kubernetes manifests, both kept in version control, so the environment can be recreated from code.
* Production application data in Cloud Spanner is backed up daily. Backups are encrypted and retained for 30 days (see the [Data Management Policy](data_management_policy.md)).
* **Recovery Time Objective (RTO): 24 hours.** Critical systems are restored to normal operation within 24 hours of the plan being activated.
* **Recovery Point Objective (RPO): 24 hours.** Because backups are taken daily, up to 24 hours of data may be lost in a worst-case restore from backup.
* Production depends on a single GCP region. Multi-region failover is not in place today; this is a documented risk in BloomAPI's risk analysis and is re-evaluated at each annual review.

## Line of Succession

The following order of succession ensures that decision-making authority for the BloomAPI Contingency Plan is uninterrupted. The HIPAA Security & Privacy Officer is the Recovery Lead, responsible for ensuring the safety of personnel and the execution of procedures documented within this Contingency Plan. If the Recovery Lead is unable to act or delegates this responsibility, the next person in the list below acts as Recovery Lead. To provide contact initiation should the contingency plan need to be initiated, please use the contact list below.

1. Tyler Brown, CEO and HIPAA Security & Privacy Officer: tyler@bloomapi.com
2. Parsa Khazaeepoul, Engineering: parsa@bloomapi.com

## Responsibilities

BloomAPI is a small team, so recovery responsibilities are assigned to roles rather than standing teams.

1. The **Recovery Lead** declares and coordinates the contingency event, makes recovery decisions, and communicates with Customers, Partners, and vendors.
2. **Engineering** (the workforce members with production access) restores the hosted environment from Terraform, Kubernetes manifests, and backups; verifies application services, logging, security, and alerting; and tests the restored environment before it serves traffic.

## Testing and Maintenance

The Recovery Lead shall establish criteria for validation/testing of the Contingency Plan, an annual test schedule, and ensure implementation of the test. This process will also serve as training for personnel involved in the plan's execution. At a minimum, a backup restore test and a disaster recovery test shall be performed annually (within 365 days) and after material changes to critical systems. The types of validation/testing exercises include technical testing.

Each test is recorded with its date, what was restored, how long it took, whether the RTO and RPO were met, and any follow-up actions. Test records are retained for six years.

### Technical Testing

The primary objective of the technical test is to ensure the communication processes and data storage and recovery processes can function to perform the functions and capabilities of the system within the designated requirements. Technical testing shall include, but is not limited to:

* Restore a Cloud Spanner backup to a separate, non-production instance and verify the restored data;
* Recreate critical infrastructure from Terraform and Kubernetes manifests, or confirm that it can be recreated; and
* Validate recovery point objectives, recovery time objectives, logging, monitoring, and access controls after restoration.

## Business Continuity

This section covers disruptions that are not caused by damage to BloomAPI systems.

### Key-person unavailability

* At least two workforce members must be able to access and operate production systems, so that no single person's absence stops recovery.
* Operational runbooks, infrastructure code, and deployment procedures are kept in the BloomAPI code repository rather than with an individual.
* Access to the accounts needed for recovery (GCP, the domain registrar, the code repository, and critical vendors) must not depend on a single person. Recovery credentials must be kept in a password manager and protected by multi-factor authentication.
* If the Recovery Lead is unavailable, the line of succession above applies.

### Critical vendor outages

* **Google Cloud.** BloomText cannot serve traffic while GCP us-central1 is unavailable. BloomAPI monitors Google Cloud status, informs affected Customers, and recovers once Google restores service. If an outage is expected to exceed the RTO, the Recovery Lead decides whether to restore from backups into another GCP region using the same Terraform and Kubernetes definitions.
* **Twilio (SMS) and SendGrid (email, a Twilio company).** These are used only to deliver notifications. During an outage, messages remain stored and available in BloomText, but SMS or email notifications to patients may be delayed or not delivered. BloomAPI informs affected Customers and, for a prolonged outage, evaluates moving notification delivery to another provider.
* Other subprocessors are listed in [Subprocessors](subprocessors.md). Their loss is handled as a non-critical system unless it prevents critical systems from functioning.

## 1. Notification and Activation Phase

This phase addresses the initial actions taken to detect and assess damage inflicted by a disruption to BloomAPI. Based on the assessment of the Event, sometimes according to the BloomAPI Incident Response Policy, the Contingency Plan may be activated by the Recovery Lead or the next person in the line of succession.

The notification sequence is listed below:

* The first responder is to notify the Recovery Lead. All known information must be relayed to the Recovery Lead.
* The Recovery Lead is to begin assessment procedures with Engineering to determine the extent of damage and estimated recovery time.
	* Damage Assessment Procedures:
	* The Recovery Lead and Engineering are to logically assess damage, gain insight into whether the infrastructure is salvageable, and begin to formulate a plan for recovery.
* The BloomAPI Contingency Plan is to be activated if one or more of the following criteria are met:
	* BloomText is, or is expected to be, unavailable for longer than the RTO.
	* The hosting region or a critical vendor is unavailable and is expected to stay unavailable for more than 24 hours.
	* Other criteria, as appropriate and as defined by BloomAPI.
	* A security incident, ransomware event, or operational failure materially affects the confidentiality, integrity, or availability of ePHI and requires alternate processing or recovery procedures.
* If the plan is to be activated, the Recovery Lead is to notify workforce members of the details of the event and whether recovery to another region is required.
* The Recovery Lead is to notify affected vendors that a contingency event has been declared.
* The Recovery Lead is to keep workforce members and affected Customers informed on the general status of the incident.
* Notification can be message, email, or phone.

## 2. Recovery Phase

This section provides procedures for recovering the application, whereas other efforts are directed to repair damage to the original system and capabilities.

Recovery Goal: The goal is to rebuild BloomAPI infrastructure to a production state within the RTO.

The tasks outlined below are not sequential and some can be run in parallel.

1. Contact Partners and Customers affected - Recovery Lead
2. Assess damage to the environment - Engineering
3. Decide whether to recover in the existing GCP region or another GCP region - Recovery Lead
4. Recreate the environment from Terraform and Kubernetes manifests and restore data from the most recent good backup - Engineering
5. Test the new environment - Engineering
6. Test logging, security, and alerting functionality - Engineering
7. Assure systems are appropriately patched and up to date - Engineering
8. Deploy environment to production and update DNS if needed - Engineering

## 3. Reconstitution Phase

This section discusses activities necessary for restoring BloomAPI operations at the original or a new location. The goal is to restore full operations within the 24-hour RTO. When the original region has been restored, BloomAPI operations may be transitioned back.

1. Original or New Region Restoration
	* Recreate the environment from Terraform and Kubernetes manifests. - Engineering
	* Test the environment. - Engineering
	* Test logging, security, and alerting functionality. - Engineering
	* Deploy environment to production. - Engineering
	* Assure systems are appropriately patched and up to date. - Engineering
	* Update DNS to the restored environment if needed. - Engineering

2. Plan Deactivation

When operations are back to normal, the Recovery Lead deactivates the plan, records what happened and how long recovery took, and removes temporary resources created during recovery. Any data copies made during recovery are handled according to the BloomAPI Disposable Media Policy and Data Retention Policy.
