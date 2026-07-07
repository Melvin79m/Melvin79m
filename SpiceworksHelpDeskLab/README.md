# Spiceworks Help Desk Lab

## Overview

This lab documents 10 help desk tickets I worked through using Spiceworks Help Desk. I set up a simulated IT environment under an org called MelTech and acted as the sole technician. The goal was to get hands-on with real tier-1 support scenarios — account lockouts, hardware failures, printer issues, slow computers, email problems, and onboarding — and actually document the process the way you would on a real help desk.

Each ticket has the full lifecycle: how the ticket came in, what I tried, what fixed it, and what I took away from it.

---

## Environment

| Field | Value |
|---|---|
| Platform | Spiceworks Help Desk (Cloud) |
| Organization | MelTech |
| Technician | Melvin Williams |
| Tickets Completed | 10 |
| Spiceworks Ticket IDs | #4, #6, #7, #8, #9, #10, #11, #12, #13, #14 |

---

## Tickets

---

### Ticket #1 – Account Locked Out

**Priority:** High | **Category:** Access/Security | **Time to Resolution:** 8 minutes

**User:** Finance Department | **Asset:** CORP-WS-0145

**What happened:**

A Finance user called saying they couldn't log into their workstation. They kept getting "Your account has been locked out." They had been trying to log in for about 10 minutes.

**What I did:**

Verified who they were, then opened Active Directory Users and Computers on DC01 and looked up their account. The "Account is locked out" box was checked. I checked the security event logs and found 5 failed login attempts from their workstation between 8:45 and 8:52 AM. I unchecked the lockout box, applied it, then reset their password to a temporary one and had them change it on next login.

User was back in within 8 minutes. Told them to contact the help desk next time instead of keep retrying — every failed attempt pushes the lockout timer further.

**What I learned:**

Always check the event logs when unlocking an account. It tells you where the failed attempts came from, which helps rule out something more serious like someone trying to get into their account.

**Screenshots:**

![Creation](./screenshots/ticket-001-creation.png)
![Details](./screenshots/ticket-001-details.png)
![Troubleshooting](./screenshots/ticket-001-with-troubleshooting.png)
![Closed](./screenshots/ticket-001-closed.png)

---

### Ticket #2 – Printer Queue Stuck, Nothing Printing

**Priority:** Medium | **Category:** Hardware | **Time to Resolution:** ~15 minutes

**Printer:** HP LaserJet Pro 400 (FIN-PRINT-01) | **Department:** Finance

**What happened:**

Multiple Finance users reported their print jobs were going to the queue but nothing was printing. The printer looked fine — power on, display said "Ready."

**What I did:**

Went to the Finance floor to check it out in person. The printer was responsive and pingable at 192.168.1.50, so it wasn't a network issue. Opened the print queue and found several jobs stuck in an error state. Tried canceling them through the UI — they wouldn't clear. 

Opened Services (services.msc), stopped the Print Spooler, went to `C:\Windows\System32\spool\PRINTERS` and deleted the stuck spool files manually, then restarted the Spooler. Sent a test print — went right through. Confirmed with the Finance users that everything was printing again.

**What I learned:**

When print jobs are stuck and won't clear from the queue, stopping the Spooler and wiping the spool folder is the move. The UI sometimes just won't clear them — you have to go manual.

**Screenshots:**

![Creation](./screenshots/ticket-002-creation.png)
![Details](./screenshots/ticket-002-details.png)
![Troubleshooting](./screenshots/ticket-002-with-troubleshooting.png)
![Closed](./screenshots/ticket-002-closed.png)

---

### Ticket #3 – Access Denied on Finance Shared Drive

**Priority:** High | **Category:** Network | **Time to Resolution:** 12 minutes

**User:** Finance Department | **Share:** \\SERVER-DC01\Finance

**What happened:**

A Finance user got an "Access Denied" error trying to open the shared Finance drive. They said they had access just the day before and needed it urgently for month-end reports.

**What I did:**

Tested the share from my workstation first — it was accessible, so the share itself wasn't the problem. Pulled up their account in ADUC and checked their group memberships. They had been removed from the `Finance-Share-Access` security group, probably during a recent AD cleanup. No change request had been submitted for them, so it was clearly an accidental removal.

Added them back to the group, had them disconnect and reconnect the network drive, and confirmed they could open their files. Whole thing took 12 minutes.

**What I learned:**

Before assuming something broke, test it from your own machine first. That tells you right away if it's a share issue or a permissions issue. In this case the share was fine — it was just missing group membership.

**Screenshots:**

![Creation](./screenshots/ticket-003-creation.png)
![Details](./screenshots/ticket-003-details.png)
![Troubleshooting](./screenshots/ticket-003-with-troubleshooting.png)
![Closed](./screenshots/ticket-003-closed.png)

---

### Ticket #4 – Computer Completely Dead, Won't Power On

**Priority:** High | **Category:** Hardware | **Time to Resolution:** ~20 minutes

**Asset:** Dell OptiPlex 7090 (CORP-WS-0234) | **Department:** Marketing

**What happened:**

Marketing user called saying their computer wouldn't turn on at all. No lights, no fans, no sound — nothing. They had a presentation at 2:00 PM and it was urgent.

**What I did:**

Grabbed my toolkit and headed to their desk on the 3rd floor. Pressed the power button — zero response. Checked the monitor separately to rule it out — monitor was fine. Then I checked the power cable at the back of the computer. It was not fully seated at the power supply port — just loose enough to not make a proper connection.

Reseated it firmly at both ends, pressed power — computer came right on. POST completed, Windows loaded normally. Verified all their files and apps were there for the presentation.

**What I learned:**

Don't overlook the basics. A computer that's completely dead with zero signs of life is often just a power connection issue. Check the cable before assuming the hardware is fried.

**Screenshots:**

![Creation](./screenshots/ticket-004-creation.png)
![Details](./screenshots/ticket-004-details.png)
![Troubleshooting](./screenshots/ticket-004-with-troubleshooting.png)
![Closed](./screenshots/ticket-004-closed.png)

---

### Ticket #5 – Computer Extremely Slow, Taking 10+ Minutes to Boot

**Priority:** Medium | **Category:** Performance | **Time to Resolution:** 50 minutes

**Asset:** HP EliteDesk 800 G3 | **Department:** Accounting

**What happened:**

Accounting user said their computer had been getting slower over the past 2–3 weeks. At the point they called, it was taking 10–15 minutes to boot, apps were freezing, and they were getting "Not Responding" constantly.

**What I did:**

Remoted in and opened Task Manager. Disk usage was pinned at 100% — the bottleneck was clear. Checked available storage — the drive was almost full. Ran Disk Cleanup to free up temp files and update caches. Then I looked at fragmentation — it was bad. I scheduled an overnight defrag since running it during the day would make things worse. Also disabled a bunch of startup programs that had been loading every boot for no reason.

After the initial cleanup there was already some improvement. Followed up the next morning after the overnight defrag finished — the user said it felt like a new computer.

**What I learned:**

A spinning HDD that's nearly full and heavily fragmented will tank performance fast. 100% disk in Task Manager is a big tell. Also learned to schedule defrags overnight — running one on an already struggling machine during business hours just makes it worse.

**Screenshots:**

![Creation](./screenshots/ticket-005-creation.png)
![Details](./screenshots/ticket-005-details.png)
![Troubleshooting](./screenshots/ticket-005-with-troubleshooting.png)
![Closed](./screenshots/ticket-005-closed.png)

---

### Ticket #6 – Excel Crashing Every Time It Opens

**Priority:** High | **Category:** Software | **Time to Resolution:** ~30 minutes

**Application:** Office 365 ProPlus | **Department:** Finance

**What happened:**

Finance user called saying Excel was crashing every single time they tried to open it — even a blank new workbook. Error said "Microsoft Excel has stopped working." It started that morning after Windows updates installed overnight. They had an 11:00 AM meeting with spreadsheets they needed.

**What I did:**

Tried launching Excel in Safe Mode first (`excel.exe /safe`) — it opened fine. That told me it wasn't a full install corruption, more likely a conflict. Disabled all COM add-ins and relaunched — still crashed. Ran the Office Quick Repair — still crashed. Finally ran the Office Online Repair, which does a full reinstall of Office components from Microsoft's servers. After that finished and the machine restarted, Excel opened clean. Tested their actual spreadsheets to make sure everything worked before the meeting.

**What I learned:**

When Safe Mode works but normal mode doesn't, it's usually an add-in or component conflict. Quick Repair doesn't always cut it — sometimes you have to run the Online Repair which is more thorough. Also good to know that Windows updates can break Office installs.

**Screenshots:**

![Creation](./screenshots/ticket-006-creation.png)
![Details](./screenshots/ticket-006-details.png)
![Troubleshooting](./screenshots/ticket-006-with-troubleshooting.png)
![Closed](./screenshots/ticket-006-closed.png)

---

### Ticket #7 – Outlook Mailbox Full, Can't Send or Receive

**Priority:** High | **Category:** Email | **Time to Resolution:** ~35 minutes

**Department:** Sales

> **Note:** The Summary field on this ticket was accidentally typed as `ticket-006-closed` when I created it — that was just a data entry mistake during the lab setup. The actual issue is the Outlook mailbox problem documented below.

**What happened:**

Sales user got an error saying "Your mailbox is full. You cannot send or receive emails until you free up space." They had 8,500+ emails going back four years and had never archived or cleaned anything out. They needed to send client emails that day.

**What I did:**

Remoted in to take a look. Mailbox was at or over the 50GB Exchange Online limit. The Deleted Items folder alone was huge — permanently emptied that first since it was the easiest quick win. Then sorted the inbox by date and moved anything older than 12 months to a local Outlook archive (.pst file). Did the same with Sent Items. Also found some emails with massive attachments — moved those files to OneDrive and replaced them with share links.

Once the mailbox dropped below the quota, send and receive both came back. Walked the user through how to check their mailbox size going forward.

**What I learned:**

A lot of users don't realize their mailbox has a size limit until they hit it. The Deleted Items folder is always a good first move — most people never empty it. AutoArchive exists for a reason and this is exactly why.

**Screenshots:**

![Creation](./screenshots/ticket-007-creation.png)
![Details](./screenshots/ticket-007-details.png)
![Troubleshooting](./screenshots/ticket-007-with-troubleshooting.png)
![Closed](./screenshots/ticket-007-closed.png)

---

### Ticket #8 – Laptop Won't Connect to Corporate WiFi

**Priority:** Medium | **Category:** Network | **Time to Resolution:** ~13 minutes

**Asset:** Dell Latitude 5420 | **Department:** Human Resources

**What happened:**

HR user in a conference room couldn't connect to the corporate WiFi (MelTech-Secure). Kept getting "Can't connect to this network." Their phone connected to the same network fine, so the access point wasn't the issue.

**What I did:**

Had them forget the network and reconnect — same error. Ran Windows WiFi diagnostics — nothing useful came back. Opened Device Manager and looked at the Intel Wi-Fi 6 AX201 adapter. The driver looked old. Updated it through Device Manager, restarted, and on the first try after the reboot they connected with no problem.

**What I learned:**

An outdated or corrupted network adapter driver can cause authentication failures that look like a network or credentials problem. When basic troubleshooting doesn't work, check the driver. Also learned that the phone test is a quick way to rule out the access point.

**Screenshots:**

![Creation](./screenshots/ticket-008-creation.png)
![Details](./screenshots/ticket-008-details.png)
![Troubleshooting](./screenshots/ticket-008-with-troubleshooting.png)
![Closed](./screenshots/ticket-008-closed.png)

---

### Ticket #9 – Second Monitor Not Working, Showing "No Signal"

**Priority:** Medium | **Category:** Hardware | **Time to Resolution:** ~8 minutes

**Setup:** Dell laptop → Dell WD19 dock → 2x Dell P2422H monitors | **Department:** Engineering

**What happened:**

Engineering user came in and their second monitor was showing "No Signal." First monitor was fine. Both worked the afternoon before.

**What I did:**

Went to their desk to check it out. The dock looked fine. I swapped the DisplayPort cables between the two monitors to test — the working monitor lost signal, and the "dead" monitor came on. That isolated it to the cable, not the monitor or dock port. Grabbed a replacement DisplayPort cable, plugged it in, and both monitors were working immediately.

**What I learned:**

Cable swap testing is fast and effective. Instead of guessing whether it's the monitor, the dock port, or the cable, you swap and the answer becomes obvious. In this case the whole thing was done in under 10 minutes because of that.

**Screenshots:**

![Creation](./screenshots/ticket-009-creation.png)
![Details](./screenshots/ticket-009-details.png)
![Troubleshooting](./screenshots/ticket-009-with-troubleshooting.png)
![Closed](./screenshots/ticket-009-closed.png)

---

### Ticket #10 – New Hire Onboarding: Amanda Chen

**Priority:** High | **Category:** Access/Security | **Status:** In Progress

**New Hire:** Amanda Chen | **Role:** Marketing Coordinator | **Start Date:** January 6, 2026

**What happened:**

HR submitted a new hire request for Amanda Chen starting Monday January 6. The request came in Thursday afternoon, so there was one business day to get everything ready before her first day.

**What I did:**

Began working through the full onboarding checklist:

- [ ] Create Active Directory user account
- [ ] Set up Microsoft 365 email and assign license (achen@meltech.com)
- [ ] Image and configure her workstation
- [ ] Provision access to Marketing network shares
- [ ] Set up Adobe Creative Cloud, Canva, and HubSpot
- [ ] Enroll in security awareness training
- [ ] Configure MFA

> This ticket was captured mid-process. Screenshots show the creation and initial details stages as the onboarding was being worked. Full completion would follow before her 9:00 AM Monday start.

**What I learned:**

New hire onboarding touches a lot of systems at once — AD, M365, applications, network shares. It's the kind of ticket where you really need a checklist so nothing slips through. One missed step means a user shows up on day one and can't do their job.

**Screenshots:**

![Creation](./screenshots/ticket-010-creation.png)
![Details](./screenshots/ticket-010-details.png)

---

## Skills Practiced

| Area | Tickets |
|---|---|
| Active Directory – unlocking accounts, fixing group membership, creating users | #1, #3, #10 |
| Hardware troubleshooting – power, cables, printers | #2, #4, #9 |
| Windows performance – disk usage, fragmentation, startup programs | #5 |
| Microsoft Office – repair tools, troubleshooting crashes | #6 |
| Exchange Online – mailbox quotas, archiving | #7 |
| Network troubleshooting – WiFi auth, driver issues, shared drive access | #3, #8 |
| New hire onboarding – multi-system provisioning | #10 |
| Help desk ticketing – intake, triage, documentation, closure | All |

---

## Ticket Summary

| # | Spiceworks ID | Issue | Priority | TTR |
|---|---|---|---|---|
| 1 | #4 | Account locked out | High | 8 min |
| 2 | #6 | Printer queue stuck | Medium | ~15 min |
| 3 | #7 | Finance share access denied | High | 12 min |
| 4 | #8 | Workstation won't power on | High | ~20 min |
| 5 | #9 | Computer extremely slow | Medium | 50 min |
| 6 | #10 | Excel crashing on open | High | ~30 min |
| 7 | #11 | Outlook mailbox full | High | ~35 min |
| 8 | #12 | WiFi authentication failure | Medium | ~13 min |
| 9 | #13 | Second monitor no signal | Medium | ~8 min |
| 10 | #14 | New hire onboarding | High | In Progress |
