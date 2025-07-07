# The Critical Value of Authenticated Scanning
This project shows how to use the right tool for the job by weighing two scan types: the on-demand, external view of unauthenticated (network-based) scans versus the deep, internal audit of authenticated (credentialed) scans.

---

_**Authenticated Scan:**_ A scan where the vulnerability scanner is given credentials (e.g., a username and password) to log in to the target system. This provides deep visibility by assessing the system from the "inside out," allowing it to check for missing patches, detailed software versions, and local misconfigurations.

_**Unauthenticated Scan:**_ A scan performed without credentials, assessing the target from the "outside in." This simulates the perspective of an external attacker and can only identify vulnerabilities on services exposed to the network, such as open ports and SSL/TLS configuration issues.

---

## Skills & Technologies Applied

* **Vulnerability Management**
    * **Tenable.io:** Configuring enterprise scans (authenticated & unauthenticated), reporting, and analysis.
    * **Risk Prioritization:** Triaging findings based on technical severity and business context.

* **Automation & Scripting**
    * **BASH:** Scripting for Linux environment configuration and remediation.

* **Cloud & Infrastructure**
    * **Microsoft Azure:** Provisioning and managing Windows & Linux VMs as scan targets.
    * **Network Security:** Understanding of network protocols (TLS, SMB) and cipher suites.

* **IT Governance & Process**
    * **Policy Development:** Drafting and finalizing an enterprise-wide security policy.
    * **Change Management:** Presenting technical changes and rollback plans to a Change Advisory Board (CAB).
    * **Stakeholder Communication:** Securing buy-in and planning remediation with IT operations teams.
