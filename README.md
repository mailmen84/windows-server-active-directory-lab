# Windows Server & Active Directory Lab

Hands-on learning project and homelab documentation for Windows Server administration,
Active Directory, PowerShell and network infrastructure. The goal is to build practical
and theoretical skills required for a **Junior Windows System Administrator** role.

The end state of the lab is a working Active Directory domain in a homelab, with all
compatible Windows computers joined to it.

## Repository structure

| Path | Purpose |
|------|---------|
| `README.md` | Project overview (this file) |
| `PROJECT_INSTRUCTIONS.md` | Learning rules, lesson format and safety rules |
| `LEARNING_ROADMAP.md` | Full curriculum, split into modules and steps |
| `PROGRESS.md` | Current status, completed steps and next step |
| `docs/lab/` | Homelab inventory, network plan, naming conventions |
| `docs/modules/` | Notes for each completed module (GUI + PowerShell) |
| `scripts/powershell/` | PowerShell scripts created during the course |
| `diagrams/` | Network and AD diagrams |

## Homelab overview

| Component | Role |
|-----------|------|
| HP ProLiant DL380 Gen9 | Proxmox VE hypervisor, hosts the Windows Server VM(s) |
| Dell PowerEdge R730 | TrueNAS SCALE storage |
| pfSense | Firewall / router, inter-VLAN routing |
| Pi-hole | DNS filtering |
| Cisco managed switches | Switching, VLANs |

Details are kept in [`docs/lab/inventory.md`](docs/lab/inventory.md).

## Conventions

- All repository content (docs, scripts, comments, commit messages) is in **English**.
- **No secrets** in the repository: no passwords, tokens, private keys or license keys.
- Every configuration task is done twice where possible: **GUI first, then PowerShell**.
- Every completed step is documented and recorded in [`PROGRESS.md`](PROGRESS.md).

## Main references

- [Microsoft Learn – Windows Server](https://learn.microsoft.com/windows-server/)
- [Microsoft Learn – Active Directory Domain Services](https://learn.microsoft.com/windows-server/identity/ad-ds/active-directory-domain-services)
- [Proxmox VE documentation](https://pve.proxmox.com/pve-docs/)
- [GitHub Docs](https://docs.github.com/)
