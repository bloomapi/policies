# IDS Policy

In order to preserve the integrity of data that BloomAPI stores, processes, or transmits for Customers, BloomAPI implements strong intrusion detection tools and policies to proactively track and retroactively investigate unauthorized access. 

## Applicable Standards from the HITRUST Common Security Framework

*  09.ab - Monitoring System Use
*  06.e - Prevention of Misuse of Information
*  10.h - Control of Operational Software

## Applicable Standards from the HIPAA Security Rule

* 164.312(b) - Audit Controls

## Intrusion Detection Policy

* Public traffic to BloomText reaches its backends through Google Cloud load balancers protected by a Google Cloud Armor security policy. Cloud Armor is Google's web application firewall (WAF) service: its rules allow, deny, or throttle requests by attributes such as path, origin, and request rate before they reach BloomAPI services, and it logs HTTP and WAF traffic for review.
* Cloud Armor rate-limiting rules automatically throttle or temporarily ban sources that send excessive requests, including repeated login attempts. Cloud Armor also applies geographic restrictions to incoming traffic. Login traffic that crosses a defined threshold generates an alert to BloomAPI.
* Google Cloud's infrastructure provides network-level protection against denial of service attacks for traffic through its load balancers.
* GCP VPC firewall rules restrict network access to BloomAPI systems to approved sources, ports, and protocols. Access to the GKE cluster control plane is limited to authorized administrator networks.
* Cloud Armor rules and firewall rules are defined in Terraform. New rules and changes are made through reviewed pull requests and tested before they are relied on in production (see the [Configuration Management Policy](configuration_management_policy.md)). Cloud Armor and firewall rules are reviewed at least annually and after a security incident involving network traffic.
* Alerts and suspicious activity are investigated according to the [Incident Response Policy](incident_response_policy.md).
