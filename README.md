# SOC Simulated Attack and Incident Detection Lab
<p align="center">

![Screenshot 2024-10-13 171608](https://github.com/user-attachments/assets/9ddf83c0-9adc-4b7b-83c8-b76e9e3d0a4a)

</p>

In this lab, I simulated various cyber attack scenarios and monitored the resulting logs and incidents in Azure Sentinel. These simulations included an Azure AD brute force attack, an MSSQL brute force attempt, a malware outbreak using the EICAR file, and a privilege escalation event involving Key Vault secret retrieval. Additionally, I triggered firewall tampering and excessive password reset attempts. Each incident was carefully observed and analyzed to understand how Sentinel detects and alerts on these security threats, showcasing my ability to respond to real-world attack scenarios in a SOC environment.




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell
- Microsoft Sentinel
- Kusto Query language (KQL)
- Log Analytics Workspaces

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1 - Trigger AAD Brute Force Success
- Step 2 - Trigger MSSQL Brute Force Attempt 
- Step 3 - Trigger Malware Outbreak
- Step 4 - Trigger Possible Privilege Escalation (AKV Critical Credential Retrieval or Update)
- Step 5 - Trigger Windows Host Firewall Tampering
- Step 6 - Trigger Excessive Password Resets



<h2>Deployment and Configuration Steps</h2>

<h2>Trigger AAD Brute Force Success</h2>  

- (from within attack-vm) Simulate brute force success against Azure AD with your attacker account:
- In an incognito windows, open portal.azure.com and fail 10-11 logins in a row, followed by a successful login
- Here I generated 10 failed login attempts to trigger an alert in the SIEM

![Screenshot 2024-10-14 172139](https://github.com/user-attachments/assets/2bc82abc-33ba-49cf-a9b9-e84198284555)
- Here is the incident being triggered in our SIEM
![Screenshot 2024-10-14 180321](https://github.com/user-attachments/assets/331d5934-66eb-4a09-a533-a32c370aef88)




<h2>Trigger MSSQL Brute Force Attempt </h2> 

- (from within attack-vm) Open SSMS and simulate brute force attempt against your SQL Server by attempting to log into it 10-11 times
-  Here I generated 10 failed login attempts to trigger an alert in the SIEM

![Screenshot 2024-10-14 173334](https://github.com/user-attachments/assets/81936f24-7461-492e-ad6c-3ac0505f14f8)
![Screenshot 2024-10-14 173713](https://github.com/user-attachments/assets/1c30ccd8-2ba3-44c7-a13f-ac49cf28009a)
- Here is the incident being triggered in the SIEM
![Screenshot 2024-10-14 180505](https://github.com/user-attachments/assets/3ddee8a4-0da1-4e81-ab33-c28a9bc5e40f)


<h2>Trigger Malware Outbreak </h2>

- (from within windows-vm) Generate a Malware alert by using an EICAR file
- Malware-Generator-EICAR.ps1 (Do from within Windows VM)
- I will use the Powershell script to trigger a fake virus which will spin an incident in the SIEM

![Screenshot 2024-10-14 175014](https://github.com/user-attachments/assets/0c255ad7-38e4-4fd7-ba5b-d81df15ccd1f)
- Here the script is being ran 15 times which will trigger the alert
![Screenshot 2024-10-14 175308](https://github.com/user-attachments/assets/df6b8904-6d37-4194-9617-6dc3072b4cc5)
The query to use to detect this attack in the logs.
![Screenshot 2024-10-14 175812](https://github.com/user-attachments/assets/1bc96699-784d-4e8e-aa22-031baafd9e9c)
- Here is the incident being created in our SIEM
![Screenshot 2024-10-14 181754](https://github.com/user-attachments/assets/9fe0e543-7505-40fd-ae6c-4c6cb6a0e023)



<h2>Trigger Possible Privilege Escalation (AKV Critical Credential Retrieval or Update) </h2>

- Manually Read Key Vault Secret “Tenant-Global-Admin-Password” in the portal and observe the incidents
- Here in the key, I will look at the secret value which will trigger an incident in the SIEM

![Screenshot 2024-10-14 181026](https://github.com/user-attachments/assets/9c0a4397-be0f-426f-9e0d-a4075af78c4f)
- here is the query to search for this incident in the logs.
![Screenshot 2024-10-14 181612](https://github.com/user-attachments/assets/ecaa9f64-378f-4c96-a172-6a88f7d5bc57)
- Here is the incident generated in the SIEM for this attack
![Screenshot 2024-10-14 184242](https://github.com/user-attachments/assets/52aa7c26-1992-44bb-ad06-90cf0f6dbbfa)


<h2>Trigger Windows Host Firewall Tampering </h2>

- Manually Enable and Disable the windows-vm Firewall and observe the incidents
- Turning a firewall on and off will trigger an Incident.

![Screenshot 2024-10-14 182350](https://github.com/user-attachments/assets/c95911a3-150f-4c0e-89f0-370f5ff5d326)
![Screenshot 2024-10-14 182500](https://github.com/user-attachments/assets/f8ebfccd-70d6-4c53-9b4f-202bd0a8916f)
- Here is the query that will generate the alert in the logs which will be sent to the SIEM.
![Screenshot 2024-10-14 182722](https://github.com/user-attachments/assets/db755087-a6db-4158-ade3-326ae971b324)
- Here is the incident triggered in the SIEM for this attack
![Screenshot 2024-10-14 184523](https://github.com/user-attachments/assets/43a91643-964b-4c0a-9705-70940cb4263b)



<h2>Trigger Excessive Password Resets</h2> 

- Manually Trigger excessive password resets (KQL-Cheat-Sheet.md) and observe the incidents by resetting a users’ password in the portal 10-11 times
 
![Screenshot 2024-10-14 183800](https://github.com/user-attachments/assets/1a809175-d382-4aae-882f-9279085b46a9)
![Screenshot 2024-10-14 183816](https://github.com/user-attachments/assets/681f9971-5284-456b-981c-764b45427fab)
- Here is the incident being created in the SIEM for this attack
![Screenshot 2024-10-14 185229](https://github.com/user-attachments/assets/10c3af59-3377-4d30-aeb9-650deb0b11ca)























