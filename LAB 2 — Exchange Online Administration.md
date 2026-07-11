# LAB 2 — Exchange Online Administration

## Product: Exchange Online / Exchange Admin Center (EAC) / PowerShell

---

## 📘 Lab Overview

This lab provides hands-on experience with **Exchange Online administration** using the Exchange Admin Center (EAC) and PowerShell.

The lab covers mailbox management, mail flow configuration, retention and compliance settings, email security controls, mailbox recovery, and reporting capabilities.

---

# 🎯 Lab Objectives

By completing this lab, you will learn how to:

* ✅ Manage Mailboxes — create, configure, and manage shared mailboxes
* ✅ Configure Mail Flow Rules (Transport Rules)
* ✅ Set Retention Policies and Archival
* ✅ Configure Journaling and Litigation Hold
* ✅ Apply Email Restrictions and Controls
* ✅ Perform Mailbox Recovery
* ✅ Generate Exchange Online Reports

---

# 🌐 Step 1: Access Exchange Admin Center (EAC)

## Access Exchange Online Administration Portal

Navigate to:

```text
https://admin.exchange.microsoft.com
```

Alternatively, access Exchange Admin Center from the Microsoft 365 Admin Center:

```text
Admin Centers → Exchange
```

After authentication, you will land on the **Exchange Online Admin Center dashboard**.

---

# 📬 Step 2: Mailbox Management

## Access Mailboxes

Navigate to:

```text
Recipients → Mailboxes
```

---

## Create a User Mailbox

To add a mailbox:

1. Click:

   ```
   Add a mailbox
   ```

2. Select:

   ```
   User mailbox
   ```

---

## Create a Shared Mailbox

Navigate to:

```text
Recipients → Mailboxes → Add → Shared mailbox
```

Configure:

* Shared mailbox name
* Alias
* Required members who need access

---

## Configure Mailbox Settings

1. Select the mailbox.
2. Open the **Mailbox** tab.

Configure settings including:

* Quota
* Forwarding
* Auto-reply
* MailTips

---

## PowerShell — Create Shared Mailbox

```powershell
New-Mailbox -Name 'Support Team' -Alias support -Shared

Add-MailboxPermission -Identity support `
-User user@domain.com `
-AccessRights FullAccess
```

> 💡 **Best Practice / Tip**
> Shared mailboxes under 50 GB do not need a license.

---

# 📮 Step 3: Mail Flow Rules (Transport Rules)

## Create a Mail Flow Rule

Navigate to:

```text
Mail Flow → Rules → Add a rule
```

---

## Common Mail Flow Rules

Examples:

* Append disclaimer to emails
* Block specific senders or domains
* Encrypt sensitive emails
* Route messages to specific connectors

---

## Configure Rule Conditions and Actions

Configure the following:

1. **Name**
2. **Apply rule if** (condition)
3. **Do the following** (action)
4. **Exceptions**
5. **Priority**

---

## PowerShell — Create Transport Rule to Add Disclaimer

```powershell
New-TransportRule -Name 'Add Disclaimer' `
-ApplyHtmlDisclaimerLocation Append `
-ApplyHtmlDisclaimerText 'Confidential' `
-SentToScope NotInOrganization
```

> ⚠️ **Warning**
> Set rule priority carefully. Rules execute in order:
>
> ```
> 0 = Highest priority
> ```

---

# 🗄️ Step 4: Retention Policies & Archival

## Configure Retention Policies

Navigate to:

```text
Microsoft Purview Compliance Portal → Data Lifecycle Management → Retention Policies
```

---

## Create a Retention Policy

1. Click:

   ```
   New retention policy
   ```

2. Provide a policy name.

3. Select locations:

   ```
   Exchange email → Mailboxes
   ```

4. Configure:

   * Retention period
     Example: 7 years for finance
   * Retention actions:

     * Retain
     * Delete
     * Retain and delete

---

## Enable Archive Mailbox

Navigate to:

```text
EAC → Recipients → Mailboxes → Select User → Others tab → Manage mailbox archive → Enable
```

---

## PowerShell — Enable Archive for All Mailboxes

```powershell
Get-Mailbox -Filter {ArchiveStatus -eq 'None'} | Enable-Mailbox -Archive
```

---

# ⚖️ Step 5: Journaling & Litigation Hold

## Configure Journaling

Navigate to:

```text
EAC → Mail Flow → Journal Rules → New journal rule
```

Configure:

* Scope:

  * Internal
  * External
  * Global

* Recipient

* Journal mailbox address

---

## Configure Litigation Hold

Navigate to:

```text
EAC → Recipients → Mailboxes → Select User → Others → Manage litigation hold → Enable
```

Configure:

* Hold duration:

  * Blank = Indefinite

* Add a note for legal context.

---

## PowerShell — Enable Litigation Hold

```powershell
Set-Mailbox -Identity user@domain.com `
-LitigationHoldEnabled $true `
-LitigationHoldDuration 2555
```

> 💡 **Best Practice / Tip**
> Litigation Hold preserves all mailbox items, including deleted items. It is required for legal and compliance scenarios.

---

# 🔒 Step 6: Email Restrictions & Controls

## Restrict Mailbox Senders

Restrict who can send **to** a mailbox:

Navigate to:

```text
EAC → Mailbox → Mailbox tab → Manage mail flow settings → Message delivery restrictions
```

---

## Configure Maximum Message Size

Navigate to:

```text
EAC → Mail Flow → Receive Connectors → Select Connector → Edit → Message size restrictions
```

---

## Block External Forwarding Tenant-Wide

Navigate to:

```text
Anti-spam outbound policy → Automatic forwarding rules → Off
```

---

## PowerShell — Block All External Auto-Forwarding

```powershell
Set-HostedOutboundSpamFilterPolicy `
-Identity Default `
-AutoForwardingMode Off
```

---

# ♻️ Step 7: Mailbox Recovery

## Recover Deleted Mailbox

Recovery period:

```text
Within 30 days
```

Steps:

1. Open:

   ```
   Microsoft 365 Admin Center → Active Users
   ```

2. Select:

   ```
   Add user
   ```

3. Create the same UPN.

The mailbox reconnects automatically.

---

## Recover Deleted Emails (User Level)

Navigate in Outlook:

```text
Deleted Items → Recover items recently removed from this folder
```

---

## Admin-Level Restore

Use:

```text
EAC → Search eDiscovery
```

or PowerShell:

```powershell
New-MailboxRestoreRequest
```

---

## PowerShell — Restore Deleted Mailbox Content

```powershell
New-MailboxRestoreRequest `
-SourceMailbox 'DeletedUser' `
-TargetMailbox admin@domain.com `
-AllowLegacyDNMismatch
```

---

# 📊 Step 8: Reporting

## View Exchange Reports

In EAC:

```text
Reports tab
```

Available reports include:

* Mail flow reports
* Spam detections
* Malware detections
* Top senders
* Top receivers

---

## Microsoft 365 Usage Reports

Navigate to:

```text
Microsoft 365 Admin Center → Reports → Usage → Email activity
```

---

## Export Reports

Steps:

1. Select report.

2. Click:

   ```
   Export
   ```

3. Download as:

   ```
   CSV
   ```

---

## PowerShell — Get Mailbox Statistics

```powershell
Get-MailboxStatistics -Identity user@domain.com | Select `
DisplayName,TotalItemSize,ItemCount
```

---

# ⭐ Best Practices & Pro Tips

* 🧪 Always test transport rules with a **"Notify sender"** action before enforcing a block to avoid business disruption.

* 📦 Enable **Auto-Expanding Archive** for mailboxes projected to exceed 100 GB.

* 🏷️ Use **Retention Labels** instead of folder-based organization for scalable compliance.

* 📜 Journal only what is legally required. Journaling every message generates significant storage costs.

* 🔍 Enable Audit Logging for all mailboxes:

```powershell
Set-Mailbox -Identity * -AuditEnabled $true
```

* 📨 Review the mail flow message trace:

```text
EAC → Mail Flow → Message Trace
```

Use Message Trace as the first troubleshooting step for email delivery issues.

---


