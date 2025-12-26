# Microsoft 365 Lab - Step 1: Tenant and User Setup

This lab documents the setup of a Microsoft 365 environment for hands-on learning. The goal is to create a clean tenant, configure users, teams, SharePoint sites, and prepare folder structures to simulate collaboration, permissions, and IT administration workflows.

---

## Lab Tenant Setup

- **Tenant Domain:** [Melvin79m.onmicrosoft.com](http://melvin79m.onmicrosoft.com/)  
- **Global Admin Account:** [MelvinWilliams@Melvin79m.onmicrosoft.com](mailto:MelvinWilliams@Melvin79m.onmicrosoft.com)  
- **Subscription:** Microsoft 365 Business Premium Trial (1 month, 10 users)  

---

## Users Created

| Display Name | Username | License |
| --- | --- | --- |
| Alice Smith | [AliceS@Melvin79m.onmicrosoft.com](mailto:AliceS@Melvin79m.onmicrosoft.com) | Microsoft 365 Business Premium |
| Bob Johnson | [BobJ@Melvin79m.onmicrosoft.com](mailto:BobJ@Melvin79m.onmicrosoft.com) | Microsoft 365 Business Premium |
| Carol Davis | [CarolD@Melvin79m.onmicrosoft.com](mailto:CarolD@Melvin79m.onmicrosoft.com) | Microsoft 365 Business Premium |
| David Martinez | [DavidM@Melvin79m.onmicrosoft.com](mailto:DavidM@Melvin79m.onmicrosoft.com) | Microsoft 365 Business Premium |
| Emma Wilson | [EmmaW@Melvin79m.onmicrosoft.com](mailto:EmmaW@Melvin79m.onmicrosoft.com) | Microsoft 365 Business Premium |
| Frank Brown | [FrankB@Melvin79m.onmicrosoft.com](mailto:FrankB@Melvin79m.onmicrosoft.com) | Microsoft 365 Business Premium |
| Grace Lee | [GraceL@Melvin79m.onmicrosoft.com](mailto:GraceL@Melvin79m.onmicrosoft.com) | Microsoft 365 Business Premium |
| Henry Clark | [HenryC@Melvin79m.onmicrosoft.com](mailto:HenryC@Melvin79m.onmicrosoft.com) | Microsoft 365 Business Premium |
| Irene Lewis | [IreneL@Melvin79m.onmicrosoft.com](mailto:IreneL@Melvin79m.onmicrosoft.com) | Microsoft 365 Business Premium |
| Jack Walker | [JackW@Melvin79m.onmicrosoft.com](mailto:JackW@Melvin79m.onmicrosoft.com) | Microsoft 365 Business Premium |
| Melvin Williams | [MelvinWilliams@Melvin79m.onmicrosoft.com](mailto:MelvinWilliams@Melvin79m.onmicrosoft.com) | Microsoft 365 Business Premium |

**Note:** All users had passwords set and are required to change them at first login.

---

## Teams Setup

Three Teams were created corresponding to departments:

| Team Name | Members | Channels |
| --- | --- | --- |
| IT Department | 6 | Announcements, Projects, Support Tickets, Training, General |
| Sales Department | 4 | General, Opportunities, Sales Reports, Training, Announcements |
| HR Department | 9 | General, Policies & Procedures, Recruitment, Employee Onboarding, Announcements |

---

## SharePoint Sites Setup

Each department has a dedicated SharePoint Team site linked to their Teams group:

| Site Name | Linked Team | Privacy |
| --- | --- | --- |
| IT Department Site | IT Department | Private |
| Sales Department Site | Sales Department | Private |
| HR Department Site | HR Department | Private |

**Template Used:** Standard team template from Microsoft to provide default document libraries and pages.

---

## SharePoint Folder Structure & Permissions

Folders were created in each department site to simulate real-world document organization. Permissions were customized to demonstrate **least privilege** and secure collaboration.

### IT Department Site

| Folder | Description | Permissions | Notes |
| --- | --- | --- | --- |
| Projects | Contains IT projects with subfolders: Network_Upgrade, Onboarding_Automation, Security_Audit | Inherited from library: Owners=Full Control, Members=Edit | Placeholder files added to each subfolder. Screenshots captured. |
| Policies | Contains company policies | Custom: Owners=Full Control, Members=Edit | Non-IT read access documented as intent. Inheritance broken. |
| Support Tickets | IT service tickets | Custom: Owners=Full Control, Members=Edit | Restricted to IT only. Demonstrates sensitive data handling. |
| Training | IT training materials | Custom: Owners=Full Control, Members=Edit | Non-IT read access documented as intent. Inheritance broken. |

> **Note:** Due to Microsoft 365 trial tenant limitations, non-IT users could not be added to read-only groups. In a production environment, these groups would exist to enforce least privilege.

---

### Projects Subfolders Example

| Subfolder | Placeholder Files | Permissions |
| --- | --- | --- |
| Network_Upgrade | `README.md`, `Network_Upgrade_Plan.docx` | Inherited from library |
| Onboarding_Automation | `README.md`, `Automation_Script.docx` | Inherited from library |
| Security_Audit | `README.md`, `Audit_Report.xlsx` | Inherited from library |

---

## Documentation & Screenshots

For each folder and subfolder:

1. Screenshot **folder structure**  
2. Screenshot **Advanced Permissions table** showing Owners & Members  
3. Optional: Screenshot **Check Permissions** for sample IT user  

These screenshots are organized under `/Screenshots` in the GitHub repo.

---

## Outcome

At the completion of Step 1:

- A clean Microsoft 365 tenant with fully configured users  
- Teams with department-based channels  
- SharePoint sites linked to Teams  
- Document library folders with permissions demonstrating least privilege and secure collaboration  
- Placeholder files in Projects subfolders for tangible evidence  

This lab provides a **foundation for demonstrating Microsoft 365 administration, file sharing, and collaboration workflows** in a professional GitHub repository.

---


