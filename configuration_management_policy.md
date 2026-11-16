# Configuration Management Policy

BloomAPI standardizes and automates configuration management by defining infrastructure and application configuration as code, kept in version control. Infrastructure is defined in Terraform and application workloads in Kubernetes manifests. Every change to production systems and networks is made through a reviewed pull request, which also serves as the record of the change. The same definitions are used to recreate the environment as part of the Disaster Recovery plan and process.

## Applicable Standards from the HITRUST Common Security Framework

* 06 - Configuration Management

## Applicable Standards from the HIPAA Security Rule

* 164.310(a)(2)(iii) Access Control & Validation Procedures

## Configuration Management

1. Terraform and Kubernetes manifests, kept in BloomAPI's GitHub repositories, are used to standardize and automate configuration management.
2. No systems are deployed into BloomAPI production environments except through a reviewed change to those definitions or an approved deployment process.
3. All changes to production systems, network configuration, and firewall or Cloud Armor rules are made through GitHub pull requests that are reviewed before they are merged. Automated continuous integration (CI) checks, such as builds, tests, linting, and security checks, run on pull requests before changes are deployed.
4. An up-to-date inventory of technology assets is maintained, including systems, applications, databases, network components, cloud resources, service accounts, and third-party services that create, receive, maintain, or transmit ePHI. All systems are categorized as production and utility to differentiate based on criticality. See Asset Inventory below.
5. BloomAPI maintains a network map or data flow diagram showing where ePHI enters, is processed, is stored, is transmitted, and leaves the BloomAPI environment. The inventory and network map are reviewed at least annually and after material changes.
6. Clocks are synchronized across all systems using NTP. Modifying time data on systems is restricted.
7. All front end functionality (developer dashboards and portals) is separated from backend (database and app servers) systems by being deployed as separate services.
8. Production systems are segmented from development, staging, corporate, and public networks. Access between segments is restricted to approved ports, protocols, services, and identities.
9. Software changes are tested before they are deployed to production, using automated tests and, where appropriate, manual verification.
10. All committed code is reviewed using pull requests in GitHub to assure software code quality and proactively detect potential security issues in development.
11. BloomAPI uses development and staging environments to test changes before production. Staging is not a full mirror of production; differences between staging and production are considered when a change is evaluated.
12. All formal change requests require unique ID and authentication.
13. Material changes affecting systems that create, receive, maintain, or transmit ePHI require evaluation of security impact, logging impact, backup impact, and any update needed to the asset inventory or network map.

## Asset Inventory

* **Cloud infrastructure.** The Terraform definitions, together with the Kubernetes manifests, are the inventory of BloomAPI's cloud infrastructure: projects, clusters, databases, storage buckets, networks, firewall and Cloud Armor rules, and service accounts. Resources that are not yet managed in Terraform are recorded in the inventory until they are brought under Terraform.
* **Workstations.** BloomAPI keeps a list of company-issued laptops, including the assigned workforce member, the device, and confirmation that full-disk encryption is on.
* **SaaS and third-party services.** BloomAPI keeps a list of SaaS tools and third-party services in use, including what data each one receives. Services that may receive PHI are also listed in [Subprocessors](subprocessors.md) and governed by the [3rd Party Policy](3rd_party_policy.md).
* The workstation and SaaS lists are reviewed at least annually, and when a workforce member joins or leaves or a service is added or removed.
