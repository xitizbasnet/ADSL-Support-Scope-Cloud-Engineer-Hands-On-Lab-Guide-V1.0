# LAB 8 — Microsoft eDiscovery

## Product: Microsoft Purview eDiscovery

---

## 📘 Lab Overview

This lab provides hands-on experience with **Microsoft Purview eDiscovery** for legal discovery, investigation, and compliance activities.

The lab covers creating eDiscovery cases, applying legal holds, performing content searches, and exporting discovery results for legal review.

---

# 🎯 Lab Objectives

By completing this lab, you will learn how to:

* ✅ Create an eDiscovery case
* ✅ Place custodians on Legal Hold
* ✅ Run content searches
* ✅ Export search results for legal review

---

# 🔎 Step 1: Access eDiscovery in Microsoft Purview

## Access Portal

Navigate to:

```text id="6t4zpw"
https://compliance.microsoft.com
```

Navigate to:

```text id="q8m1dc"
eDiscovery → Premium (or Standard)
```

---

## eDiscovery Versions

| Version             | Features                                              |
| ------------------- | ----------------------------------------------------- |
| eDiscovery Standard | Search and export capabilities                        |
| eDiscovery Premium  | Adds custodian management, review sets, and analytics |

---

# 📁 Step 2: Create an eDiscovery Case

## Create Case

1. Click:

```text id="r5j8nx"
Create a case
```

2. Enter:

* Case name
* Description
* Reference number

---

## Add Case Members

Add additional administrators who require access to the case.

---

## Open Case

Open the newly created case to begin configuration.

---

# ⚖️ Step 3: Place a Legal Hold

## Create Legal Hold

Inside the case:

Navigate to:

```text id="p7c2mv"
Hold → Create Hold
```

---

## Configure Hold Settings

Define:

### Hold Name

Provide a descriptive name for the legal hold.

---

### Select Custodians

Select the users, mailboxes, or sites that require preservation.

Examples:

* User mailboxes
* SharePoint sites
* OneDrive locations
* Teams content

---

### Define Hold Scope

Choose:

* All content

or

* Query-based hold:

  * Keywords
  * Date range
  * Specific criteria

---

## Activate Hold

After activation:

* Affected content is preserved.
* Content remains available even if deleted by the user.

---

> 💡 **Best Practice / Tip**
> Legal Hold notification emails can be sent to custodians directly from within the case. This feature is available in eDiscovery Premium.

---

# 🔍 Step 4: Run Content Search

## Create Search

Inside the case:

Navigate to:

```text id="j8w4qb"
Searches → New Search
```

---

## Select Data Locations

Choose locations:

* Exchange mailboxes
* SharePoint sites
* Microsoft Teams messages
* OneDrive

---

## Configure Search Criteria

Add:

### Keywords

Example:

```text id="w9k3tm"
"project phoenix"
```

### Date Range

Specify required investigation period.

### Sender / Recipient

Filter content by communication participants.

---

## Review Search Results

After running the search:

Review:

* Item count
* Data size

Preview results before exporting.

---

# 📤 Step 5: Export Search Results

## Export Discovery Results

From search results:

Navigate to:

```text id="x3n7qa"
Actions → Export results
```

---

## Configure Export Options

Select:

### Output Options

Configure:

* De-duplication
* Include versions

---

### File Format

Choose required format:

* PST for email
* Native format for files

---

## Download Export Package

Download the export package using:

```text id="v6m2zr"
eDiscovery Export Tool
```

Requirements:

* Internet Explorer mode in Microsoft Edge

---

> ⚠️ **Warning**
> eDiscovery exports may contain highly sensitive data. Restrict access strictly and maintain logs of all exports.

---

# ⭐ Best Practices & Pro Tips

* 👥 Always create a dedicated **eDiscovery Manager role group**. Never use Global Administrator for routine discovery operations.

* 🎯 Use **query-based holds** instead of blanket holds whenever possible to reduce scope and storage impact.

* 📝 Document all legal hold creation and release actions with timestamps to maintain chain-of-custody compliance.

* 🔎 Use **Review Sets (Premium)** to annotate, redact, and tag documents before exporting information to legal counsel.

* ⚖️ Coordinate with Legal or HR teams before releasing any legal hold. Early release may create compliance risks.

---

