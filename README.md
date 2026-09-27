# IT Support & Systems Administration Labs

A hands-on IT homelab built to develop practical experience with **Windows Server, Active Directory, networking, PowerShell, IIS, authentication, VMware, and troubleshooting**.

The goal of this lab is to reproduce common IT Support and Systems Administration scenarios in a controlled environment and document the troubleshooting process.

---

## Lab Environment

```text
Windows 11 Host
       │
       │ VMware
       ▼
┌─────────────────────────────┐
│ Windows Server              │
│                             │
│ Active Directory            │
│ Domain: telugu.local        │
│ DNS                         │
│ IIS / SWAuth                │
│ PowerShell                  │
└──────────────┬──────────────┘
               │
               │ Domain / Network
               ▼
        Windows Client
```

### Core Environment

| Component        | Purpose                            |
| ---------------- | ---------------------------------- |
| VMware           | Virtualization platform            |
| Windows Server   | Server and domain infrastructure   |
| Active Directory | Identity and user management       |
| DNS              | Domain name resolution             |
| IIS              | Web server and authentication      |
| PowerShell       | Administration and troubleshooting |
| Windows Client   | Domain/user testing                |

---

# Lab 01 — Active Directory

## Objective

Build a Windows Server domain environment and practice common Active Directory administration tasks.

### Configuration

```text
Domain:
telugu.local

NetBIOS:
TELUGU
```

### Tasks

* Installed Active Directory Domain Services
* Created a new forest and domain
* Configured the domain controller
* Created domain users
* Configured user attributes
* Tested domain authentication
* Managed user passwords
* Tested domain logon
* Troubleshot user authentication issues

### Useful Commands

Check the current user:

```powershell
whoami
```

Check the current Windows identity:

```powershell
[System.Security.Principal.WindowsIdentity]::GetCurrent().Name
```

Check the domain:

```powershell
Get-ADDomain
```

Check a user's details:

```powershell
Get-ADUser username -Properties *
```

List users:

```powershell
Get-ADUser -Filter *
```

Check the domain controller:

```powershell
nltest /dsgetdc:telugu.local
```

---

# Lab 02 — User & Account Management

## Objective

Practice managing users and troubleshooting account-related issues.

### Tasks

* Create AD users
* Verify usernames
* Configure UPN
* Reset passwords
* Check account status
* Check group membership
* Test authentication
* Troubleshoot domain logon problems

### Check a User

```powershell
Get-ADUser sreddy -Properties UserPrincipalName,Enabled
```

### Reset a Password

```powershell
Set-ADAccountPassword sreddy -Reset `
-NewPassword (Read-Host "Enter New Password" -AsSecureString)
```

### Unlock an Account

```powershell
Unlock-ADAccount sreddy
```

### Enable an Account

```powershell
Enable-ADAccount sreddy
```

### Check Group Membership

```powershell
Get-ADPrincipalGroupMembership sreddy |
Select-Object Name
```

---

# Lab 03 — Windows Server & IIS

## Objective

Configure IIS and troubleshoot Windows web services.

### Tasks

* Installed IIS
* Configured a website/application
* Enabled Windows Authentication
* Tested local web access
* Tested access using the server IP
* Restarted IIS services
* Investigated HTTP errors

### Useful Commands

Check IIS service:

```powershell
Get-Service W3SVC
```

Restart IIS:

```powershell
iisreset
```

Test a local endpoint:

```powershell
curl.exe -I http://localhost/SWAuth
```

Test using the server IP:

```powershell
curl.exe -I http://192.168.11.143/SWAuth
```

---

# Lab 04 — Authentication & SWAuth

## Objective

Understand how a web application can use Active Directory for authentication.

### Lab Flow

```text
User
 │
 ▼
Spiceworks Web
 │
 ▼
SWAuth
 │
 ▼
Windows Authentication
 │
 ▼
Active Directory
 │
 ▼
TELUGU\username
```

### Configuration

```text
AD Domain:
telugu.local

NetBIOS:
TELUGU

SWAuth:
http://192.168.11.143/SWAuth
```

### Troubleshooting Performed

During the lab, authentication issues were investigated involving:

* Incorrect username/password
* AD user attributes
* `userPrincipalName`
* Windows Authentication
* IIS configuration
* HTTP `401`
* HTTP `500`
* HTTP `503`
* ASP.NET errors
* IIS service status
* Network connectivity

This provided practical experience tracing an authentication problem from the **web layer → IIS → authentication handler → Active Directory**.

---

# Lab 05 — Network Troubleshooting

## Objective

Practice diagnosing connectivity problems between the host, virtual machine, server, and web services.

### Tests

Ping the server:

```powershell
ping 192.168.11.143
```

Test HTTP port:

```powershell
Test-NetConnection 192.168.11.143 -Port 80
```

Check IP configuration:

```powershell
ipconfig
```

Check DNS configuration:

```powershell
ipconfig /all
```

### Troubleshooting Approach

```text
Is the VM running?
       ↓
Is the IP correct?
       ↓
Can the host ping the VM?
       ↓
Is TCP port 80 reachable?
       ↓
Is IIS running?
       ↓
Is the application responding?
       ↓
Is authentication working?
```

---

# Lab 06 — PowerShell Administration

PowerShell is used throughout the lab for administration, verification, and troubleshooting.

### Common Commands

```powershell
whoami
```

```powershell
hostname
```

```powershell
ipconfig
```

```powershell
Get-ComputerInfo
```

```powershell
Get-Service
```

```powershell
Get-ADDomain
```

```powershell
Get-ADUser
```

```powershell
Get-ADGroup
```

```powershell
Test-NetConnection
```

```powershell
iisreset
```

---

# Troubleshooting Method

The lab follows a structured troubleshooting approach rather than applying random fixes.

```text
1. Identify
      ↓
2. Reproduce
      ↓
3. Gather information
      ↓
4. Isolate the problem
      ↓
5. Test a possible cause
      ↓
6. Apply the fix
      ↓
7. Verify the result
      ↓
8. Document the solution
```

---

# What These Labs Demonstrate

These labs provide hands-on practice with:

* Windows administration
* Active Directory
* User and account management
* Domain authentication
* Windows Server
* IIS
* PowerShell
* DNS
* TCP/IP
* VMware
* Network troubleshooting
* Authentication troubleshooting
* Service troubleshooting
* Structured problem solving

---

# Lab Philosophy

The objective is not just to make a service work.

Each issue is treated as a troubleshooting exercise:

**Observe → Investigate → Test → Fix → Verify → Document**

This approach helps build practical skills applicable to **IT Support, Desktop Support, Technical Support, Service Desk, and Junior System Administration** roles.

---

## Current Lab Status

```text
[✓] VMware environment
[✓] Windows Server
[✓] Active Directory
[✓] Domain configuration
[✓] User management
[✓] PowerShell administration
[✓] IIS
[✓] Windows Authentication
[✓] SWAuth integration
[✓] Network troubleshooting
[✓] Authentication troubleshooting
[ ] Expand client/server scenarios
[ ] Add additional troubleshooting cases
```

---

<p align="center">

**IT Support Homelab**

**Build → Troubleshoot → Verify → Document**

</p>
