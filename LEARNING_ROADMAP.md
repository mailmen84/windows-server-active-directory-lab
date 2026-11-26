# Learning Roadmap

The curriculum is split into modules. Each module is split into small steps.
Steps are refined as the course progresses; the step list of a module may grow
once we reach it. Status is tracked in [`PROGRESS.md`](PROGRESS.md).

## Module 0 – Git and GitHub
- 0.1 Repository, branch, commit and Pull Request basics (review and merge the initial docs)
- 0.2 Cloning the repository locally (GitHub Desktop / `git` CLI)
- 0.3 Editing, committing and pushing a change
- 0.4 `.gitignore` and keeping secrets out of the repository

## Module 1 – Lab planning and the Windows Server VM
- 1.1 Inventory of the existing Windows Server VM (version, edition, resources)
- 1.2 Proxmox VM review (CPU type, RAM, disks, VirtIO drivers, QEMU Guest Agent)
- 1.3 Proxmox snapshot and backup before changes
- 1.4 Naming conventions (domain name, server names, OUs, accounts)
- 1.5 Windows Update, time zone, computer name

## Module 2 – Networking for a Domain Controller
- 2.1 IP addressing and VLAN plan for the lab
- 2.2 Static IP address configuration
- 2.3 DNS client settings for a future DC
- 2.4 pfSense rules and connectivity tests (`ping`, `Test-NetConnection`)

## Module 3 – Active Directory Domain Services
- 3.1 AD DS concepts: forest, domain, DC, schema, global catalog
- 3.2 Installing the AD DS role
- 3.3 Promoting the first Domain Controller (new forest)
- 3.4 Post-promotion verification (`dcdiag`, services, SYSVOL/NETLOGON)

## Module 4 – DNS
- 4.1 AD-integrated DNS zones
- 4.2 Forward and reverse lookup zones, records
- 4.3 Forwarders (pfSense / Pi-hole) and conditional forwarders
- 4.4 DNS troubleshooting (`nslookup`, `Resolve-DnsName`)

## Module 5 – DHCP
- 5.1 DHCP concepts and choosing the DHCP server (pfSense vs Windows)
- 5.2 Installing and authorizing the DHCP role
- 5.3 Scopes, options, reservations
- 5.4 DHCP failover (later, with a second server)

## Module 6 – Users, Groups and Organizational Units
- 6.1 OU design
- 6.2 User accounts
- 6.3 Groups (scope and type, AGDLP)
- 6.4 Bulk operations with PowerShell (CSV import)

## Module 7 – Domain Join
- 7.1 Client prerequisites (DNS, time, edition: Pro/Enterprise)
- 7.2 Joining a test VM to the domain
- 7.3 Joining physical Windows computers
- 7.4 Moving computer objects into OUs

## Module 8 – Group Policy
- 8.1 GPO concepts, LSDOU processing order
- 8.2 Creating and linking GPOs
- 8.3 Common policies (password policy, drive maps, desktop settings)
- 8.4 `gpupdate`, `gpresult`, troubleshooting

## Module 9 – File Server, SMB and NTFS Permissions
- 9.1 File Server role and SMB shares
- 9.2 NTFS vs share permissions
- 9.3 Access-based enumeration, mapped drives via GPO
- 9.4 Integration with TrueNAS SCALE (SMB, AD join)

## Module 10 – PowerShell and Automation
- 10.1 PowerShell basics: cmdlets, pipeline, objects, help
- 10.2 ActiveDirectory module
- 10.3 Writing and running scripts safely (execution policy)
- 10.4 Scheduled tasks and reporting

## Module 11 – Remote Administration
- 11.1 RSAT on a Windows client
- 11.2 PowerShell Remoting (WinRM)
- 11.3 Remote Desktop and Windows Admin Center

## Module 12 – Security
- 12.1 Tiered admin accounts, least privilege
- 12.2 Fine-grained password policies, account lockout
- 12.3 LAPS
- 12.4 Auditing and event logs
- 12.5 Hardening the Domain Controller

## Module 13 – Backup and Disaster Recovery
- 13.1 Windows Server Backup and system state backup
- 13.2 Proxmox backups of the DC (and why snapshots are not AD backups)
- 13.3 AD Recycle Bin and object restore
- 13.4 Authoritative vs non-authoritative restore

## Module 14 – Second Domain Controller and Replication
- 14.1 Adding a second DC
- 14.2 Sites and services, replication topology
- 14.3 `repadmin` and replication troubleshooting

## Module 15 – FSMO Roles
- 15.1 The five FSMO roles
- 15.2 Transferring roles
- 15.3 Seizing roles (disaster scenario)

## Module 16 – Homelab Integration
- 16.1 pfSense: DNS, DHCP relay, firewall rules for AD
- 16.2 Pi-hole together with AD DNS
- 16.3 TrueNAS SCALE joined to the domain
- 16.4 Proxmox authentication against AD (LDAP/AD realm)

## Module 17 – Troubleshooting
- 17.1 Event Viewer and common AD/DNS errors
- 17.2 Domain join, logon and trust relationship problems
- 17.3 Time synchronization (W32Time)

## Module 18 – Practical Administration Scenarios
- 18.1 New employee onboarding
- 18.2 Employee offboarding
- 18.3 Password reset and account unlock
- 18.4 Helpdesk-style tickets
