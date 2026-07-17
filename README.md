[README.md](https://github.com/user-attachments/files/30142521/README.md)
# active-directory-home-lab
Self-built AD lab demonstrating domain setup, GPOs, and troubleshooting
# Active Directory Home Lab

## Project Overview
A self-directed home lab project built to gain hands-on experience with core IT support tasks: deploying a Windows domain, managing users and groups, joining a client workstation to the domain, and enforcing policy through Group Policy Objects (GPOs). This project simulates the day-to-day environment of a company's internal network and the kinds of tickets an IT support technician handles regularly.

## Tools & Environment
- **VirtualBox** — virtualization platform
- **Windows Server 2022** (evaluation) — domain controller
- **Windows 11** (evaluation) — domain-joined client workstation
- **Active Directory Domain Services (AD DS)**
- **Group Policy Management**
- **Domain:** `homelab.local`

## What I Built

### Phase 1: Domain Controller Setup
- Installed Windows Server in VirtualBox and configured networking
- Installed the Active Directory Domain Services (AD DS) role
- Promoted the server to a domain controller and created the domain `homelab.local`
- Verified AD installation and DNS functionality

### Phase 2: Active Directory Configuration
- Created an Organizational Unit (`Employees`) to organize accounts
- Created a domain user account (`jsmith`) and a security group (`Sales`)
- Verified user/group structure in Active Directory Users and Computers

### Phase 3: Domain Join
- Joined the client workstation (`PC01`) to the `homelab.local` domain
- Verified connectivity between `PC01` and the domain controller

### Phase 4: Domain Authentication Testing
- Logged into `PC01` using the domain account `jsmith`
- Verified successful authentication against Active Directory

### Phase 5: Group Policy Enforcement
- Created a GPO (`Restrict Control Panel`) and linked it to the `Employees` OU
- Verified enforcement — Control Panel access is blocked for `jsmith` on `PC01`

## Screenshots

### Domain Controller Promotion
![Domain promotion](images/domain-promotion.png)
<img width="1018" height="916" alt="domain-promotion" src="https://github.com/user-attachments/assets/b0bccdce-40bd-470d-be27-112ef7fd1d14" />

### Active Directory Users, OUs, and Groups
![AD Users and Computers](images/ad-users-groups.png)
<img width="1006" height="946" alt="ad-users-groups" src="https://github.com/user-attachments/assets/cc2af075-ba23-4012-a8b4-faba4dc8ecdd" />
<img width="1010" height="874" alt="ad-users-groups pt 2" src="https://github.com/user-attachments/assets/12c4e310-3b25-423e-aa52-bdf0f329f944" />


### Group Policy Configuration
![GPO settings](images/gpo-config.png)
<img width="1016" height="940" alt="gpo-config" src="https://github.com/user-attachments/assets/07a75f37-1a85-4ae4-bf1e-b4e0c233b5de" />

### Domain-Joined Client Login
![Client domain login](images/client-login.png)
<img width="1000" height="918" alt="client-login" src="https://github.com/user-attachments/assets/b77e18d7-1058-44f6-a39c-9b2c3d2a9c81" />

### Policy Enforcement Verified
![Policy enforcement](images/policy-enforcement.png)
<img width="1020" height="924" alt="policy-enforcement" src="https://github.com/user-attachments/assets/ede0ce16-d19f-414d-bbbb-d5d856d90659" />

## Troubleshooting Highlights
Real IT support work is as much about diagnosing issues as it is configuration. Three issues came up during this project:

**Domain vs. Workgroup confusion during client join**
When joining `PC01` to the network, it wasn't initially clear whether `homelab.local` belonged in the "Workgroup" or "Domain" field. After reviewing the purpose of each, I confirmed that Active Directory requires a domain join (not a workgroup) and resolved it correctly.

**"Username or password is incorrect" on first login attempt**
After joining the domain, `jsmith` couldn't log into `PC01`. I methodically checked each layer — confirmed the domain join was successful, confirmed the account existed in Active Directory, then compared the username as created vs. as entered at login and found a mismatch. Correcting the username resolved the issue and authentication succeeded.

**GPO not applying to the target OU**
After configuring the Control Panel restriction policy, it wasn't taking effect on `PC01`. I checked Group Policy Management and found the GPO had been created but not actually linked to the `Employees` OU. Linking it and running `gpupdate /force` resolved the issue — verified by a "Restrictions" popup blocking Control Panel access.

## What I Learned
- How domain controllers manage authentication and access across a network
- How to structure OUs, users, and groups the way real organizations do
- How Group Policy is used to enforce security and system settings company-wide
- Practical troubleshooting methodology: isolating a problem layer by layer (network → domain join → account → credentials → policy link) rather than guessing

## Why This Project
I built this lab to develop real, hands-on IT support skills — account provisioning, permissions management, and policy enforcement — that mirror tasks handled daily by IT helpdesk and support technicians.and honestly it was so fun. 
