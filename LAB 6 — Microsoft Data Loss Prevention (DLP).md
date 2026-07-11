# LAB 6 — Microsoft Data Loss Prevention (DLP)

## Product: Microsoft Purview / Data Loss Prevention (DLP)

---

## 📘 Lab Overview

This lab provides hands-on experience with **Microsoft Purview Data Loss Prevention (DLP)** policy management, incident investigation, and reporting.

The lab covers creating DLP policies, defining sensitive information types, investigating policy violations, and generating compliance reports.

---

# 🎯 Lab Objectives

By completing this lab, you will learn how to:

* ✅ Create and configure DLP Policies
* ✅ Define Sensitive Information Types
* ✅ Investigate and manage DLP Incidents
* ✅ Generate DLP Reports

---

# 🌐 Step 1: Access Microsoft Purview Compliance Portal

## Access Portal

Navigate to:

```text id="9q2x7m"
https://compliance.microsoft.com
```

---

## Access DLP Policies

Navigate to:

```text id="r8x1pa"
Data Loss Prevention → Policies
```

---

# 🛡️ Step 2: Create a DLP Policy

## Create New Policy

1. Click:

```text id="5g2wqe"
Create Policy
```

2. Choose a policy template:

Examples:

* Financial data — India
* PII
* GDPR

Alternatively:

* Start with a custom policy

---

## Select Policy Locations

Choose the locations where DLP controls will apply:

* Exchange
* SharePoint
* OneDrive
* Microsoft Teams
* Endpoint devices

---

## Define DLP Rules

Configure rules using:

```text id="j3v6kp"
Content contains [Sensitive Information Type] → Action
```

---

## Available Actions

Configure actions such as:

* Block or audit sharing
* Show policy tip to users
* Notify administrators
* Encrypt content

---

## Configure Policy Mode

Set policy mode:

1. Test mode first:

   ```
   Simulate without enforcement
   ```

2. Review results.

3. Change to:

   ```
   Active
   ```

   when ready for enforcement.

---

> 💡 **Best Practice / Tip**
> Always start DLP policies in **Test mode** and review alerts for at least **2 weeks** before enabling enforcement.

---

# 🔎 Step 3: Custom Sensitive Information Types

## Create Custom Sensitive Information Type (SIT)

Navigate to:

```text id="u7a4pz"
Data Classification → Sensitive Info Types → Create
```

---

## Define Sensitive Information Type Properties

Configure:

* Name
* Description
* Pattern (Regex)
* Keyword lists
* Confidence level

---

## Example — Indian Aadhaar Number Pattern

Use the following Regex pattern:

```regex id="d9o6pq"
\b[0-9]{4}\s[0-9]{4}\s[0-9]{4}\b
```

---

## Validate Custom SIT

Before publishing:

1. Test the Sensitive Information Type with sample data.
2. Confirm detection accuracy.
3. Reference the custom SIT in DLP rules.

---

# 🚨 Step 4: Investigate DLP Incidents

## View DLP Alerts

Navigate to:

```text id="k5n1tw"
Data Loss Prevention → Alerts
```

---

## Review Alert Details

Select an alert to view:

* User
* File or email content
* Matched policy
* Activity details

---

## Available Investigation Actions

Actions include:

* Dismiss alert (false positive)
* Escalate
* View evidence

---

## Email Incident Investigation

For email-related incidents:

Review message trace in Exchange to obtain additional context.

---

## Advanced Investigation

Navigate to:

```text id="z3c8wa"
Incidents & Alerts → Incidents
```

Use this area for advanced investigation activities.

---

# 📊 Step 5: DLP Reporting

## View DLP Reports

Navigate to:

```text id="q9m2vx"
Reports → DLP Policy Matches and DLP Incidents
```

---

## Filter Reports

Apply filters by:

* Date
* Policy
* Location
* Severity

---

## Export Reports

Export reports as:

```text id="m4r8kt"
CSV
```

Use exported reports for compliance documentation.

---

## Schedule Reporting

Create dashboards using:

* Power BI
* Microsoft Graph API

---

## PowerShell — Get DLP Policy Match Events

```powershell id="a7c5ny"
Get-DlpDetailReport `
-StartDate (Get-Date).AddDays(-30) `
-EndDate (Get-Date) |
Export-Csv dlp_report.csv
```

---

# ⭐ Best Practices & Pro Tips

* 🧪 Run all new DLP policies in **Test mode for at least 14 days** before enforcement.

* ✅ Use **Business Justification overrides**. Allow users to override actions with a reason to avoid blocking legitimate business activities.

* 🎯 Scope DLP policies to specific locations or groups initially. Avoid organization-wide enforcement until the policy has been validated.

* 📈 Tune policies based on false positive rates. Policies that block too much may encourage users to bypass controls.

* 🔐 Integrate DLP alerts into your SIEM platform:

  ```
  Microsoft Sentinel
  ```

  for centralized security monitoring.

* 🔄 Review and update Sensitive Information Type patterns annually as data formats and business requirements change.

---


