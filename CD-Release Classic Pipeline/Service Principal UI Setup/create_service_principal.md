# 🟦 Azure DevOps Service Connection (Manual SP + RBAC) — Full Notes 📘✨

This guide explains **exact steps** to manually create a Service Principal (SP), generate a client secret, assign RBAC roles, and connect it to Azure DevOps. All steps include emojis for clarity! 😄🔥

---

## 🔵 1. Create an App Registration (Service Principal)

1. Go to **Azure Portal → Microsoft Entra ID → App registrations**
2. Click **➕ New registration**
3. Enter:

   - **Name:** `service-principal` 🏷️
   - **Supported account types:** ✔️ **Accounts in this organizational directory only**

4. Click **Register**

🎉 Now your App Registration (SP) is created.

---

## 🔵 2. Create a Client Secret 🔐

1. Inside the App registration → **Certificates & secrets**
2. Click **New client secret**
3. Add:

   - **Description:** `sp-conn-secret`
   - **Expires:** Recommended 180 days

4. Click **Add**
5. ⚠️ **Copy the Value immediately** — you cannot view it again!

You will use:

- ✔️ **Application (client) ID**
- ✔️ **Directory (tenant) ID**
- ✔️ **Client Secret Value**

---

## 🔵 3. Assign RBAC Role to the Service Principal 👑

Your SP must have access to the Subscription.

1. Go to **Azure Portal → Subscriptions → Your Subscription**
2. Go to **Access Control (IAM)**
3. Click **Add → Add role assignment**
4. Choose Role:

   - ⭐ **Contributor** (recommended)

5. Click **Next → Members**
6. Select:

   - **User, group, or service principal**

7. Search for your SP:

   - `service-principal` 🔍

8. Select it → **Next → Review + assign**

🎉 Your SP now has rights to deploy resources.

---
