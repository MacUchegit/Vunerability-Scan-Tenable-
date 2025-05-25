<img width="1280" alt="image" src="https://github.com/user-attachments/assets/4993f34d-76cb-4634-ad58-538e58976334" />

---
# **Vulnerability Management Lab with Tenable**

---

## 🔍 **What is a Vulnerability?**

A **vulnerability** is a flaw or weakness in a system’s design, implementation, or configuration that could be exploited by a threat actor to compromise the system's integrity, availability, or confidentiality.

### ✅ **Key Points to Know:**

* Vulnerabilities can exist in hardware, software, or processes.
* They are exploited through malware, phishing, outdated software, and misconfigurations.
* Common vulnerability types: buffer overflow, code injection, misconfiguration, and outdated software.

---

## **Why is Vulnerability Assessment Important?**

Vulnerability assessment plays a **critical role in proactive cybersecurity defense**. It allows organizations to:

* **Identify** weaknesses before attackers do.
* **Prioritize** remediation based on risk severity.
* **Ensure** compliance with industry standards (e.g., DISA/STIG, CIS).
* **Protect** sensitive assets and reduce potential damage from breaches.

---

## 🎯 **Project Objective**

To simulate a real-world vulnerability management process by:

* Setting up a virtual environment.
* Scanning and identifying vulnerabilities.
* Intentionally introducing a vulnerability.
* Remediating the threat.
* Visualizing results to track the lifecycle of vulnerability management.

---

## **Key Concepts Covered**

* **Introduction to Vulnerability Management**

  * Understanding what software vulnerabilities are.
  * How vulnerability scanners (e.g., Nessus) work.
  * The remediation process and risk reduction strategies.

---

## **Tools Used**

* **Microsoft Azure** – To create and host the virtual environment.
* **Tenable Nessus Essential** – For vulnerability scanning and reporting.

---

## **Hands-On Steps Summary**

* Create a Windows 10 VM in Azure.
* Install and configure Nessus Essential.
* Run initial scans to establish a baseline.
* Intentionally install vulnerable software (Firefox 3.6.12).
* Run subsequent scans to observe increased vulnerabilities.
* Remove the vulnerable software and enable Windows updates.
* Perform a final scan and compare results.
* Visualize data using Excel.

---

## **Step-by-Step Implementation**

---

### 🔹 **1. Create the Azure Virtual Machine**

* Create a Resource Group: `Vulnerability-Lab1`
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/e6cc5cdd-bf52-4cd7-92cc-45b8db08f542" />
  
**Create a Virtual Machie**

* VM Name: `Vunerable-Machine`
* Region: `US East 2`
* Image: `Windows 10 Pro N, version 22H2`
* Size: `Standard D2als_v6 `
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/c658fa4c-2857-4f7a-a7f3-c7ceddc005af" />
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/6928fcda-0152-47d0-81e4-18f65d29adc6" />
* Set Administrator credentials.
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/096c621c-067c-4d1e-a5d0-d8b1bd5aa67a" />
 
**Other Tabs:**

* Disks: `Standard HDD`
* Networking: Enable NIC and Public IP deletion on VM removal.
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/ecb2235f-2b47-481e-b411-b49eadcf69b3" />
* Monitoring: Disable boot diagnostics.
* Click `Review + Create`, then launch the VM.
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/8961b6f4-ebee-427c-aaa6-18e05e0b4ce5" />
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/2b836f16-a2bf-4332-ac56-09d9869a86d3" />

---

### 🔹 **2. Configure Windows 10 Environment** 

* **Connect via Remote Desktop.**
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/dbcaf3f3-ce36-4a8e-89ae-04ddb6772080" />
* **Install Nessus Professional** on the VM.
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/2c40df15-947e-4d9b-843e-7c1a79eed01c" />
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/089b1b88-135f-4ebd-bf6d-bfe2106e7397" />
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/2bc1492d-4cea-4854-9523-3535d58ee97d" />
  * Go ahead select "Register for Nessus Essentials" (It is Free!)
  * Input your work email address (a non-gmail address) and the activation Key that appears. Then wait for initialization.  
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/e5987c6e-c6fa-456b-bd89-9f834445dd12" />
* **Configure Windows Defender Firewall**:

  * Go to `wf.msc`.
  * Modify Domain, Private, and Public profile settings.
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/d8021e03-478e-41bb-8de7-cd2c180142f3" />
* **Set up PowerShell**:
  * Copy and paste the command below in Windows Powershell (Open the Windows Powershell CLI to do this)


  ```powershell
  Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" -Name "LocalAccountTokenFilterPolicy" -Value 1 -Type DWord -Force
  ```
* **Restart the VM** to apply changes.

---

### 🔹 **3. Run Initial Vulnerability Scan (Scan 1)**

* Open Nessus → Policies → **Scan Templates** → **Basic Network Scan** 

* Configure:

  * Name: `Windows 10 Scan`
  * Target: VM Private IP (e.g., 10.1.0.4)
  
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/6f92118b-6655-4a36-a57c-d27ab99b2e77" />
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/8f013106-ab32-4190-91ec-d1f002412e48" />
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/e2b445fd-18a0-41ee-b3ed-4be594ab5680" />
  
* Enable required services (Remote Registry, Admin Shares, Server).
  * These services are essential for a successful credentialed scan, as they allow the scanner to remotely access system configurations, registry data, and shared resources—enabling deeper and more accurate vulnerability detection.
  
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/83bc7ac3-df47-4ffc-9cdb-6a02ffe28553" />
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/dbb4166b-e53d-4e97-9bf2-230a7f4c642a" />
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/f1349dd3-2fdc-4e02-82a3-3c7b241268a8" />
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/8662327c-9118-4034-a906-4b1e98ec3e13" />
* **Run the scan** and note the result:

  <img width="931" alt="image" src="https://github.com/user-attachments/assets/af893d7e-9f02-4181-aec6-4014d89f55b1" />
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/a1178266-4e65-43ed-9774-50b81847444f" />
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/b8d3fe95-f8d3-4c6f-bd67-0677c26864fd" />
  
```yaml 
Scan 1 Result:  
Critical: 0 | High: 3 | Medium: 7 | Low: 1
```
* **Next, we perform a credentialed scan** by adding the Windows admin credentials under the **Credentials** tab. This allows Nessus to authenticate and access deeper system-level information that is not visible in a basic (unauthenticated) scan.

* **Credentialed scans provide a more accurate and comprehensive assessment** by identifying vulnerabilities that require local access—such as missing patches, weak configurations, and outdated software. Be sure to compare the results with the initial scan to see the expanded visibility.
  
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/c0d51ac7-b749-4ac6-9c72-28b56dfbf01b" />

  * Result

  <img width="931" alt="image" src="https://github.com/user-attachments/assets/3d115a35-40ec-46d9-b855-858253a04a0f" />
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/7e8f3837-3f1b-4ea2-b3d0-0303bed6e73f" />

```yaml 
Scan 2 Result:  
Critical: 2 | High: 7 | Medium: 7 | Low: 0
```
---

### 🔹 **4. Introduce Vulnerability (Make VM Vulnerable)**

* Installed deprecated software:
  **Firefox Setup 3.6.12.exe**
  (Known to contain multiple security vulnerabilities)

  <img width="931" alt="image" src="https://github.com/user-attachments/assets/4089ab60-6e84-41b5-940c-1cfc3ff10a6d" />
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/c9b6ab56-c24d-4fe5-adad-28651446b26f" />

---

### 🔹 **5. Run third Vulnerability Scan (Scan 3)** 
* Re-run the configured scan.
  
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/cc1daf26-4b32-4507-a53a-0ba0d18e10ea" />
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/dca4e7f4-3358-4174-af61-3dbd6173cb59" />
 
```yaml
Scan 3 Result:  
Critical: 94 | High: 90 | Medium: 25 | Low: 1
```

> Significant spike in vulnerabilities due to deprecated Firefox. 

---

### 🔹 **6. Remediate Vulnerabilities**

* **Uninstall** Firefox version 3.6.12.
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/592dbdad-69cd-4689-b175-be48ea2e5800" />
* **Enable** Windows Update and install all available patches.
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/5f18a897-c8d1-4697-a4e0-3c3c8ae58906" />
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/05100607-2cf4-452c-998a-b14fad395932" />
---

### 🔹 **7. Run Final Vulnerability Scan (Scan 4)**

* Re-scan the VM after remediation steps.
  
  <img width="931" alt="image" src="https://github.com/user-attachments/assets/00f8ad93-10cb-43d6-8797-4882b8e1d06c" />

```yaml
Scan 4 Results:  
Critical: 0 | High: 1 | Medium: 5 | Low: 0
```

> Huge improvement in system health.

---

### 📊 **8. Visualize Vulnerability Lifecycle**

*  Used a formatted Excel document to input scan results and generate visual charts.

  <img width="931" alt="image" src="https://github.com/user-attachments/assets/ebd8048a-bf35-42b1-a9f5-fa4d6521ca97" />

**Analysis:** 

* **Scan 1 and 2**: Initial baseline – minimal vulnerabilities.
* **Scan 3**: Huge spike from deprecated Firefox.
* **Scan 4**: Dramatic drop after remediation and updates.

---

## ✅ **Conclusion**

This lab successfully demonstrated a practical vulnerability management cycle:

* We created a secure test environment.
* Scanned and identified existing vulnerabilities.
* Simulated a real-world threat by introducing deprecated software.
* Applied remediation strategies to restore system health.
* Visualized the results for clear insight.

Through this hands-on project, I gained essential experience in:

* Using Tenable Nessus for vulnerability scans.
* Understanding how poor software hygiene leads to risks.
* Implementing remediation practices.
* Analyzing and visualizing vulnerability data for effective reporting.

