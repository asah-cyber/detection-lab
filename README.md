🚀 Automated Detection Engineering Lab (One-Click)
==================================================

This repository provides a fully automated, Infrastructure-as-Code (IaC) environment for detection engineering and threat hunting. With a single command, you can deploy a mini-corporate network featuring a **Splunk Enterprise** SIEM and a **Windows Active Directory** environment.

---

## 🏗️ Lab Architecture

| Component | Operating System | Role | IP Address |
| :--- | :--- | :--- | :--- |
| **The Brain** | Ubuntu 22.04 | Splunk Enterprise (Indexer/Search Head) | `192.168.56.10` |
| **The DC** | Windows Server 2022 | Domain Controller (`lab.local`) | `192.168.56.20` |
| **The Target** | Windows 10 | Domain-Joined Workstation | `192.168.56.30` |

### **Telemetry Flow**
* **Log Transport:** Splunk Universal Forwarders (UF) installed on all Windows nodes.
* **Inbound Port:** TCP `9997` (Splunk Receiving).
* **Log Sources:** Windows Security, System, and Application event logs.
    

🛠️ Prerequisites
-----------------

Before running the deployment, ensure your host machine (Windows Laptop) has:

1.  **VMware Workstation Pro** installed.
    
2.  **Internet Access** (to download VM images and Splunk packages).
    
3.  **PowerShell** (Run as Administrator).
    

⚡ Deployment: The "One-Click" Way
---------------------------------

### 1\. Clone the Repository

PowerShell

`git clone https://github.com/asah-cyber/detection-lab.git`

`cd detection-lab-auto `

### 2\. Run the Deployer

Right-click Deploy-Lab.ps1 and select **Run with PowerShell**, or execute:

PowerShell

`.\Deploy-Lab.ps1   `

_The script will automatically check for Vagrant, install necessary VMware plugins, and provision all three VMs. Sit back and grab a coffee—it takes about 15–20 minutes._

🕵️ Usage & Validation
----------------------

Once the script finishes, you can access your lab:

*   **Splunk Web UI:** http://192.168.56.10:8000 (User: admin / Pass: Password123!)
    
*   **Search for Logs:** Run the following query in Splunk to verify data is flowing:index="wineventlog" | stats count by host
    

🧹 Cleanup
----------

To save disk space and RAM when you are finished with your research, run the destruction script:

PowerShell

`.\Destroy-Lab.ps1   `

_This will completely remove the VMs from your system._

📝 Important Notes
------------------

*   **Developer License:** This lab installs Splunk with a trial license. To extend this, follow the instructions in the post to upload your **Splunk Developer License**.
    
*   **Resources:** This lab requires approximately **16GB of RAM** and **80GB of Disk Space**.

## Contributions
Found a bug or want to add Sysmon support? Feel free to submit a Pull Request!
