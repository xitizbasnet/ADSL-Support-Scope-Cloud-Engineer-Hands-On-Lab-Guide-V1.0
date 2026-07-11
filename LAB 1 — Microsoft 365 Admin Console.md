# LAB 1 — Microsoft 365 Admin Console

## Product: Microsoft 365 Admin Center

## 📘 Lab Overview

This lab provides hands-on experience with the Microsoft 365 Admin Center and covers essential administrative tasks including user and group management, tenant configuration, licensing operations, Microsoft support requests, and monitoring Microsoft 365 service notifications.

---

# 🎯 Lab Objectives

By completing this lab, you will learn how to:

* ✅ Create and manage Users and Groups
* ✅ Manage Access, Tenant settings, and Domain records
* ✅ Assign and reclaim Microsoft 365 Licenses
* ✅ Raise a support case with Microsoft
* ✅ Monitor Message Centre notifications and plan corrective actions

---

# 🛠️ Step 1: Access the Microsoft 365 Admin Center

## Access Portal

1. Open a web browser and navigate to:

   ```
   https://admin.microsoft.com
   ```

2. Sign in using your **Global Administrator** or appropriate administrative credentials.

3. After successful authentication, you will land on the **Microsoft 365 Admin Center Home dashboard**.

> 💡 **Best Practice / Tip**
> Bookmark this URL. All Microsoft 365 management tasks start from the Microsoft 365 Admin Center.

---

# 👤 Step 2: Create a New User

## Create User Account

1. In the left navigation pane, go to:

   ```
   Users → Active Users → Add a user
   ```

2. Enter the required user information:

   * First name
   * Last name
   * Username (UPN)
   * Display name

3. Configure the password:

   * Set a temporary password, or
   * Allow the system to auto-generate a password

4. Assign a **Usage Location**.

   > ⚠️ **Important**
   > Usage Location is required before assigning Microsoft 365 licenses.

5. Click **Next**.

6. Assign the appropriate license.

   Example:

   ```
   Microsoft 365 E3
   ```

7. Configure administrative roles if required.

   Example:

   ```
   Global Reader — Helpdesk staff
   ```

8. Click:

   ```
   Finish adding
   ```

   to create the account.

## Verification

* Search for the newly created user under:

  ```
  Active Users
  ```

> 💡 **Best Practice / Tip**
> Always set Usage Location first. License assignment will fail without it.

---

# 👥 Step 3: Create and Manage a Group

## Create a Group

1. Navigate to:

   ```
   Teams & Groups → Active Teams & Groups → Add a group
   ```

2. Select the required group type:

   | Group Type          | Purpose                                     |
   | ------------------- | ------------------------------------------- |
   | Microsoft 365 Group | Used for Teams and SharePoint collaboration |
   | Security Group      | Used for access control and permissions     |

3. Configure the group details:

   * Group name
   * Description
   * Owner

4. For Microsoft 365 Groups, configure:

   * Privacy settings:

     * Public
     * Private
   * Group members

5. Click:

   ```
   Create group
   ```

---

## Manage Group Membership

To update group membership:

```
Select Group → Members tab → Add/Remove members
```

---

## PowerShell — Get All Members of a Group

```powershell
Connect-MsolService

Get-MsolGroupMember -GroupObjectId
```

---

# ⚙️ Step 4: Manage Tenant Settings

## Organization Settings

Navigate to:

```
Settings → Org Settings
```

Review and configure:

* Security & privacy
* Microsoft 365 services
* Partner relationships

---

## Domain Management

Navigate to:

```
Settings → Domains
```

Add and verify a custom domain:

1. Click:

   ```
   Add domain
   ```

2. Enter your domain name.

3. Verify ownership using a TXT record in your DNS provider.

4. Add required DNS records:

   * MX
   * CNAME
   * TXT record for SPF

5. Set the domain as the default domain if required.

> ⚠️ **Warning**
> Never delete the `onmicrosoft.com` domain. It is your fallback identity.

---

# 🔑 Step 5: License Management

## View Available Licenses

Navigate to:

```
Billing → Licenses
```

View all available subscriptions.

---

## Assign a License

1. Navigate to:

   ```
   Active Users
   ```

2. Select the user.

3. Open:

   ```
   Licenses and apps tab
   ```

4. Select the required license.

5. Click:

   ```
   Save
   ```

---

## Reclaim a License

1. Select the user.

2. Open:

   ```
   Licenses and apps
   ```

3. Uncheck the assigned license.

4. Save changes.

---

## Purchase Additional Licenses

Navigate to:

```
Billing → Purchase Services
```

---

## PowerShell — Assign License

```powershell
Set-MsolUserLicense -UserPrincipalName user@domain.com -AddLicenses `
'tenantname:ENTERPRISEPACK'
```

---

## PowerShell — Remove License

```powershell
Set-MsolUserLicense -UserPrincipalName user@domain.com -RemoveLicenses `
'tenantname:ENTERPRISEPACK'
```

---

# 🆘 Step 6: Raise a Support Case with Microsoft

## Create a Support Request

1. Navigate to:

   ```
   Support → New service request
   ```

   Alternatively, select the:

   ```
   ? icon (top-right corner)
   ```

2. Describe the issue in the search box.

3. Review AI-suggested solutions first.

4. If unresolved, select:

   ```
   Contact support
   ```

5. Choose a support method:

   * Phone callback
   * Email
   * Chat

6. Provide:

   * Issue summary
   * Severity level
   * Contact details

7. Save the support case number for tracking.

---

## Track Support Requests

Navigate to:

```
Support → View service requests
```

---

# 📢 Step 7: Monitor Message Centre & Plan Corrective Actions

## Access Message Centre

Navigate to:

```
Health → Message Centre
```

---

## Filter Notifications

Use filters:

* Product
* Category:

  * Plan for Change
  * Stay Informed
  * Prevent or Fix Issues

---

## Review Notifications

For each relevant message:

1. Review the impact.
2. Check the timeline.
3. Identify required actions.

---

## Message Management

Use:

* **Archive** — For completed items
* **Favourite** — For critical items

---

## Create a Corrective Action Plan

Document and execute the following process:

1. Document the change.
2. Test the change in a staging tenant.
3. Schedule user communications.
4. Execute the change in production.

---

## Enable Weekly Digest Emails

Navigate to:

```
Preferences → Email → Enable digest
```

> 💡 **Best Practice / Tip**
> Integrate Message Centre alerts with Microsoft Teams or ServiceNow using Power Automate for proactive management.

---

# ⭐ Best Practices & Pro Tips

* 🔐 Use the **Principle of Least Privilege** — assign only the minimum administrator role required for each task.

* 🔒 Always enable **Multi-Factor Authentication (MFA)** for all administrator accounts before performing administrative activities.

* 👥 Use **Microsoft 365 Groups** instead of Distribution Lists for modern collaboration workloads.

* 📊 Monitor the **Service Health dashboard daily** — it is faster than waiting for user-reported issues.

* 📝 Document every license change in a **Configuration Management Database (CMDB)** or change log for audit purposes.

* 🧪 Test all tenant changes in a dedicated **staging/development tenant** before applying changes to production.

---

