# 🟦 Create & Understand Azure Service Principals (SP)

## 🟩 What Is a Service Principal?

A **Service Principal (SP)** is:

✔️ A *security identity* for apps, scripts, CI/CD pipelines  
✔️ Used to authenticate **without a human user**  
✔️ Used by automation tools like Azure DevOps, GitHub Actions, Terraform, Jenkins  

👉 Think of it as a **robot account for automation**.

---

## 🟧 What Is an Azure Subscription?

An Azure **Subscription** is:

✔️ A **billing container**  
✔️ The place where all Azure resources live  
✔️ NOT an identity  
✔️ Cannot be used to log in  

💡 Subscription = *Where resources exist*  
💡 SP = *Who/what accesses them*

---

## 🟦 Difference Between Service Principal & Subscription

| Feature | Service Principal (SP) | Subscription |
|--------|------------------------|-------------|
| What is it? | Identity for automation | Container for resources |
| Used for authentication? | ✔️ Yes | ❌ No |
| Holds resources? | ❌ No | ✔️ Yes |
| Used by pipelines/tools? | ✔️ Yes | ❌ No |
| Can assign roles? | ✔️ Yes | ❌ No |
| Can expire/rotate? | ✔️ Yes | ❌ No |

➡ **Summary:**  
- **Subscription = storage of resources**  
- **Service Principal = identity to access those resources**

---

## 🟦 Why Use Service Principal Instead of Subscription?

### ✔️ 1. Automation Needs Identity  
Tools like:  
- Azure DevOps  
- GitHub Actions  
- Terraform  
- Ansible  
- Jenkins  

…cannot log in as a human. They need a **Service Principal**.

### ✔️ 2. Security  
Never store personal passwords in pipelines.  
SP allows safe authentication using:
- Client ID  
- Client Secret  

### ✔️ 3. Least Privilege  
You can limit SP permissions:
- Reader  
- Contributor  
- Owner  

### ✔️ 4. Revocable + Expiring  
SP secrets can expire and be rotated.

### ✔️ 5. Headless Login  
Allows:

```
az login --service-principal
```

Perfect for CI/CD.

---

# 🟦 How to Create a Service Principal (Step-by-Step)

## 🟩 Step 1 — Register the Application  
1. Go to **Azure Portal**  
2. Open **Azure Active Directory**  
3. Select **App registrations**  
4. Click **New registration**  
5. Enter:  
   - Name  
   - Supported account types → *Default*  
   - Redirect URI → leave blank  
6. Click **Register**

---

## 🟩 Step 2 — Generate Client Secret  
1. Inside the App, go to **Certificates & secrets**  
2. Click **New client secret**  
3. Copy the **client secret value** ⚠️

---

## 🟩 Step 3 — Assign Role to SP  
Go to:  
**Subscription → Access Control (IAM)**

1. Click **Add role assignment**  
2. Choose a role (Contributor, Reader, Owner)  
3. Assign to:  
   **User, group, or service principal**  
4. Search your app → select → save

---

# 🟦 SP Credentials Needed in Pipelines

You will get:

```
Tenant ID
Client ID
Client Secret
Subscription ID
```

Example login:

```
az login --service-principal   --username CLIENT_ID   --password CLIENT_SECRET   --tenant TENANT_ID
```

---

# 🟦 Quick Summary

| Concept | Meaning |
|--------|---------|
| **Service Principal** | Identity for automation |
| **Subscription** | Where resources live (billing container) |
| **Use SP** | For CI/CD, scripts, Terraform |
| **SP Permissions** | Given through IAM roles |
| **Setup** | App Registration → Secret → IAM Role |

---

If you want, I can also create a **diagram**, **Terraform example**, or **Azure DevOps SP usage tutorial**. 