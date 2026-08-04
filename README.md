<p align="center">
  <img src="assets/homelab-logo.png" width="120" height="120" alt="homelab.local logo">
</p>

<h1 align="center">Homelab Documentation</h1>
<p align="center"><strong>HOMELAB.LOCAL — SOC & IT Operations Practice Lab</strong></p>

Documentation for a home lab built for hands-on SOC analyst and IT help desk practice. Covers Active Directory, cross-platform Linux/Windows authentication, SIEM monitoring, and a full help desk ticketing workflow — all running on VirtualBox with a 16GB RAM budget.

## What's in here

| Folder | Purpose |
|---|---|
| [`tickets/`](./tickets) | Troubleshooting log — real issues encountered in the lab, documented in a ticket/KB-article format (symptoms, root cause, resolution, prevention) |
| [`configs/`](./configs) | Configuration write-ups for services set up in the lab (integrations, installs, settings) |
| [`assets/`](./assets) | Logos and shared images |

Each ticket/config entry lives in its own folder alongside the screenshots referenced in it, e.g.:
```
tickets/ticket-001-winbind-auth-failure/
├── ticket-001-winbind-auth-failure.md
└── (screenshots referenced in the writeup)
```

## Lab Environment

| Role | System | Notes |
|---|---|---|
| Domain Controller | Windows Server (AD DS + DNS) | `homelab.local` |
| Linux Server | Ubuntu Server | Wazuh SIEM, Samba/winbind (domain-joined), osTicket, MailHog (Docker) |
| Workstations | Windows 10/11 | Domain-joined endpoints |
| Attacker Box | Kali Linux | On-demand only, not domain-joined |

## Why this exists

Built to demonstrate hands-on experience for SOC analyst and IT help desk roles — not just tool familiarity, but the actual troubleshooting process: root-cause chasing, documentation habits, and getting disparate systems (AD, SIEM, ticketing, mail) to work together the way they would in a real environment.

## Highlights

- Joined a Linux server to Active Directory via Samba/winbind — traced and resolved a multi-layered failure chain (DNS misconfiguration → hostname mismatch → missing packages → Kerberos clock skew → socket permissions)
- Integrated MailHog with osTicket for testable email notifications without live mail infrastructure
- Documented every build and fix using consistent templates, treating the lab as a portfolio rather than a one-off project

---
*Maintained by Mike Mayberry — built for SOC analyst / IT support job search practice.*
