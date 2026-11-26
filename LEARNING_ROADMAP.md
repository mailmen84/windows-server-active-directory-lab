# Learning Roadmap

Detailed learning programme. The module list matches the roadmap table in
[`README.md`](README.md). Each module is split into small steps; the steps of a
module may be refined when the module starts. Status is tracked in
[`PROGRESS.md`](PROGRESS.md).

Where possible, every step is done twice: GUI first, then PowerShell.

## Module 00 – GitHub and Project Organisation
- 00.1 Repository, commit, branch and Pull Request basics (review and merge the initial documentation)
- 00.2 Cloning the repository locally (GitHub Desktop or `git` CLI)
- 00.3 Editing, committing and pushing a change
- 00.4 `.gitignore` and keeping secrets out of the repository

## Module 01 – Windows Server Environment Preparation
- 01.1 Inventory of the existing Windows Server VM (version, edition, resources)
- 01.2 Proxmox VM review (CPU type, RAM, disks, VirtIO drivers, QEMU Guest Agent)
- 01.3 Proxmox snapshot and backup before changes
- 01.4 Naming conventions (domain name, server names, OUs, accounts)
- 01.5 Windows Update, time zone and computer name

## Module 02 – Network Configuration
- 02.1 IP addressing and VLAN plan for the lab
- 02.2 Static IP address configuration on the server
- 02.3 DNS client settings for a future Domain Controller
- 02.4 pfSense firewall rules and connectivity tests (`ping`, `Test-NetConnection`)

## Module 03 – Active Directory Fundamentals
- 03.1 AD DS concepts: forest, domain, Domain Controller, schema, Global Catalog
- 03.2 Installing the AD DS role
- 03.3 Promoting the first Domain Controller (new forest, AD-integrated DNS)
- 03.4 Post-promotion verification (`dcdiag`, services, SYSVOL and NETLOGON)

## Module 04 – User and Group Management
- 04.1 Organizational Unit (OU) design
- 04.2 User accounts
- 04.3 Groups: scope and type, AGDLP model
- 04.4 Bulk operations with PowerShell (CSV import)

## Module 05 – Computer and Domain Management
- 05.1 Client prerequisites (DNS, time, edition: Pro/Enterprise)
- 05.2 Joining a test VM to the domain
- 05.3 Moving computer objects into OUs
- 05.4 Joining physical Windows computers (with local profile and data protection)

## Module 06 – Group Policy Management
- 06.1 GPO concepts and processing order (LSDOU)
- 06.2 Creating and linking GPOs
- 06.3 Common policies (password policy, drive mappings, desktop settings)
- 06.4 `gpupdate`, `gpresult` and GPO troubleshooting

## Module 07 – DNS and DHCP Services
- 07.1 Forward and reverse lookup zones, record types
- 07.2 Forwarders to pfSense / Pi-hole and conditional forwarders
- 07.3 DNS troubleshooting (`nslookup`, `Resolve-DnsName`)
- 07.4 DHCP concepts and choosing the DHCP server (pfSense vs Windows Server)
- 07.5 Installing and authorizing the DHCP role, scopes, options and reservations

## Module 08 – File Servers and Permissions
- 08.1 File Server role and SMB shares
- 08.2 NTFS vs share permissions
- 08.3 Access-based enumeration and drive mappings via GPO
- 08.4 TrueNAS SCALE joined to the domain (SMB with AD accounts)

## Module 09 – PowerShell and Automation
- 09.1 PowerShell basics: cmdlets, pipeline, objects, help
- 09.2 The ActiveDirectory module
- 09.3 Writing and running scripts safely (execution policy)
- 09.4 Remote administration: RSAT, PowerShell Remoting (WinRM), Windows Admin Center
- 09.5 Scheduled tasks and reporting

## Module 10 – Security and Backup
- 10.1 Separate admin accounts and least privilege
- 10.2 Password and account lockout policies, fine-grained password policies
- 10.3 Windows LAPS
- 10.4 Auditing and event logs
- 10.5 Windows Server Backup and system state backup
- 10.6 Proxmox backups of a Domain Controller (and why snapshots are not AD backups)

## Module 11 – Advanced Active Directory Administration
- 11.1 Adding a second Domain Controller
- 11.2 Sites and Services, replication, `repadmin`
- 11.3 FSMO roles: transfer and seizure
- 11.4 AD Recycle Bin, authoritative vs non-authoritative restore
- 11.5 Proxmox authentication against Active Directory

## Module 12 – Real-World Administration Scenarios
- 12.1 New employee onboarding
- 12.2 Employee offboarding
- 12.3 Password reset and account unlock
- 12.4 Troubleshooting: logon, trust relationship and time synchronization (W32Time) problems
- 12.5 Helpdesk-style tickets
