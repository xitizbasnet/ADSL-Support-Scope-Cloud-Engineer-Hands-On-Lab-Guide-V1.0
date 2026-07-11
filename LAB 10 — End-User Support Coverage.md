# LAB 10 — End-User Support Coverage

## Product: Microsoft 365 / Microsoft Intune / Microsoft Entra ID

---

## 📘 Lab Overview

This lab provides hands-on guidance for **Microsoft 365 end-user support operations** using Microsoft Entra ID, Microsoft Intune, and Microsoft 365 administration tools.

The lab focuses on assisting users with MFA recovery, managing policy exceptions through proper governance processes, and troubleshooting endpoint enrollment and compliance issues.

---

# 🎯 Lab Objectives

By completing this lab, you will learn how to:

* ✅ Reset MFA for locked-out users
* ✅ Grant Policy Exceptions and document them
* ✅ Assist with Endpoint Compliance Enrollment

---

# 🔐 Step 1: MFA Reset for a Locked-Out User

## Reset MFA Registration

Navigate to:

```text id="4v8k2m"
Entra Admin Center → Users → All Users
```

---

## Locate User Account

1. Search for the affected user.
2. Select the user.
3. Navigate to:

```text id="n7c5xp"
Authentication Methods
```

---

## Require MFA Re-Registration

Select:

```text id="m5w2qy"
Require re-register multifactor authentication
```

Confirm the action.

---

## Remove Phone-Based MFA Method

Alternatively, for phone-based MFA:

1. Select the registered authentication method.
2. Click:

```text id="k8x4vz"
Delete
```

---

## User Registration Process

Instruct the user to:

1. Sign in.
2. Complete the MFA registration process.
3. Register a new authentication method.

---

## PowerShell — Reset MFA Registration

```powershell id="q3m9wy"
Reset-MsolStrongAuthenticationMethodByUpn `
-UserPrincipalName user@domain.com
```

---

> 💡 **Best Practice / Tip**
> For MFA reset requests, always verify the user's identity through an alternative channel before resetting MFA.
>
> Examples:
>
> * Manager verification
> * HR confirmation
> * Photo ID verification
>
> MFA resets are considered high-risk administrative actions.

---

# 📋 Step 2: Policy Exceptions

## Policy Exception Process

Policy exceptions must follow a formal **Change Management process**.

---

## Exception Request Workflow

1. User or manager submits a request through:

   * ServiceNow
   * Email

2. Administrator reviews the business justification.

3. Obtain approval from:

   * Security team
   * Compliance team

4. Administrator implements the exception.

   Example:

   ```
   Add user to Conditional Access exclusion group
   ```

5. Set an expiry date.

   > Exceptions should always be time-limited.

6. Document:

   * User
   * Policy
   * Reason
   * Approver
   * Expiry date

---

## Create Conditional Access Exception Group

Navigate to:

```text id="p6x3kr"
Entra → Groups → Create Security Group
```

Create group:

```text id="x9m4qa"
CA-Exclusion-PolicyName
```

Add approved users.

---

> ⚠️ **Warning**
> Never grant policy exceptions without documented approval. Uncontrolled exceptions create unaudited compliance gaps.

---

# 💻 Step 3: Endpoint Compliance Enrollment Support

## User Reports Device as "Not Compliant"

Common scenario:

* User opens Company Portal.
* Device status shows:

```text id="c7p2ms"
Not compliant
```

---

# 🔧 Troubleshooting Steps

## Step 1: Sync Device

Ask the user to:

1. Open:

```text id="a8w4nx"
Company Portal app
```

2. Select:

```text id="w2k7qp"
Sync device
```

---

## Step 2: Check Device Compliance Status

Navigate to:

```text id="g5m9vx"
Intune Admin Center → Devices → All Devices → Select Device → Device Compliance
```

---

## Step 3: Identify Compliance Failure Reason

Common reasons:

* BitLocker disabled
* Operating system outdated
* Microsoft Defender disabled

---

## Step 4: Guide User Remediation

Assist the user with:

### Enable BitLocker

Navigate to:

```text id="z6p4mj"
Settings → Update & Security → Device Encryption
```

---

### Update Windows

Run:

```text id="r8w2kn"
Windows Update
```

---

### Enable Defender

Verify:

```text id="y5v7qc"
Microsoft Defender
```

is enabled.

---

## Step 5: Re-evaluate Compliance

After remediation:

1. User syncs Company Portal again.
2. Compliance status is re-evaluated.

Expected timeframe:

```text id="m4q9px"
Within 15 minutes
```

---

# 🔄 Endpoint Re-Enrollment Support

For enrollment issues:

Navigate to:

```text id="t6k8vy"
Settings → Accounts → Access Work or School
```

Steps:

1. Remove old account.
2. Re-enroll the device.

---

## Check Intune Enrollment Status

Run on the device:

```cmd id="b9x3qw"
dsregcmd /status
```

---

## Verify Successful Enrollment

Confirm:

```text id="h4m8zn"
AzureAdJoined: YES
```

and:

```text id="v7q2km"
MDMUrl: https://enrollment.manage.microsoft.com
```

---

> 💡 **Best Practice / Tip**
> The values **AzureAdJoined: YES** and **MDMUrl: https://enrollment.manage.microsoft.com** confirm successful device enrollment.

---

# ⭐ Best Practices & Pro Tips

* 🔐 Create an **MFA Reset SOP** and share it with the helpdesk team.

  Standardize identity verification steps before performing any MFA reset.

* 📝 Log all policy exceptions in a dedicated register:

  Examples:

  * SharePoint list
  * ServiceNow

  Include:

  * Approval details
  * Expiry dates
  * Automated reminder notifications

* 📘 Create an **Intune troubleshooting runbook** covering the top 10 compliance failure reasons and remediation steps.

* 🖥️ Use **Intune Remote Help** for live desktop support on enrolled devices. It provides faster troubleshooting than phone-based guidance.

* 📧 Configure automated email notifications to users when their device becomes non-compliant.

---

