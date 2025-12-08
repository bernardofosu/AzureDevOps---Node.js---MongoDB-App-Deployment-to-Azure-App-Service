## 🔵 Add the SP to Azure DevOps Service Connection 🔗

1. Go to **Azure DevOps → Project Settings → Service connections**
2. Click **New service connection**
3. Choose **Azure Resource Manager**
4. Select **Service principal (manual)**
5. Enter the details:

| Field                 | Value                         |
| --------------------- | ----------------------------- |
| Subscription ID       | Your Azure subscription ID 🆔 |
| Subscription Name     | Azure subscription 1          |
| Tenant ID             | Directory (tenant) ID 🏢      |
| Service Principal ID  | Application (client) ID 🔑    |
| Service Principal Key | Client secret Value 🔐        |

6. ✔️ **Grant access permission to all pipelines**
7. Click **Verify and Save**

If successful → You will see a green ✔️ on the connection.

---

## 🔵 5. Why Azure DevOps Asked Again for Client ID?

Because you selected **Manual Service Principal authentication**, which ALWAYS requires:

- Client ID
- Client Secret
- Tenant ID

Even if you used the connection previously, Azure DevOps requires these fields to verify access.

---

## 🔵 6. Common Issues & Fixes ⚠️🔧

### ❌ Issue: "Service Principal not found"

✔️ Fix: Your SP is in a different Tenant → Check the directory in the portal top-right.

### ❌ Issue: "No permission to subscription"

✔️ Fix: Give **Contributor** role at Subscription or Resource Group.

### ❌ Issue: "Invalid client secret"

✔️ Fix: Create a **new client secret** and update DevOps.

### ❌ Issue: "Federated credentials message in DevOps"

✔️ Ignore — this only applies when using **OIDC federation**, not client secret.

---

## 🟦 Final Summary ⭐

Your Azure DevOps Service Connection requires:

- **Client ID** (App Registration → Overview)
- **Tenant ID** (App Registration → Overview)
- **Client Secret** (Certificates & secrets)
- **Contributor Role** on Subscription (IAM → Role Assignment)

Once all these are set → DevOps can deploy Web Apps, VMs, AKS, Storage, etc. 🚀

---

If you want, I can also generate:
✨ A diagram version
✨ A YAML pipeline using this SP
✨ A PDF version for download

Just tell me! 😊💙

# 🔐 Azure DevOps – New UI (2025)

## How to Create Azure Resource Manager Service Connection (Manual SPN)

Microsoft updated the Azure DevOps UI, so manual SPN creation is now hidden.
This guide shows the **exact new steps** to create a **manual Service Principal connection**.

---

## 🚀 1. Open Service Connections

Go to:

➡️ **Project Settings → Service Connections → New service connection**

Select:

🌐 **Azure Resource Manager** → **Next**

---

## 🚀 2. Azure DevOps Shows Automatic Mode

By default, you will see:

- **Identity type:** App registration (automatic)
- **Credential:** Workload identity federation
- **Subscription:** Your Azure subscription

❗ The screen does **NOT** show the Manual SPN option yet.

---

## 🚀 3. Switch to Manual Mode (Hidden Step)

Under the subscription dropdown, click this small blue link:

🔵 **"create manually"**

💥 This replaces the former “Manual Service Principal” option.

---

## 🚀 4. Manual SPN Form Appears

After clicking **create manually**, the form expands and shows:

- 🆔 **Application (client) ID**
- 🏢 **Directory (tenant) ID**
- 🔐 **Client Secret**
- 🔧 **Credential Type (Service principal key)**
- 📝 **Service Connection Name**

This is the full manual SPN configuration.

---

## 🚀 5. Enter Your Service Principal Details

Paste the values from Azure App Registration:

🔑 **Tenant ID** → Found in Azure AD / Entra
🆔 **Client ID** → From App Registration
🔐 **Client Secret** → From Certificates & Secrets

Click:

✔️ **Verify**

You should see:

✅ **Verification succeeded**

---

## 🚀 6. Save the Connection

Fill in a name, e.g.:

- `webapp-conn`
- `sp-conn`
- `production-conn`

Enable:

✔ **Grant access permission to all pipelines** (recommended)

Then click:

💾 **Verify and Save**

---

## 🎉 Final Result

You now have a **working Azure Resource Manager service connection** using **manual Service Principal authentication**.

This connection can be used for:

- App Service deployments
- Terraform deployments
- AKS / ACR / VM deployments
- Release pipelines
- YAML pipelines

---

## ✅ Quick Summary (Cheat Sheet)

- 👉 New ARM connection → Next
- 👉 Auto mode appears
- 👉 Click **create manually**
- 👉 Enter Client ID, Tenant ID, Secret
- 👉 Verify → Save
- 🎉 Done!

---

Let me know if you want **a second Canva file explaining SP creation steps** 😄
