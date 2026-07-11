# LAB 11 — SharePoint Online Administration

## Product: SharePoint Online (SPO)

---

## 📘 Lab Overview

This lab provides hands-on experience with **SharePoint Online administration** using the SharePoint Admin Center and PowerShell.

The lab covers SharePoint site creation, permission management, storage administration, information management policies, and monitoring SharePoint health and usage.

---

# 🎯 Lab Objectives

By completing this lab, you will learn how to:

* ✅ Create and manage SharePoint Sites
* ✅ Configure permissions and site sharing
* ✅ Manage site storage and quotas
* ✅ Apply Information Management Policies
* ✅ Monitor SharePoint health and usage

---

# 🌐 Step 1: Access SharePoint Admin Center

## Access SharePoint Administration Portal

Navigate to:

```text id="a8f5kc"
https://admin.microsoft.com → Admin Centers → SharePoint
```

---

## Direct Access

You can also access SharePoint Admin Center directly:

```text id="p3v7nm"
https://<tenant>-admin.sharepoint.com
```

---

# 📂 Step 2: Create a SharePoint Site

## Create New Site

Navigate to:

```text id="x7m4qb"
Sites → Active Sites → Create
```

---

## Select Site Type

Choose the appropriate site type:

| Site Type          | Purpose                                              |
| ------------------ | ---------------------------------------------------- |
| Team Site          | Connected to a Microsoft 365 Group for collaboration |
| Communication Site | Used for intranet publishing and information sharing |

---

## Configure Site Details

Enter:

* Site name
* Owner
* Language
* Privacy settings

For Team Sites:

* Private
* Public

---

## Provision Site

Click:

```text id="k9q2wm"
Finish
```

The site is provisioned within seconds.

---

## PowerShell — Create a SharePoint Site

```powershell id="r5n8vx"
Connect-SPOService -Url https://tenant-admin.sharepoint.com

New-SPOSite `
-Url https://tenant.sharepoint.com/sites/newsite `
-Owner admin@domain.com `
-StorageQuota 1024 `
-Template STS#3 `
-Title 'New Team Site'
```

---

# 🔐 Step 3: Manage Permissions

## Access Site Permissions

Open the SharePoint site:

Navigate to:

```text id="m8x4qv"
Settings (gear icon) → Site Permissions
```

---

## Default SharePoint Groups

SharePoint uses three default permission groups:

| Group    | Permission Level |
| -------- | ---------------- |
| Owners   | Full Control     |
| Members  | Edit             |
| Visitors | Read             |

---

## Add Users to Site

Steps:

1. Open:

```text id="w6p2kt"
Site Permissions
```

2. Select:

```text id="c4m8zy"
Share site
```

3. Enter user email address.
4. Select the required permission level.

---

## External Sharing Configuration

Verify that:

* The site's sharing level allows external guests.
* Tenant sharing settings permit external access.

> **Note**
> Site sharing settings inherit from tenant configuration but can be restricted further at the site level.

---

## Break Permission Inheritance

For a document library or list:

Navigate to:

```text id="q7v5mk"
Library settings → Permissions → Stop Inheriting Permissions
```

---

> ⚠️ **Warning**
> Breaking permission inheritance at the document level creates management complexity. Use site-level or library-level permission scoping whenever possible.

---

# 💾 Step 4: Storage and Quota Management

## Manage Site Storage

Navigate to:

```text id="z4n8px"
SharePoint Admin Center → Sites → Active Sites
```

---

## Adjust Storage Settings

1. Select the site.

2. Open:

   ```
   Storage column
   ```

   or:

   ```
   Site properties
   ```

3. Adjust the storage limit.

---

## Configure Site-Specific Quota

Navigate to:

```text id="b7m3qa"
Edit → Storage → Set maximum storage
```

---

## PowerShell — Set Site Storage Quota

```powershell id="t9k5wy"
Set-SPOSite `
-Identity https://tenant.sharepoint.com/sites/mysite `
-StorageQuota 5120 `
-StorageQuotaWarningLevel 4608
```

---

# 📑 Step 5: Information Management Policies

## Configure Content Management Policies

Navigate to:

```text id="n3q8vx"
Site Collection → Site Settings → Site Collection Administration → Content Type Policy Templates
```

---

## Apply Retention Policies

Configure retention using Microsoft Purview:

```text id="v5m7kp"
Microsoft Purview → Data Lifecycle Management → Retention Policies → Add SharePoint locations
```

---

## Apply Sensitivity Labels

Navigate to:

```text id="h8q4mz"
Site Settings → Site Information → Sensitivity Label
```

---

## Sensitivity Label Controls

Sensitivity labels can control:

* External sharing
* Conditional Access
* Default DLP policy for the site

---

# 📊 Step 6: Monitor SharePoint Health and Usage

## SharePoint Usage Reports

Navigate to:

```text id="s6m2qw"
SharePoint Admin Center → Reports → Usage
```

Review:

* Active sites
* Files
* Page views

---

## Tenant-Wide SharePoint Reports

Navigate to:

```text id="j4p8nx"
Microsoft 365 Admin Center → Reports → Usage → SharePoint
```

---

## Site Health Monitoring

Navigate to:

```text id="c9v5mk"
SharePoint Admin Center → Health → Site Health
```

Review:

* Site issues
* Performance concerns
* Configuration warnings

---

## PowerShell — Get All Sites with Storage Usage

```powershell id="f7m3qy"
Get-SPOSite -Limit All |
Select Url,StorageUsageCurrent,StorageQuota |
Sort StorageUsageCurrent -Desc
```

---

> 💡 **Best Practice / Tip**
> Sites using more than **80% of their storage quota** should be reviewed and cleaned up or expanded proactively.

---

# ⭐ Best Practices & Pro Tips

* 🏢 Use **Hub Sites** to connect related SharePoint sites and apply consistent navigation and branding.

* 🔐 Avoid granting users **Site Collection Administrator** permissions unless required. Use Members (Edit) permissions by default.

* 🏷️ Enable **Sensitivity Labels** on SharePoint sites for automatic DLP and sharing policy enforcement.

* 🔍 Perform a quarterly SharePoint permissions audit.

  Use:

  * SharePoint Migration Tool scanning features
  * PnP PowerShell

* ♻️ Implement SharePoint site lifecycle management:

  Recommended approach:

  * Archive inactive sites after 180 days
  * Delete sites after 365 days with approval

* 📚 Use **SharePoint Syntex** or document libraries with **Retention Labels** to automatically classify and retain compliance documents.

---
