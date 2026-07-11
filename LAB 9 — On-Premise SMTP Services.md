# LAB 9 — On-Premise SMTP Services

## Product: Windows SMTP / IIS SMTP / Postfix

---

## 📘 Lab Overview

This lab provides hands-on experience with configuring an **on-premises SMTP relay service** using Windows SMTP/IIS SMTP.

The lab covers installing SMTP services, configuring relay permissions, integrating with Exchange Online as a smart host, and testing SMTP mail flow.

---

# 🎯 Lab Objectives

By completing this lab, you will learn how to:

* ✅ Install and configure an SMTP relay server on Windows
* ✅ Configure relay restrictions and authentication
* ✅ Test SMTP mail flow
* ✅ Integrate with Exchange Online as a smart host

---

# ⚙️ Step 1: Install SMTP Feature on Windows Server

## Install SMTP Server Role

Open:

```text id="n8x5kp"
Server Manager → Manage → Add Roles and Features
```

---

## Installation Steps

1. Select:

   ```
   Role-based installation
   ```

2. Select the target server.

3. Under **Features**:

   Expand:

   ```
   SMTP Server
   ```

4. Select:

   ```
   Install
   ```

This installation includes:

```text id="h3q9mw"
IIS Management Console
```

---

## PowerShell Alternative

Install SMTP Server using PowerShell:

```powershell id="b8w4rt"
Install-WindowsFeature SMTP-Server -IncludeManagementTools
```

---

# 📮 Step 2: Configure IIS SMTP Server

## Open IIS SMTP Management Console

Open:

```text id="q6m2zs"
IIS 6.0 Manager
```

Access methods:

* Search for:

```text
inetmgr6
```

or:

* Administrative Tools

---

## Configure SMTP Virtual Server

Expand the server:

```text id="v7k1px"
SMTP Virtual Server #1
```

Right-click:

```text
Properties
```

---

## General Settings

Configure:

* IP Address:

  ```
  Server static IP address
  ```

* Port:

  ```
  25
  ```

---

## Configure Connection Restrictions

Navigate to:

```text id="m4z9cb"
Access tab → Connection
```

Allow only specific IP addresses:

* On-premises devices
* Applications requiring SMTP relay

---

## Configure Relay Restrictions

Navigate to:

```text id="j8r2nd"
Access tab → Relay
```

Add:

* Approved IP addresses
* Approved network subnets

---

## Configure Smart Host

Navigate to:

```text id="x5w7qp"
Delivery tab → Advanced
```

Configure:

* Smart host:

  * Exchange Online connector
  * ISP relay server

---

> ⚠️ **Warning**
> Never configure relay as **"All except the list below"**. This creates an open relay that can be exploited by spammers.

---

# ☁️ Step 3: Configure Exchange Online as Smart Host

## Create Exchange Online Connector

In Exchange Admin Center:

Navigate to:

```text id="c9m4vk"
Mail Flow → Connectors → New Connector
```

---

## Connector Configuration

Configure:

From:

```text
Your organization's email server
```

To:

```text
Office 365
```

---

## Configure SMTP Smart Host

In the SMTP server:

Navigate to:

```text id="p2w6js"
Delivery tab → Smart host
```

Set:

```text
.mail.protection.outlook.com
```

---

## Authentication Configuration

Configure:

* TLS authentication
* Certificate matching:

```text
*.outlook.com
```

---

## Test Relay

Send a test email from:

* Application
* Printer
* Scanner
* SMTP-enabled device

configured to use the SMTP relay server.

---

# 🧪 Step 4: Test SMTP Mail Flow with Telnet

## SMTP Connection Test

Open Command Prompt and run:

```text id="k9f4za"
telnet <SMTP Server> 25
```

---

## SMTP Commands

```text
EHLO testclient

MAIL FROM:<sender@example.com>

RCPT TO:<recipient@example.com>

DATA

Subject: SMTP Test

This is a test email.

.

QUIT
```

---

> 💡 **Best Practice / Tip**
> If Telnet is blocked, use the following PowerShell command:

```powershell id="w2q8mv"
Test-NetConnection -ComputerName <SMTP Server> -Port 25
```

---

# ⭐ Best Practices & Pro Tips

* 🔒 Lock SMTP relay permissions by IP range. Allow only approved devices such as:

  * Printers
  * Scanners
  * Application servers

* 🔐 Enable TLS encryption on all SMTP relay connections. Never send email traffic in plain text.

* 👤 Use a dedicated service account for SMTP authentication.

  Avoid using:

  * Personal accounts
  * Administrator accounts

* 📊 Monitor SMTP logs daily:

```text id="s7m3xc"
C:\Windows\System32\LogFiles\SMTPSVC1\
```

Use logs for:

* Relay abuse detection

* Troubleshooting

* Security monitoring

* ☁️ Consider migrating on-premises SMTP relay workloads to **Exchange Online Connectors**:

  * Direct Send
  * SMTP Relay

This reduces infrastructure maintenance requirements.

---

