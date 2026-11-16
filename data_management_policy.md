# Data Management Policy

BloomAPI has procedures to create and maintain retrievable exact copies of stored electronic protected health information (ePHI). The policy and procedures will assure that complete, accurate, retrievable, and tested backups are available for all systems used by BloomAPI.

Data backup is an important part of the day-to-day operations of BloomAPI. To protect the confidentiality, integrity, and availability of ePHI, both for BloomAPI and BloomAPI Customers, complete backups are done daily to assure that data remains available when it needed and in case of disaster.

Violation of this policy and its procedures by workforce members may result in corrective disciplinary action, up to and including termination of employment.

## Applicable Standards from the HITRUST Common Security Framework

* 01.v - Information Access Restriction

## Applicable Standards from the HIPAA Security Rule

* 164.308(a)(7)(ii)(A) - Data Backup Plan
* 164.310(d)(2)(iii) - Accountability
* 164.310(d)(2)(iv) - Data Backup and Storage

## Backup Policy and Procedures

1. Perform daily snapshot backups of all systems that process, store, or transmit ePHI for BloomAPI Customers.
2. The Security Officer is in charge of backups. Backups are automated through Google Cloud; Tyler Brown (Security Officer) and Parsa Khazaeepoul (Engineering) are responsible for monitoring them and performing restores.
3. Workforce members who manage backups are trained on the backup and restore procedures.
4. Document backups 
	* Name of the system
	* Date & time of backup
	* Where backup stored (or to whom it was provided)
5. Cloud Spanner backups are retained for 30 days.
6. Securely encrypt stored backups in a manner that protects them from loss or environmental damage.
7. Protect backup encryption keys separately from encrypted backup data and limit key access to authorized workforce members.
8. Maintain backup protections that are resilient to accidental deletion, malicious alteration, ransomware, and compromise of a single production account where feasible.
9. Test backups at least annually and after material backup architecture changes, and document that files have been completely and accurately restored from the backup media.
10. Document recovery point objectives and recovery time objectives for critical systems and review them at least annually. The current objectives are an RTO of 24 hours and an RPO of 24 hours (see the [Disaster Recovery Policy](disaster_recovery_policy.md)).
