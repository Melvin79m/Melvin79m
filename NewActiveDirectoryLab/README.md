# New Active Directory Lab Using Proxmox

## Phase 1: Core Infrastructure Foundation

### Phase 1: Step 1 – Static IP Configuration
I initiated the lab setup by transitioning the Windows Server 2022 instance from a dynamic to a static network configuration. By manually assigning an IPv4 address, subnet mask, and default gateway based on my local network's architecture, I ensured that the server maintains a permanent address that won't change after reboots. I configured the Preferred DNS to 127.0.0.1, pointing the server to itself in preparation for its role as a Domain Controller, and added 8.8.8.8 as an Alternate DNS to maintain internet access during the transition. This creates a stable foundation for the Active Directory services that will rely on this fixed identity.

**Screenshot:** `Lab.1`

### Phase 1: Step 2 – Naming the Server and Installing the AD Role
After establishing the network settings, I moved into the system configuration phase by renaming the server to MEL-DC-01. Standardizing the host name is a critical best practice before promotion to ensure the Active Directory database reflects a professional naming convention. Once the server rebooted to apply the new name, I utilized Server Manager to install the Active Directory Domain Services (AD DS) role. This process loaded the necessary binaries and management consoles onto the OS, officially preparing the machine to be promoted to the primary Domain Controller for the lab environment.

**Screenshot:** `Lab.2`

### Phase 1: Step 3 – Domain Promotion and Forest Creation
The final stage of the foundation involved promoting the server to a Domain Controller by initiating a new Active Directory forest. I designated the root domain as MELVINLAB.local and configured the Directory Services Restore Mode (DSRM) with a secure recovery password to ensure administrative access in the event of database corruption. During this process, the server automatically configured the DNS role and established the global catalog and schema partitions. Upon completion of the promotion and a final system reboot, I verified the success of the installation by logging in with domain administrator credentials. This successfully establishes MEL-DC-01 as the central identity and authentication authority for the entire lab environment.

**Screenshot:** `Lab.3`

---

## Phase 2: Workstation Integration & Domain Validation

### Phase 2: Step 1 – Standardized Domain Join
The primary objective of this phase was to integrate the Windows 11 workstation into the established melvinlab.local forest. I standardized the client naming convention to MEL-CL-01 to align with the infrastructure schema and configured the network interface to utilize MEL-DC-01 (10.10.10.25) as the primary DNS resolver. By authenticating with administrative credentials, I successfully joined the workstation to the domain, establishing the trust relationship required for centralized management and future Group Policy deployment.

**Screenshots:** 
* `Lab.4` (The "Welcome to the Domain" popup)
* `Lab.5` (MEL-CL-01 visible in Active Directory Users and Computers)

---

## Phase 3: Organizational Hierarchy & User Provisioning

### Phase 3: Step 1 – Organizational Unit (OU) Architecture
With the core domain infrastructure established, I moved into the design and implementation of the directory’s logical structure. I created a top-level Parent OU, MelvinLab_users, to house all lab-specific data and separate it from default system containers. Within this root, I architected a nested OU hierarchy—specifically creating an Admins OU for privileged accounts and a Departments OU for standard business units (IT, HR, Finance, and Sales). This structure is a professional best practice that facilitates granular Group Policy targeting and delegated administrative permissions in future lab phases.

**Screenshot:** `Lab.6` (ADUC sidebar showing the MelvinLab_users nested tree)

### Phase 3: Step 2 – Manual User Provisioning & Identity Management
To build muscle memory for common Service Desk tasks, I manually provisioned 20 standard unique user accounts across the departmental OUs. I implemented a standardized naming convention of Firstname + LastInitial (e.g., MelvinW) to ensure consistency across the global address list. During the creation process, I enforced account security by enabling the "User must change password at next logon" attribute, simulating a real-world onboarding scenario where user privacy and initial credential rotation are required.

**Screenshot:** `Lab.7` (Properties of a user showing populated Department and Job Title fields)

### Phase 3: Step 3 – Administrative Escalation and Role Assignment
The final step of this phase involved the creation of dedicated administrative identities to practice the principle of least privilege. I provisioned a secondary admin account, ThomasA, within the Admins OU to serve as a backup to my primary account. I then manually escalated these accounts by modifying their Member Of attributes to include the Domain Admins security group. This ensures that administrative tasks are performed by designated identities rather than using the default built-in Administrator account.

**Screenshot:** `Lab.8` (The "Member Of" tab for ThomasA showing Domain Admins membership)

---

## Phase 4: Service Desk Operations & Access Control

### Phase 4: Step 1 – Security Group Implementation & RBAC
To transition from individual account management to Role-Based Access Control (RBAC), I implemented a Global Security Group strategy. I created departmental groups (e.g., GS_IT_Staff, GS_HR_Staff) within the MelvinLab_users OU hierarchy. By nesting the individual user accounts into these security groups, I established a scalable permission model. This ensures that future resource access—such as file shares or application permissions—can be managed at the group level rather than on a per-user basis, significantly reducing administrative overhead and the potential for permission creep.

**Screenshot:** `Lab.9` (The Members tab of GS_IT_Staff showing the IT users)

### Phase 4: Step 2 – Delegated Local Administration
I practiced the principle of least privilege by delegating local administrative authority without compromising domain-wide security. Instead of granting "Domain Admin" rights to technical staff for local troubleshooting, I modified the Local Administrators group on the MEL-CL-01 workstation. By adding the GS_IT_Staff security group to the local machine’s administrative database, I enabled all members of the IT department to perform elevated tasks (such as software installations and system configuration) on that specific endpoint while maintaining their status as standard users across the rest of the forest.

**Screenshot:** `Lab.10` (The Local Administrators group properties on MEL-CL-01 showing GS_IT_Staff as a member)

### Phase 4: Step 3 – Group Membership Verification
To confirm that the domain-level permissions were correctly inherited by the client workstation, I performed a technical verification via the command line. By logging into the MEL-CL-01 workstation as a departmental user and executing the `whoami /groups` command, I verified that the user's access token correctly reflected their membership in the GS_IT_Staff group. This confirms that the trust relationship between the client and the Domain Controller is healthy and that permissions are propagating as intended across the network.

**Screenshot:** `Lab.11` (The Command Prompt output showing the active group memberships)
