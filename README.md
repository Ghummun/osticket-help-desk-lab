# osTicket Help Desk Ticketing System — Azure

A self-hosted IT help desk ticketing system built on a Linux virtual machine in Microsoft Azure, running osTicket on a LAMP stack. This project simulates the full lifecycle of a help desk environment: standing up the server, configuring departments and SLAs, onboarding agents and end users, and working real tickets from submission to resolution — exactly the workflow a help desk analyst handles day to day.

## Project overview

- **Platform:** Microsoft Azure (Free Tier)
- **VM:** `osticket-vm` — Ubuntu 24.04 LTS, Standard D2ds v7 (2 vCPUs, 8 GiB RAM)
- **Resource group:** `helpdesk-lab`
- **Stack:** Apache, MySQL, PHP (LAMP)
- **Ticketing software:** osTicket v1.18.1
- **Public IP:** 52.188.69.81

## What this project demonstrates

- Deploying and configuring a Linux VM in Azure, including networking, security groups, and inbound port rules
- Connecting to a remote Linux server via SSH
- Installing and configuring a full LAMP stack (Apache, MySQL, PHP) from the command line
- Creating a MySQL database and dedicated database user for an application
- Installing and configuring osTicket, including post-install security hardening
- Designing a department structure (IT Support, Network Operations) and tiered SLA plans (SEV-1/2/3) based on real industry standards
- Creating help topics, staff agents, and end users to simulate a realistic organization
- Working tickets end to end: triage (priority, department, SLA, assignment), internal notes, agent replies, and resolution

## Build walkthrough

### 1. Provisioning the virtual machine

Created a new VM named `osticket-vm` in a dedicated `helpdesk-lab` resource group, running Ubuntu 24.04 LTS. The deployment includes a virtual network, network security group, and public IP — with inbound rules opened for SSH (22), HTTP (80), and HTTPS (443).

![VM deployment complete](screenshots/vm_deployment_complete.png)
![VM overview](screenshots/vm_overview.png)

### 2. Connecting via SSH

Connected to the VM remotely via SSH from a Windows PowerShell terminal to begin server configuration.

![SSH connected](screenshots/ssh_connected.png)

### 3. Installing the LAMP stack and osTicket

With the server updated, installed Apache (web server), MySQL (database), and PHP with the extensions osTicket requires. Created a dedicated `osticket` database and `osticketuser` MySQL account, then downloaded, extracted, and configured osTicket before restarting Apache.

### 4. Running the osTicket installer

Navigated to the osTicket setup page in a browser to confirm the server met all prerequisites — PHP 8.3 and the MySQLi extension — before proceeding with installation.

![osTicket installer - prerequisites check](screenshots/osticket_installer.png)

### 5. Completing installation

Filled out the installer with the helpdesk name, admin account, and database credentials. Installation completed successfully, after which the setup directory was removed and config file permissions were locked down for security — a standard post-install hardening step.

![osTicket installation complete](screenshots/osticket_install_complete.png)

### 6. Logging into the admin dashboard

Logged into the Staff Control Panel for the first time, confirming osTicket was fully operational with the default "osTicket Installed!" ticket already in the queue.

![osTicket admin dashboard](screenshots/osticket_dashboard.png)

### 7. Configuring departments

osTicket ships with three default departments (Maintenance, Sales, Support). Added two more to reflect a real IT environment: **IT Support** and **Network Operations** — each handling a different category of ticket.

![Default departments](screenshots/departments.png)
![Departments after adding IT Support and Network Operations](screenshots/departments_complete.png)

### 8. Building SLA plans

Created tiered Service Level Agreement plans based on standard industry severity levels:

- **SEV-1** — 1 hour grace period (critical issues, e.g. system down)
- **SEV-2** — 4 hour grace period (high priority, department-impacting)
- **SEV-3** — 8 hour grace period (normal, single-user issues)

![SLA plans](screenshots/sla_plans_complete.png)

### 9. Creating agents and users

Created two staff agents — **John Smith** (IT Support) and **Jane Doe** (Network Operations) — alongside the default admin account. Also created three end users — **Mike Johnson**, **Sarah Williams**, and **David Brown** — to simulate employees submitting support requests.

![Agents](screenshots/agents_complete.png)
![Users](screenshots/users_complete.png)

### 10. Submitting tickets through the user portal

From the public-facing support portal, submitted three realistic tickets covering common help desk categories: a password reset, a network connectivity issue, and a software installation request.

![User support portal](screenshots/user_portal.png)
![Ticket submitted confirmation](screenshots/_tickets_submitted.png)

### 11. Viewing the ticket queue

After all three tickets were submitted, the agent dashboard shows the full open ticket queue — each entry showing the ticket number, subject, submitter, and priority, ready to be triaged.

![Ticket queue](screenshots/ticket_queue.png)

### 12. Triaging and working a ticket

Opened the **"Unable to login - password expired"** ticket from Mike Johnson and triaged it like a real help desk agent would: raised priority to High, transferred to the IT Support department, applied the SEV-2 SLA, and assigned it to agent John Smith.

![Ticket triaged](screenshots/ticket_triaged.png)

### 13. Responding to the ticket

Posted a reply to the user acknowledging the issue and setting expectations for resolution — building a full audit trail of every action taken on the ticket, including priority changes, department transfers, SLA updates, and assignment.

![Ticket reply and audit trail](screenshots/ticket_reply.png)

### 14. Resolving tickets

Worked through all three submitted tickets — password reset, network connectivity, and software installation — replying to each user with a resolution and marking the tickets as **Resolved**.

![Password reset ticket resolved](screenshots/ticket_resolved.png)
![Network connectivity ticket resolved](screenshots/ticket_resolved_network.png)
![Software installation ticket resolved](screenshots/ticket_resolved_software.png)

### 15. Closed ticket queue

All three tickets completed and closed the same day, each showing the closing agent and timestamp — a clean record of a full support cycle from submission to resolution.

![Closed tickets](screenshots/closed_tickets.png)

## Key takeaways

This project covers the day-to-day reality of a help desk role: standing up the tools IT teams rely on, organizing tickets by department and priority, and working through real support scenarios from intake to resolution. Combined with the Combined with the [Active Directory home lab](https://github.com/Ghummun/active-directory-home-lab), this project..., this project demonstrates both sides of help desk work — managing the directory and accounts users depend on, and managing the support requests that come in when something goes wrong.

## Tools used

- Microsoft Azure (Free Tier)
- Ubuntu Server 24.04 LTS
- Apache, MySQL, PHP (LAMP stack)
- osTicket v1.18.1
- SSH / PowerShell
