# LAB 7 — Microsoft Entra ID (Azure AD) Administration

## Product: Microsoft Entra ID (Azure Active Directory)

---

## 📘 Lab Overview

This lab provides hands-on experience with **Microsoft Entra ID identity and access management**.

The lab covers configuring Conditional Access policies, enforcing Multi-Factor Authentication (MFA), implementing Self-Service Password Reset (SSPR), configuring Single Sign-On (SSO), and managing hybrid identity synchronization using Microsoft Entra Connect.

---

# 🎯 Lab Objectives

By completing this lab, you will learn how to:

* ✅ Configure Conditional Access Policies
* ✅ Enable and enforce MFA
* ✅ Configure Self-Service Password Reset (SSPR)
* ✅ Set up Single Sign-On (SSO) for applications
* ✅ Manage Identity and Directory Sync (Entra Connect)

---

# 🌐 Step 1: Access Microsoft Entra Admin Center

## Access Portal

Navigate to:

```text id="9qz1rm"
https://entra.microsoft.com
```

Alternative portal:

```text id="2xw8nv"
https://aad.portal.azure.com
```

Sign in using:

* Global Administrator credentials

---

# 🛡️ Step 2: Conditional Access Policy

## Create Conditional Access Policy

Navigate to:

```text id="c1m7ps"
Protection → Conditional Access → Policies → New Policy
```

---

## Configure Policy Details

Example policy name:

```text
Require MFA for All Users
```

---

## Configure Assignments

### Users

Select:

* All users

or:

* Specific groups

---

### Cloud Apps

Select:

* All cloud apps

or:

* Specific applications

---

## Configure Conditions

Configure optional conditions:

* Device platform
* Locations
* Sign-in risk

---

## Configure Access Controls

Navigate to:

```text id="w5k8yu"
Access Controls → Grant
```

Select:

```text
Require multi-factor authentication
```

Click:

```text
Select
```

---

## Enable Policy

Recommended deployment process:

1. Set policy to:

   ```
   Report-only
   ```

2. Review impact.

3. Enable:

   ```
   On
   ```

---

> ⚠️ **Warning**
> Always exclude at least one break-glass account from Conditional Access policies to avoid accidental tenant lockout.

---

# 🔐 Step 3: Enable and Enforce MFA

## Method 1 — Security Defaults (Basic)

Navigate to:

```text id="j4w0xy"
Entra Admin → Overview → Properties → Manage security defaults
```

Enable:

```text
Security Defaults
```

---

## Method 2 — Per-User MFA

Navigate to:

```text id="r5g8nm"
Entra Admin → Users → Per-user MFA
```

Enable MFA for individual users.

---

## Method 3 — Conditional Access (Recommended)

Use the Conditional Access policy created in Step 2.

Conditional Access provides more flexibility and is recommended for enterprise environments.

---

## Enable Microsoft Authenticator

Navigate to:

```text id="v8k2mt"
Protection → Authentication Methods → Microsoft Authenticator
```

Enable:

```text
Microsoft Authenticator
```

---

## PowerShell — Check MFA Status for All Users

```powershell id="x5p7qd"
Get-MsolUser -All |
Select DisplayName,StrongAuthenticationRequirements |
Export-Csv mfa_status.csv
```

---

> 💡 **Best Practice / Tip**
> Conditional Access MFA is significantly more flexible than per-user MFA. Prefer Conditional Access for enterprise deployments.

---

# 🔑 Step 4: Self-Service Password Reset (SSPR)

## Configure SSPR

Navigate to:

```text id="m2z6pv"
Protection → Password Reset
```

---

## Enable SSPR

Choose:

* Selected (pilot group)
* All users

---

## Configure Authentication Methods

Require two authentication methods:

Options:

* Mobile app notification
* Email
* Mobile phone
* Security questions

---

## Registration Settings

Configure:

* Require users to register on next sign-in
* Set re-confirmation period

Example:

```text
180 days
```

---

## Notification Settings

Enable notifications:

* Notify users after password reset
* Notify administrators after password reset

---

## On-Premises Writeback

Enable password writeback when using a hybrid environment.

Requirement:

```text
Microsoft Entra Connect
```

---

# 🔗 Step 5: Single Sign-On (SSO) for Applications

## Add Enterprise Application

Navigate to:

```text id="p6n8wz"
Applications → Enterprise Applications → New Application
```

---

## Add Application

Options:

* Search application gallery

Examples:

* Salesforce
* ServiceNow

or:

* Add a custom application

---

## Configure SSO

Inside the application:

Navigate to:

```text id="d8q4kw"
Single Sign-On → SAML
```

---

## Configure SAML Settings

Configure:

* Entity ID
* Reply URL (ACS URL)

Obtain these values from the application's SSO documentation.

---

## Federation Metadata

Steps:

1. Download Federation Metadata XML.
2. Upload the XML file to the application.

---

## Assign Users and Groups

Assign required:

* Users
* Security groups

---

## Test SSO

Use:

```text id="n3r7xp"
Test this application
```

button in the SSO configuration.

---

# 🔄 Step 6: Directory Sync — Microsoft Entra Connect

## Install Entra Connect

Install Microsoft Entra Connect on:

```text
Member Server
```

> ⚠️ Do not install Entra Connect on a Domain Controller.

---

## Download Microsoft Entra Connect

Download from:

```text
https://www.microsoft.com/en-us/download/details.aspx?id=47594
```

---

## Run Setup Wizard

Choose:

### Express Settings

For:

* Simple deployments

### Custom Settings

For:

* Advanced deployments
* OU selection
* Attribute filtering

---

## Authentication Requirements

Sign in using:

Cloud:

```text
Global Administrator
```

On-premises:

```text
Enterprise Administrator
```

---

## Select Synchronization Method

Choose one:

* Password Hash Sync (PHS)
* Pass-through Authentication (PTA)
* Federation (ADFS)

---

## Verify Synchronization

After synchronization:

1. Open Entra Admin Center.
2. Confirm users appear with:

```text
Synced from on-premises
```

---

## PowerShell — Force Delta Sync

```powershell id="z8n4vk"
Start-ADSyncSyncCycle -PolicyType Delta
```

---

## PowerShell — Force Full Sync

```powershell id="h7m2qs"
Start-ADSyncSyncCycle -PolicyType Initial
```

---

> ⚠️ **Warning**
> Do not sync service accounts, administrator accounts, or honeypot accounts to the cloud.

---

# ⭐ Best Practices & Pro Tips

* 🚨 Maintain at least two **Break-glass (emergency access) accounts** and exclude them from all Conditional Access policies.

* 🌍 Use **Named Locations** in Conditional Access to trust corporate IP ranges and block unexpected geographic sign-ins.

* 🛡️ Enable **Identity Protection risk-based Conditional Access** to automatically block risky sign-ins.

* 🧪 Audit Conditional Access policy impact using **Report-only mode** for at least 7 days before enabling production enforcement.

* 🚫 Never sync the on-premises built-in **Administrator account** to Microsoft Entra ID.

* 📅 Schedule monthly **Entra ID Access Reviews** to ensure application assignments remain current.

---

