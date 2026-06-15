# Configuration Management Policy

BloomAPI standardizes and automates configuration management through the use of Ansible scripts as well as documentation of all changes to production systems and networks. Ansible automatically configures all BloomAPI systems according to established and tested policies, and is used as part of our Disaster Recovery plan and process.

## Applicable Standards from the HITRUST Common Security Framework

* 06 - Configuration Management

## Applicable Standards from the HIPAA Security Rule

* 164.310(a)(2)(iii) Access Control & Validation Procedures

## Configuration Management

1. Ansible is used to standardize and automate configuration management.
2. No systems are deployed into BloomAPI environments without approval of the BloomAPI CTO.
3. All changes to production systems, network devices, and firewalls are approved by the BloomAPI CTO before they are implemented. Additionally, all changes are tested before they are implemented in production.
4. An up-to-date inventory of technology assets is maintained, including systems, applications, databases, network components, cloud resources, service accounts, and third-party services that create, receive, maintain, or transmit ePHI. All systems are categorized as production and utility to differentiate based on criticality.
5. BloomAPI maintains a network map or data flow diagram showing where ePHI enters, is processed, is stored, is transmitted, and leaves the BloomAPI environment. The inventory and network map are reviewed at least annually and after material changes.
6. Clocks are synchronized across all systems using NTP. Modifying time data on systems is restricted.
7. All front end functionality (developer dashboards and portals) is separated from backend (database and app servers) systems by being deployed on separate servers.
8. Production systems are segmented from development, staging, corporate, and public networks. Access between segments is restricted to approved ports, protocols, services, and identities.
9. All software and systems are tested using end-to-end tests.
10. All committed code is reviewed using pull requests GitHub to assure software code quality and proactively detect potential security issues in development.
11. BloomAPI utilizes development and staging environments that mirror production to assure proper function.
12. All formal change requests require unique ID and authentication.
13. Material changes affecting systems that create, receive, maintain, or transmit ePHI require evaluation of security impact, logging impact, backup impact, and any update needed to the asset inventory or network map.
