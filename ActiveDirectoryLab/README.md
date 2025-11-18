![Project Status](https://img.shields.io/badge/Project-In%20Progress-yellow)
![Last Update](https://img.shields.io/badge/Last%20Update-November%202025-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![Tech Stack](https://img.shields.io/badge/Tech-VirtualBox%20%7C%20Windows%20Server%202022-lightgrey)

# Active Directory Home Lab Project

This project is the start of my personal IT home lab, where I’ll be getting hands-on experience with **Windows Server 2022** and **Active Directory**.

The goal is to build a small virtual network using **Oracle VirtualBox** to simulate a real-world business environment. I’ve started by downloading the core tools:

- Windows 11 ISO – for the client machine  
- Windows Server 2022 ISO – for the domain controller  
- VirtualBox – to manage and run the virtual machines

Through this project, I’ll be setting up:

- An **Active Directory Domain**  
- **User and group management**  
- **Group Policies**  
- **DNS and DHCP services**  

> **Note:** This is an ongoing project and I will continue adding more steps, screenshots, and documentation as I expand my lab.

---

## Table of Contents

1. [Step 1: Installing the ISOs in VirtualBox](#step-1-installing-the-isos-in-virtualbox)  
2. [Step 2: Installing and Configuring Active Directory](#step-2-installing-and-configuring-active-directory)  
3. [Step 3: Installing Guest Additions and Creating Users](#step-3-installing-guest-additions-and-creating-users)  
4. [Step 4: Network Configuration and Domain Connection](#step-4-network-configuration-and-domain-connection)  
5. [Step 5: User Account Management and Security Policies](#step-5-user-account-management-and-security-policies)  
6. [Step 6: Installing and Using Action1](#step-6-installing-and-using-action1)  
7. [Notes / Observations](#notes--observations)  
8. [Certifications](#certifications)  

---

## Step 1: Installing the ISOs in VirtualBox

I created two virtual machines in Oracle VirtualBox—one for **Windows Server 2022** and one for **Windows 11**. Each VM was set up using its respective ISO file. Windows Server 2022 will act as the domain controller, and Windows 11 will serve as the client machine.

**Screenshots:**  
![Step 1-0](./screenshots/Lab/1.0.png)  
![Step 1-1](./screenshots/Lab/1.1.png)  
![Step 1-2](./screenshots/Lab/1.2.png)  

---

## Step 2: Installing and Configuring Active Directory

Installed **Active Directory Domain Services (AD DS)** on Windows Server 2022 and promoted the server to a **Domain Controller**. Created a new forest and domain named **MelTech.com**, then rebooted the server to complete the setup.

**Screenshots:**  
![Step 2-0](./screenshots/Lab/2.0.png)  
![Step 2-1](./screenshots/Lab/2.1.png)  
![Step 2-2](./screenshots/Lab/2.2.png)  
![Step 2-3](./screenshots/Lab/2.3.png)  

---

## Step 3: Installing Guest Additions and Creating Users

Installed **VirtualBox Guest Additions** on the Windows Server 2022 VM to enable folder sharing between the host and VM. Created two **Active Directory user accounts**: **Thomas C Anderson** and **Melvin L Williams**, used to test domain connectivity from the client machine.

**Screenshots:**  
![Step 3-0](./screenshots/Lab/3.0.png)  
![Step 3-1](./screenshots/Lab/3.1.png)  
![Step 3-2](./screenshots/Lab/3.2.png)  

---

## Step 4: Network Configuration and Domain Connection

Configured network settings and connected the Windows 11 client to the domain. Assigned static IP addresses: `10.1.10.2` to the Windows Server 2022 Domain Controller, `10.1.10.3` to the Windows 11 client. Verified the connection by confirming **Desktop01** appeared under the Computers container in Active Directory Users and Computers. Enabled Remote Desktop access and confirmed connectivity.

**Screenshots:**  
![Step 4-0](./screenshots/Lab/4.0.png)  
![Step 4-1](./screenshots/Lab/4.1.png)  
![Step 4-2](./screenshots/Lab/4.2.png)  
![Step 4-3](./screenshots/Lab/4.3.png)  
![Step 4-4](./screenshots/Lab/4.4.png)  
![Step 4-5](./screenshots/Lab/4.5.png)  
![Step 4-6](./screenshots/Lab/4.6.png)  

---

## Step 5: User Account Management and Security Policies

Managed user accounts and applied security policies within Active Directory. Practiced resetting passwords, activating/disabling accounts, deleting accounts, and setting login hour restrictions (e.g., Thomas C Anderson Mon–Fri 6:00 a.m.–6:00 p.m.).  

Under **Group Policy**, updated security settings:

- Max password age: 90 days  
- Account lockout threshold: 3 failed attempts  
- Lockout duration: 360 minutes  

Verified the policies by testing failed logins, then unlocked accounts in **Active Directory Users and Computers**.

**Screenshots:**  
![Step 5-0](./screenshots/Lab/5.0.png)  
![Step 5-1](./screenshots/Lab/5.1.png)  
![Step 5-2](./screenshots/Lab/5.2.png)  
![Step 5-3](./screenshots/Lab/5.3.png)  
![Step 5-4](./screenshots/Lab/5.4.png)  
![Step 5-5](./screenshots/Lab/5.5.png)  
![Step 5-6](./screenshots/Lab/5.6.png)  

---

## Step 6: Installing and Using Action1

Downloaded and installed **Action1** on the Windows Server 2022 Domain Controller. Scanned for missing updates and deployed **five updates**, then ran **vulnerability remediation** to identify and address potential security risks.

**Screenshots:**  
![Step 6-0](./screenshots/Lab/6.0.png)  
![Step 6-1](./screenshots/Lab/6.1.png)  

---

## Notes / Observations

- Active Directory setup & domain management  
- Group Policy & security enforcement  
- Network configuration & client-domain connectivity  
- Patch management & vulnerability remediation  

---

## Certifications

- CompTIA Security+  
- Microsoft Azure Fundamentals (AZ-900)  
- Currently studying for Cisco CCNA
