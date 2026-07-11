# LAB 4 — Microsoft Intune (Endpoint Management)

## Product: Microsoft Intune / Microsoft Endpoint Manager (MEM)

---

## 📘 Lab Overview

This lab provides hands-on experience with **Microsoft Intune endpoint management** using the Intune Admin Center.

The lab covers device enrollment, application deployment, compliance policy configuration, device configuration profiles, and endpoint compliance support scenarios.

---

# 🎯 Lab Objectives

By completing this lab, you will learn how to:

* ✅ Enroll and manage devices (Windows, iOS, Android)
* ✅ Deploy applications to managed devices
* ✅ Create and assign Compliance Policies
* ✅ Configure Device Configuration Profiles
* ✅ Support endpoint compliance scenarios

---

# 🌐 Step 1: Access Intune Admin Center

## Access Portal

Navigate to:

```text
https://intune.microsoft.com
```

Sign in using:

* Intune Administrator credentials, or
* Global Administrator credentials

---

# 💻 Step 2: Device Enrollment — Windows Autopilot

## Configure Windows Autopilot Enrollment

Navigate to:

```text
Devices → Enroll devices → Windows enrollment → Windows Autopilot Deployment Profiles
```

---

## Upload Device Hardware Hash

1. Obtain the device hardware hash CSV file from:

   * Device vendor
   * OEM provider

2. Upload the CSV file into Intune.

---

## Create Autopilot Deployment Profile

Configure:

* Deployment mode:

  * User-driven

* Join type:

  * Azure AD Joined

* OOBE settings

---

## Assign Profile to Device Group

Assign the Autopilot profile to the appropriate device group.

---

## New Device Experience

On a new device:

1. Power on the device.
2. Connect to the internet.
3. Sign in using corporate credentials.

The device will automatically configure based on the assigned Autopilot profile.

---

> 💡 **Best Practice / Tip**
> For manual enrollment, use:

```text
Settings → Accounts → Access Work or School → Connect → Sign in with corporate UPN
```

---

# 📦 Step 3: Application Management

## Add Applications

Navigate to:

```text
Apps → All Apps → Add
```

---

## Supported Application Types

| Application Type     | Description                                 |
| -------------------- | ------------------------------------------- |
| Microsoft 365 Apps   | Microsoft 365 application suite             |
| Store App            | Windows, iOS, or Android store applications |
| Line-of-Business App | Custom MSI, IPA, or APK applications        |
| Web Link             | Browser-based application links             |

---

## Assign Applications

Steps:

1. Select the application.
2. Open:

```text
Properties → Assignments
```

3. Select:

```text
Add group
```

4. Choose deployment type:

* **Required** — Mandatory installation
* **Available** — Optional installation

---

## PowerShell — Check Installed Apps on a Device via Graph API

```powershell
Connect-MgGraph -Scopes 'DeviceManagementApps.Read.All'

Get-MgDeviceManagedDeviceDetectedApp -ManagedDeviceId
```

---

# 🔐 Step 4: Compliance Policies

## Create Compliance Policy

Navigate to:

```text
Devices → Compliance Policies → Create Policy
```

---

## Select Platform

Supported platforms:

* Windows 10/11
* iOS
* Android

---

## Configure Compliance Rules

Configure requirements such as:

* Require BitLocker
* Minimum OS version
* Require antivirus
* Password requirements

---

## Configure Non-Compliance Actions

Available actions:

* Send email notification
* Mark device as non-compliant after grace period
* Retire device

---

## Assign Policy

Assign compliance policies to:

* User groups
* Device groups

---

> ⚠️ **Warning**
> Test compliance policies in a pilot group before organization-wide rollout to avoid accidental device lockout.

---

# ⚙️ Step 5: Configuration Profiles

## Create Configuration Profile

Navigate to:

```text
Devices → Configuration Profiles → Create Profile
```

---

## Common Configuration Profiles

| Profile             | Purpose                             |
| ------------------- | ----------------------------------- |
| Wi-Fi Settings      | Configure wireless network access   |
| VPN Configuration   | Deploy VPN settings                 |
| Email Settings      | Configure corporate email profiles  |
| Endpoint Protection | Configure Windows Defender settings |
| Kiosk Mode          | Configure restricted device usage   |

---

## Assign Configuration Profile

Assign profiles to appropriate device groups.

---

## Monitor Profile Deployment

Navigate to:

```text
Devices → Configuration Profiles → Select Profile → Device and User Check-in Status
```

---

## Force Device Sync with Intune

### On Device

Navigate to:

```text
Start → Run → DeviceMgmt.msc → Sync
```

---

### PowerShell on Device

```powershell
Start-Process `
-FilePath 'C:\Windows\System32\deviceenroller.exe' `
-ArgumentList '/o /o'
```

---

# 🛠️ Step 6: Endpoint Compliance Support

## Check Device Compliance Status

Navigate to:

```text
Devices → All Devices → Select Device → Device Compliance
```

---

## Common Non-Compliance Reasons

Examples:

* BitLocker disabled
* Outdated operating system
* Missing antivirus protection
* Device not encrypted

---

## Remediation Steps

Assist users with:

* Enabling BitLocker
* Running Windows Update
* Configuring Microsoft Defender

---

## Available Remote Actions

Administrators can perform:

* Sync
* Restart
* Quick Scan
* Retire
* Wipe

---

> 💡 **Best Practice / Tip**
> Use **Remote Help (Intune add-on)** for live assisted support sessions on managed devices.

---

# ⭐ Best Practices & Pro Tips

* 👥 Always use **Azure AD Groups** (Dynamic Groups preferred) for policy assignments. Never assign policies directly to individuals.

* 🔍 Create a **"Non-compliant Devices" dynamic group** to track and remediate issues proactively.

* 🚀 Use **Autopilot for zero-touch provisioning**. It eliminates manual imaging completely.

* ⏳ Set a compliance grace period of **3–7 days** before enforcement to allow users time to self-remediate.

* 🔄 Enable **Windows Update Rings** in Intune to control operating system update deployment and prevent unexpected reboots.

* 🧹 Audit device inventory monthly. Retire stale or unmanaged devices to maintain a clean environment.

---

