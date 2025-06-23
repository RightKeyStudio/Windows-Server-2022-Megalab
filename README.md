# 🧠 Windows Server 2022 Megalab Project

Simulated a full enterprise environment with Active Directory, user/group provisioning, NTFS permissions, Group Policy, and PowerShell-based log analysis tools. This project showcases practical cybersecurity and systems administration skills.

## ✅ Key Skills Demonstrated

-   **Active Directory Management:** User and group provisioning, Organizational Unit (OU) design.
-   **NTFS Permission Control:** Implementing granular folder access permissions.
-   **Group Policy Objects (GPO):** Configuring and enforcing security policies (e.g., UI lockdowns, drive mapping).
-   **PowerShell Scripting:** Advanced log parsing, data extraction, and CSV export.
-   **Security Information & Event Management (SIEM) Lite:** Real-time login failure monitoring (Event ID 4625) and threat IP extraction using PowerShell.

---

## 👨‍💻 Phase 1: Active Directory Design & Management

Designed and implemented a logical Active Directory structure for `ajx.local`, including custom Organizational Units (OUs) for department-specific user and group management. User accounts were provisioned across these OUs, and security groups were created (e.g., `AJX_Staff`, `Finance_Staff`) to facilitate streamlined access control and policy application.

![AD Organizational Unit Structure](Screenshots/aduc_ous_and_groups.png.png)
*Visual representation of the custom OU structure within Active Directory Users and Computers.*

![User Account Membership](Screenshots/aduc_user_member_of_group.png)
*Demonstrates a user account's membership in relevant security groups, crucial for permissions and GPO targeting.*

---

## 📂 Phase 2: File System Security & Group Policy Enforcement

Configured robust file system security using NTFS permissions and enforced security best practices across the domain through Group Policy Objects (GPOs).

### NTFS Permissions

Granular NTFS permissions were applied to shared network drives, ensuring that only authorized security groups (e.g., `AJX_Staff`) had appropriate access levels (e.g., Modify) to sensitive data.

![NTFS Folder Permissions](Screenshots/ntfs .jpg)
*Screenshot of the NTFS security tab, showing explicit permissions granted to a custom security group on a shared folder.*

### Group Policy Object (GPO) Lockdowns

Implemented restrictive GPOs to enhance endpoint security for standard users, preventing access to critical system tools.

![GPO Configured Lockdowns](Screenshots/lockdown gpo on drive z.png)
*Displays the configured GPO settings in the Group Policy Management Editor, including policies to disable Control Panel, Command Prompt, and Task Manager.*

![GPO Lockdown Effect](Screenshots/gpo_user_tskmgrblocked_lockdowgpi.jpg)
*Validation of GPO enforcement: A standard user's attempt to access Task Manager is blocked by policy.*

### GPO Drive Mapping

Automated network drive mapping for users based on their Active Directory group membership, providing consistent access to shared resources.

![GPO Drive Mapping Effect](Screenshots/Z Drive.png)
*File Explorer view from a standard user's session, confirming the successful automatic mapping of a network drive (Z:).*

---

## 🔐 Phase 3: PowerShell Log Analysis & SIEM Simulation

Developed PowerShell scripts to perform real-time security monitoring, focusing on failed login attempts (Event ID 4625), and to extract and export critical security event data.

### Real-time Login Monitoring Dashboard

A continuous PowerShell script simulates a Security Information and Event Management (SIEM) dashboard, providing a live, console-based view of failed login attempts, including timestamps, usernames, and source IP addresses.

![Live Failed Login Dashboard](Screenshots/failed login dashboard.jpg)
*Screenshot of the PowerShell console displaying the dynamic, real-time failed login event dashboard.*

### Log Parsing and Data Export

Utilized `Get-WinEvent` with advanced filtering and regex to efficiently parse Windows Security event logs for Event ID 4625 (failed logons). Extracted key details were then structured and exported to CSV files for audit, further analysis, and long-term storage.

![Raw Get-WinEvent Output](Screenshots/getwinvent filterhashtable.png)
*Demonstrates the raw output from a targeted `Get-WinEvent` query, highlighting the ability to filter and retrieve specific security events.*

![Exported Failed Logins CSV](Screenshots/failedips.jpg)
*Content of an exported CSV file, showing structured failed login data (TimeCreated, IPAddress), ready for auditing.*

All generated log data (CSV files) is stored in a dedicated, shared directory on the domain controller, accessible for centralized security analysis.

![Shared Logs Directory](Screenshots/csv.jpg)
*File Explorer view of the designated `C:\AJXShared\Logs` directory, confirming the presence of generated audit CSV files.*

---

## 🧩 What’s Next

-   **Azure Cloud VM Deployment:** Extend the environment to Azure for hybrid cloud management and integration.
-   **Task Scheduler Log Scans:** Implement scheduled PowerShell tasks for automated, periodic log analysis and reporting.
-   **Email Alerting:** Configure PowerShell scripts to send email notifications for critical security events, such as brute-force attempts.
-   **GPO-Based Account Lockouts:** Implement advanced GPO settings to automatically lock out user accounts after a defined number of failed login attempts, enhancing brute-force protection.

---
