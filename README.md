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
    * **PowerShell:** Scripting automated remediation for system hardening and configuration changes.
    * **BASH:** Scripting for Linux environment configuration and remediation.

* **Cloud & Infrastructure**
    * **Microsoft Azure:** Provisioning and managing Windows & Linux VMs as scan targets.
    * **Network Security:** Understanding of network protocols (TLS, SMB) and cipher suites.

* **IT Governance & Process**
    * **Policy Development:** Drafting and finalizing an enterprise-wide security policy.
    * **Change Management:** Presenting technical changes and rollback plans to a Change Advisory Board (CAB).
    * **Stakeholder Communication:** Securing buy-in and planning remediation with IT operations teams.
---

### Methodology

To conduct this comparison, a controlled test environment was established using Microsoft Azure and Tenable.io. The process was as follows:

* **Environment:** All virtual machines were hosted in a single Azure resource group with standard network settings.

* **Scan Targets:**
    * One **Windows 10 Pro** virtual machine.
    * One **Ubuntu 22.04 LTS** virtual machine.

* **Scan Configuration:** Four distinct vulnerability scans were configured and executed from Tenable.io to gather comparative data:
    1.  An **unauthenticated** scan targeting the Windows 10 VM.
    2.  An **authenticated** scan targeting the Windows 10 VM (using local administrator credentials).
    3.  An **unauthenticated** scan targeting the Ubuntu VM.
    4.  An **authenticated** scan targeting the Ubuntu VM (using SSH key-based credentials).
  
---

### Results & Analysis

The difference in findings was immediate and significant. The authenticated scans provided far superior visibility into the true security posture of the systems, moving beyond surface-level network observations to detailed internal host configurations.

#### Data Summary

The table below quantifies the difference in vulnerability counts discovered by each scan type on both operating systems.

| Operating System | Scan Type | Critical | High | Medium | Low | Total Findings |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: |
| **Windows 10** | Unauthenticated | 0 | 0 | 6 | 1 | 36 |
| **Windows 10** | **Authenticated** | **0** | **2** | **9** | **1** | **146** |
| **Linux** | Unauthenticated | 0 | 0 | 0 | 1 | 21 |
| **Linux** | **Authenticated** | **0** | **0** | **0** | **1** | **57** |

#### Windows Analysis
The authenticated scan on the Windows 10 machine was crucial, discovering **2 High** and **9 Medium** severity vulnerabilities that were completely invisible to the unauthenticated scan. These included specific software flaws (e.g., in Microsoft Paint 3D, 7-Zip) and detailed patch information that can only be verified with system-level access.

#### Linux Analysis
Similarly, while no high-severity vulnerabilities were found on the Linux machine, the authenticated scan provided more than **double the visibility** (57 findings vs. 21). It successfully enumerated installed software packages and identified local security misconfigurations, such as user accounts with non-expiring passwords, which are essential for security hardening.

#### Visual Evidence

*View the full reports: [Authenticated Scan Report](https://drive.google.com/file/d/1GyB9r4LvCUBFlevMH9nsPWb3DgXb6IVt/view?usp=sharing) | [Unauthenticated Scan Report](https://drive.google.com/file/d/1NLzpGQK0H7FJZQLtWCoNuWQJFUWpQUEj/view?usp=sharing)*

*A side-by-side comparison of Windows scan results.*
![image](https://github.com/user-attachments/assets/47c3afaa-230a-470d-8976-cbe2b414b06c)


![Linux Scan Comparison](URL_to_your_Linux_comparison_image)
*A side-by-side comparison of Linux scan results.*
