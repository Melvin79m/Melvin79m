# Azure Admin Lab — Entra ID Users, Groups & Administrative Units

**Platform:** Microsoft Azure (Entra ID)  
**Skills:** User management, Security groups, RBAC role assignment, Administrative Units

---

## What I Built

A working Entra ID environment using Philadelphia sports teams as the user/group structure. The lab covers creating users, organizing them into security groups, assigning directory roles, and scoping those roles with an Administrative Unit.

---

## Part 1 — Users & Security Groups (2026-08-05)

Created member users across two Philadelphia sports teams and organized them into **Security groups with Assigned membership**.

### Philadelphia 76ers Group
Players added as member users in Entra ID, then placed in the `Philadelphia 76ers` security group.

![76ers group members](screenshots/01-76ers-group-members.png)

### Philadelphia Phillies Group
Created the `Philadelphia Phillies` security group with 5 players:

![Phillies members](screenshots/04-phillies-members.png)

Both groups visible in the All Groups view — Security type, Assigned membership:

![All groups — two groups](screenshots/03-all-groups-two.png)

---

## Part 2 — Role Assignments & Additional Groups (2026-08-07)

### Helpdesk Administrator Role Assignment
Assigned the **Helpdesk Administrator** built-in role to all 5 Phillies players at **Directory** scope. This gives them the ability to reset passwords for non-admin users across the entire tenant.

![Helpdesk Admin assignments](screenshots/05-helpdesk-admin-assignments.png)

### Fans Group
Created a `Fans` security group with 5 members — separate from team staff and players.

![Fans group members](screenshots/06-fans-group-members.png)

**Members:** Brittney Jefferson, James Washington, Jerry Thomas, Kevin Stevenson, Larry Jackson

### Staff Groups
Created two additional staff groups — one per team:

**76ers Staff** — Max Smith, Nichole Frank, Sam Adams, Sarah Greene, Steve Jones

![76ers Staff members](screenshots/09-76ers-staff-members.png)

**Phillies Staff** — Amber Brown, Brad Thompson, Jackie Wilcox, Jon Walker, Liz Simpson

![Phillies Staff members](screenshots/10-phillies-staff-members.png)

All 5 groups in the final All Groups view:

![All groups — five groups](screenshots/08-all-groups-five.png)

| Group | Type | Membership |
|---|---|---|
| 76ers Staff | Security | Assigned |
| Fans | Security | Assigned |
| Philadelphia 76ers | Security | Assigned |
| Philadelphia Phillies | Security | Assigned |
| Phillies Staff | Security | Assigned |

---

## Part 3 — Administrative Unit: Citizen Bank Park

Created an **Administrative Unit** named `Citizen Bank Park` (the Phillies' stadium) to scope admin roles to a specific subset of the directory.

### AU Creation — Review + Create
Configured the AU and assigned the **Password Administrator** role to the 5 Phillies players — but scoped *only* to this AU, not the full directory.

![Creating Citizen Bank Park AU](screenshots/07-create-citizen-bank-park-au.png)

**Password Administrator (scoped to Citizen Bank Park AU):**
- Bryce Harper
- Chris Sanchez
- J.T. Realmuto
- Kyle Schwarber
- Zach Wheeler

### AU Members
Added the **Phillies Staff** users as members of the AU — these are the accounts the scoped admins can manage.

![Citizen Bank Park AU users](screenshots/11-citizen-bank-park-au-users.png)

**AU Members:** Amber Brown, Brad Thompson, Jackie Wilcox, Jon Walker, Liz Simpson

---

## Key Concepts Demonstrated

| Concept | Applied As |
|---|---|
| Security groups (Assigned) | 5 groups across two teams + fans |
| Built-in RBAC role assignment | Helpdesk Admin → Phillies players at directory scope |
| Administrative Units | Citizen Bank Park AU scoping Password Admin to Phillies Staff only |
| Role scoping | Same users have a *broader* role (Helpdesk Admin, directory-wide) and a *narrower* role (Password Admin, AU-scoped) |

Administrative Units let you give someone a role without giving them access to the whole tenant. The Phillies players can reset passwords — but only for users inside `Citizen Bank Park`.
