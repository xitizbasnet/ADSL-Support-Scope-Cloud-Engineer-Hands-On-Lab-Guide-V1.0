# LAB 5 — Microsoft OneDrive Policy Management

## Product: SharePoint Admin Center / OneDrive

---

## 📘 Lab Overview

This lab provides hands-on experience with **Microsoft OneDrive policy management** using the **SharePoint Admin Center** and OneDrive administrative settings.

The lab focuses on configuring OneDrive sharing controls, synchronization policies, storage management, and Known Folder Move (KFM) to improve data protection and user productivity.

---

# 🎯 Lab Objectives

By completing this lab, you will learn how to:

* ✅ Configure OneDrive sharing and sync policies
* ✅ Control external sharing at the tenant level
* ✅ Set storage quotas
* ✅ Manage Known Folder Move (KFM)

---

# 🌐 Step 1: Access OneDrive Admin Settings

## Access SharePoint Admin Center

Navigate to:

```text id="8d8j5s"
https://admin.microsoft.com → Admin Centers → SharePoint
```

---

## Configure OneDrive-Specific Settings

In the SharePoint Admin Center:

Navigate to:

```text id="m9k8rt"
Policies → Sharing
```

Configure:

* OneDrive sharing controls
* SharePoint sharing controls

For OneDrive-specific configuration:

Navigate to:

```text id="zq7v6p"
Settings → OneDrive
```

---

# 🔗 Step 2: Sharing Policies

## Configure Sharing Controls

Navigate to:

```text id="7k8q2m"
Policies → Sharing
```

Configure the following settings:

---

## External Sharing Level for OneDrive

Available options:

| Setting                 | Description                              |
| ----------------------- | ---------------------------------------- |
| Anyone                  | Allows anonymous access links            |
| New and existing guests | Allows new and existing guest users      |
| Existing guests         | Allows only previously added guests      |
| Only people in your org | Restricts sharing to internal users only |

---

## Default Sharing Link Type

Configure default link behavior:

* Specific people
* Only people in your organization
* Anyone with the link

---

## Default Link Permissions

Configure default permissions:

* View
* Edit

---

## Advanced Sharing Settings

Configure:

* Require sign-in
* Expiration days for guest links
* Domain allow/block list

---

> ⚠️ **Warning**
> Set external sharing to **"Existing guests only"** or **"Only people in your org"** for regulated industries.

---

# 🔄 Step 3: Sync Client Policies

## Configure OneDrive Synchronization Settings

Navigate to:

```text id="a1l2sd"
Settings → Sync
```

---

## Restrict Sync to Domain-Joined PCs

Configure:

* Allow syncing only on PCs joined to specific domains.
* Enter the required domain GUIDs.

---

## Block Specific File Types

Prevent synchronization of risky file types.

Example:

```text
.exe
.bat
```

Enter file extensions in the blocked files list.

---

## Manage OneDrive Policies

Manage OneDrive policies using:

* Microsoft Intune
* Group Policy

Deploy:

```
OneDrive ADM/ADMX templates
```

---

## Registry Key — Enable Silent Sign-In

Configure the following registry setting:

```text id="3v9c7k"
HKLM\SOFTWARE\Policies\Microsoft\OneDrive
```

Set:

```text id="s0x8tj"
SilentAccountConfig = 1 (DWORD)
```

---

# 💾 Step 4: Storage Quota Management

## Configure Default OneDrive Storage

Navigate to:

```text id="q8p6za"
SharePoint Admin Center → Settings → Storage limit
```

Configure the default OneDrive storage allocation per user.

---

## Configure Individual User Storage Quota

Navigate to:

```text id="w4g7yc"
SharePoint Admin Center → More features → User Profiles → Manage User Profiles
```

Steps:

1. Find the user.

2. Select:

   ```
   Edit
   ```

3. Configure:

   ```
   Disk Quota
   ```

---

## PowerShell — Set User OneDrive Quota

```powershell id="v4x0sq"
Set-SPOSite `
-Identity https://tenant-my.sharepoint.com/personal/user_domain_com `
-StorageQuota 102400
```

---

# 📂 Step 5: Known Folder Move (KFM) — Backup Desktop/Documents/Pictures

## Configure Known Folder Move

Configure KFM using:

* Microsoft Intune
* Group Policy
* Group Policy Object (GPO)

---

## Policy Path

Navigate to:

```text id="m1y6kp"
User Configuration → Administrative Templates → OneDrive → Silently move Windows known folders to OneDrive
```

---

## Enable KFM Policy

Configure:

1. Set the Tenant ID value.
2. Enable the policy.

---

## KFM Functionality

This ensures the following folders are automatically backed up to OneDrive:

* Desktop
* Documents
* Pictures

---

> 💡 **Best Practice / Tip**
> KFM is one of the highest-impact data protection features. It enables seamless PC replacement without data loss.

---

# ⭐ Best Practices & Pro Tips

* 🛡️ Enable **Known Folder Move (KFM)** for all users. It is one of the most impactful OneDrive data protection features.

* ⏳ Set external sharing expiration dates.

  Example:

  ```
  30 days
  ```

  This prevents stale sharing links.

* 🚫 Block risky file types from syncing to OneDrive:

  ```
  .exe
  .bat
  .cmd
  .ps1
  ```

  These file types present security risks when synchronized to personal devices.

* 🔐 Use **Conditional Access** to restrict OneDrive access from:

  * Unmanaged devices
  * Non-compliant devices

* 📊 Monitor sharing activity reports:

```text id="8o9j7c"
SharePoint Admin Center → Reports → Sharing activity
```

---

