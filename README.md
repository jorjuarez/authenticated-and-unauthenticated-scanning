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

* **System Preparation for Authentication:** To ensure the scanner could successfully log in, specific configurations were enabled on the target systems prior to the authenticated scans.

    * **On Windows**, remote administrative UAC restrictions were disabled using the following PowerShell command:
        ```powershell
        Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" -Name "LocalAccountTokenFilterPolicy" -Value 1 -Type DWord -Force
        ```

    * **On Linux**, the root user was enabled for SSH login for the scan using these BASH commands:
        ```bash
        # Set a password for the root user
        sudo passwd root

        # Permit root login via SSH and restart the SSH service
        sudo sed -i 's/^PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config
        sudo systemctl restart sshd
  
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

---

#### Windows Scans
*Side-by-side Scan Comparison - Left Unauthenticated | Right Authenticated*
![Windows Scan Comparison](https://github.com/user-attachments/assets/06af40ed-4ccb-47a3-bada-2c2d450aa0b0)
*View the full reports: [Unauthenticated Scan Report](https://drive.google.com/file/d/1NLzpGQK0H7FJZQLtWCoNuWQJFUWpQUEj/view?usp=sharing) | [Authenticated Scan Report](https://drive.google.com/file/d/1GyB9r4LvCUBFlevMH9nsPWb3DgXb6IVt/view?usp=sharing)*

---

#### Linux Scans
*Side-by-side Scan Comparison - Left Unauthenticated | Right Authenticated*
![Linux Scan Comparison](https://github.com/user-attachments/assets/6f51d3cb-458d-4e89-bc88-5fd78d192a0c)
*View the full reports: [Unauthenticated Scan Report](https://drive.google.com/file/d/16T7GnWTkRMlNvM2DEQT-VIrzYOE3wP4w/view?usp=sharing) | [Authenticated Scan Report](https://drive.google.com/file/d/1T8OJixQrp7bT34uAIII9PuwVZk1RMi2o/view?usp=sharing)*

---
### Conclusion

The conclusion is simple: you can't protect what you can't see.

An unauthenticated scan is like walking around a house to check for open doors (open ports). In contrast, an authenticated scan is like having the keys to go inside, where you can find the real dangers, like a stove left on (an exploitable service) or a recalled smoke detector (outdated software).

Relying on the outside view alone is a security risk. To make smart decisions, you need the full story that only credentialed scanning provides.
