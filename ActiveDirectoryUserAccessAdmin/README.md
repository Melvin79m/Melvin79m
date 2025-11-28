# Active Directory User & Access Administration Project

This project is the continuation of my MelTech.com Active Directory home lab, expanded into a full enterprise-style environment. The purpose is to gain hands-on experience with **users, groups, permissions, roles, OU structure, department layouts, floors/shifts, Group Policy Objects (GPOs), and real-world sysadmin workflows**.

Through this project, I will be:

- Organizing users and groups into structured OUs and departments  
- Implementing floors and shift-based divisions  
- Delegating administrative roles and permissions  
- Applying GPOs for security, workflow, and access control  
- Documenting every step with screenshots and notes for reproducibility  

> **Note:** This is an ongoing project and will continue to grow with each step.

---

## Step 1: Designing the Enterprise OU Structure

In this phase of the project, I expanded my existing MelTech.com Active Directory lab into a full enterprise-style identity and access management environment. Building on the domain, users, and foundational configuration completed earlier, I designed a complete organizational unit structure that mirrors how a real company organizes people, departments, and access boundaries. I created departmental OUs for **Admins, HelpDesk, Interns, SystemAdmin, Networking, Security, HR, Executives, and Sales**, then structured **four floor-level OUs** to reflect a physical building layout—**Floor 1 through Floor 4**. Each department was placed on its corresponding floor:

- Floor 1: Interns and HelpDesk  
- Floor 2: SystemAdmin and Networking  
- Floor 3: Security and HR  
- Floor 4: Executives and Sales  

To support realistic access control scenarios, I added **DayShift** and **NightShift** sub-OUs under every department, allowing future group policies, restrictions, and workflow rules to be applied based on shift schedules. This enterprise-style OU hierarchy forms the core framework for **permission modeling, delegated administration, user provisioning, and all upcoming identity and security exercises** in the project.

**Screenshots:**  
![Step 1-0](./screenshots/Lab/1.0.png)  
![Step 1-1](./screenshots/Lab/1.1.png)  
![Step 1-2](./screenshots/Lab/1.2.png)  

---

## Notes / Observations

- Active Directory OU planning and structure  
- Departmental divisions for realistic enterprise simulation  
- Floor and shift subdivisions for GPO and access modeling  
- Foundation for delegated administration, user management, and workflow testing
