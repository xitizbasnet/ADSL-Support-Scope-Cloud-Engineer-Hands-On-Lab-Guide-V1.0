# LAB 3 — Microsoft Teams Policy Management

## Product: Teams Admin Center

---

## 📘 Lab Overview

This lab provides hands-on experience with **Microsoft Teams administration** using the **Teams Admin Center** and PowerShell.

The lab focuses on configuring Teams policies that control meetings, messaging, applications, guest access, and external collaboration settings.

---

# 🎯 Lab Objectives

By completing this lab, you will learn how to:

* ✅ Create and assign Teams Meeting Policies
* ✅ Configure Messaging and App Permission Policies
* ✅ Manage Teams Calling Policies
* ✅ Set up Guest Access and External Access Policies

---

# 🌐 Step 1: Access Teams Admin Center

## Access Portal

Navigate to:

```text
https://admin.teams.microsoft.com
```

Alternatively, access Teams Admin Center from the Microsoft 365 Admin Center:

```text
M365 Admin Center → Admin Centers → Teams
```

After authentication, you will land on the **Teams Admin Center dashboard**.

---

# 🎥 Step 2: Meeting Policies

## Create a Meeting Policy

Navigate to:

```text
Meetings → Meeting Policies → Add
```

---

## Configure Meeting Settings

Configure the following options:

* Allow cloud recording
* Allow transcription
* Who can present
* Allow meeting chat
* Lobby bypass settings

---

## Assign Meeting Policy to Users

Steps:

1. Select the policy.

2. Choose:

   ```
   Manage users
   ```

3. Search for users.

4. Assign the policy.

---

## PowerShell — Create Meeting Policy

```powershell
New-CsTeamsMeetingPolicy `
-Identity 'RestrictedMeeting' `
-AllowCloudRecording $false `
-AllowTranscription $false
```

---

## PowerShell — Assign Meeting Policy

```powershell
Grant-CsTeamsMeetingPolicy `
-Identity user@domain.com `
-PolicyName 'RestrictedMeeting'
```

---

# 💬 Step 3: Messaging Policies

## Create Messaging Policy

Navigate to:

```text
Messaging Policies → Add
```

---

## Configure Messaging Features

Configure the following options:

* Allow Giphy
* Allow memes
* Allow stickers
* Allow URL previews
* Allow read receipts
* Priority notifications

---

## Assign Messaging Policies

Assign policies to specific user groups.

Example:

* Apply stricter messaging policies to regulated departments.

---

# 📱 Step 4: App Permission Policies

## Configure App Permissions

Navigate to:

```text
Teams Apps → Permission Policies → Add
```

---

## Configure Application Access

Define which applications users can install:

* Microsoft applications
* Third-party applications
* Custom applications

---

## Compliance-Based Application Restrictions

For compliance-sensitive roles:

1. Set third-party apps to:

   ```
   Block specific apps and allow all others
   ```

2. Block required applications according to organizational policy.

---

## PowerShell — Block a Specific Teams App

```powershell
New-CsTeamsAppPermissionPolicy `
-Identity 'BlockedApps' `
-DefaultCatalogApps Allow `
-PrivateCatalogApps Allow `
-GlobalCatalogApps Disallow
```

---

# 🌍 Step 5: Guest Access & External Access

## Configure Guest Access

Navigate to:

```text
Users → Guest Access
```

Enable:

```text
Allow guest access in Teams → On
```

---

## Configure Guest Permissions

Review and configure:

* Meetings
* Calling
* Messaging

---

## Configure External Access

Navigate to:

```text
Users → External Access
```

Configure federation with specific domains.

---

> ⚠️ **Warning**
> Guest users inherit tenant-wide settings but can be further restricted through meeting policies.

---

# ⭐ Best Practices & Pro Tips

* 🏢 Use the **Global (Org-wide default) policy** as a baseline and create restricted policies for specific user groups.

* 🎥 Disable **cloud recording** by default. Enable it only for teams or roles that legitimately require recording capabilities.

* 📊 Audit Teams usage regularly through:

```text
Teams Admin Center → Analytics & Reports → Usage Reports
```

* 🔐 Enable **Information Barriers** if your organization requires regulatory separation.

  Example:

  ```
  Finance department separation requirements
  ```

* 🌐 Review external access domains quarterly and remove stale federated domains.

---

