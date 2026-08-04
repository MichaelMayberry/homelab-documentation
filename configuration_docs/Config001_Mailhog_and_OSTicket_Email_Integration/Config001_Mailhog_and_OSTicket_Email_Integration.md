# Config #[001] — [Mailhog and OSTicket Email Integration]

| | |
|---|---|
| **Date Configured** |8/4/2026|
| **System(s) Involved** | SRV01-UBT (Ubuntu VM, OSTicket, Docker, Mailhog)|
| **Status** | Complete |

## Purpose
OSTicket need an SMTP server to send outbound emails for functionality. I wanted to have something light weight that would be able to do this rather than actually configuring a real mail server for a simple virtual home lab. I realized that I could use Mailhog as a fake SMTP catcher. Instead of something like Outlook or Gmail, Mailhog catches the SMTP email and displays it in the web UI, no verification of email addresses as well. This allows me to run a poller script which polls every 30 seconds from Mailhog server and displays the content in the terminal so then other machines on this network can grab any email that their respective username is matched too. This is also a big security flaw which I intended, as there is no authentication, so that I can exploit and document it in the future. All sent emails stay internal within the network

## Environment
| | |
|---|---|
| **Host system** |SRV01-UBT24 (Ubuntu Server)|
| **OS / Version** |Ubuntu 24.04|
| **Related services** |OSTicket (needs Apache/PHP/MySQL running directly on host), Mailhog (Docker Container) |

## Prerequisites
What needed to already be in place before starting this configuration.

- Apache installed
- MySql 5.5 or better
- PHP 8.2 but 8.4 is recomended
- 1GB Ram at least
- Docker Installed
- Mailhog running in a docker container with ports 1025 for SMTP and 8025 for a WebUI
- OSTicket running direclty on host not in Docker Container

## Configuration Steps
Numbered, sequential. Include the actual commands/settings used, not just descriptions.

1. Confirm Mailhog is running in docker container using: docker ps
2. Logged Into OSTicket Admin Panel and go to Emails -> Emails
3. Click on the selected default Support email address: My example was mayberry-admin@homelab.com
4. Open the Outgoing (SMTP) and set Status: Enable, Hostname: Server IP, PortNumber: 1025, Authentication: None, Header Spoofing: unchecked
5. Verify Mailhog is detecting traffic on port 1025 using python script
6. Trigger real test by creating and replying to a ticket in OSTicket


## Verification
How you confirmed the configuration actually works — the real test, not just "it looked right."

```
Created and replied to a ticket in OSTicket and Checked Mailhogs UI to confirm Mailhog received it
```
**Expected result:**
The osTicket generated notification email will populate the Mailhog inbox list
## Issues Encountered
Anything that didn't work as expected during setup, and how it was resolved. (If nothing came up, note that too — it's still useful to know a setup went cleanly.)

| Issue | Root Cause | Fix |
|---|---|---|
| Vbox can be weird with NTP and also keeping the state of the VMs so | NTP and saved state of machines can interfere with authentication tokens | Every time I boot up the VMs i must make sure they all have the same time with the AD and if not, I have to sync them|

## Limitations / Known Gaps
Mailhog only catches outbound mail. It does not support incoming mail parsing/fetching such as protocols POP/IMAP. This means I can not create a ticket by emailing I have to us the OSTicket interface

## Notes for Next Time
Make sure to check current times on VMs and if they are in sync with AD. Also make sure every service need is running such as Mailhog and Docker

## References
MailHog GitHub, OSTicket Documentation
