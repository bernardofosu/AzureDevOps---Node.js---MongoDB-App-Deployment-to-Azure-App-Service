# 🚀 Azure DevOps CI/CD: Java & Node.js + MongoDB App Deployment to Azure App Service

This project demonstrates an **end-to-end CI/CD implementation using Azure DevOps Classic Pipelines** to deploy **both Node.js and Java applications** to **Azure App Service (Linux)**, with **MongoDB (Azure Cosmos DB API)** as the backend.  
It covers **Service Principal authentication, environment variables, artifact publishing, SSH operations, and DNS configuration**.

---

## 🧩 Architecture Overview

- 🖥️ **Frontend / Backend**
  - Node.js (Express)
  - Java Web Application
- 🍃 **Database**
  - MongoDB (Azure Cosmos DB – MongoDB API)
- 🔁 **CI/CD**
  - Azure DevOps – Classic CI & CD Pipelines
- ☁️ **Hosting**
  - Azure App Service (Linux)
- 🔐 **Authentication**
  - Azure Service Principal
- 📦 **Artifacts**
  - Azure DevOps Artifacts (Universal Packages)
- 🌐 **DNS**
  - CNAME & A Records

---

## 🛠️ Tools & Technologies Used

- 🟦 **Azure DevOps (Classic Pipelines)**
- 🟩 **Node.js (v24)**
- ☕ **Java (Web App Deployment)**
- 🍃 **MongoDB / Azure Cosmos DB**
- 🔐 **Azure Service Principal**
- 📦 **Azure Artifacts (Universal Publish)**
- 🌐 **Azure App Service (Linux)**
- 🧠 **Environment Variables**
- 🌍 **DNS (CNAME, A Records)**
- 🐧 **Linux & Bash**
- 🔄 **CI/CD Automation**

---

## 🔄 CI Pipeline (Build)

### CI Steps:
- ✅ Checkout source code
- 📥 Install runtime (Node.js / Java)
- 📦 Run `npm install` / build Java app
- 🗜️ Archive build output
- 🚀 Publish artifacts to Azure DevOps

---

## 🚀 CD Pipeline (Release)

### CD Steps:
- 📥 Consume build artifacts
- 🔐 Authenticate using Azure Service Principal
- ☁️ Deploy to Azure App Service
- ▶️ Run startup command  
  - Node.js: `cd a && npm start`
  - Java: App Service startup configuration
- ✅ Verify deployment via browser & logs

---

## 🔐 Service Principal Configuration

Used for **secure, non-interactive authentication** between Azure DevOps and Azure.

Includes:
- 🆔 App Registration
- 🔑 Client ID & Client Secret
- 📜 Subscription access
- 🛡️ Role assignment (Contributor)

📸 *Reference screenshots included in repo*

---

## 🌱 Environment Variables (Azure App Service)

Sensitive configuration is injected securely using App Service settings.

- `AZURE_COSMOS_CONNECTIONSTRING`
- ❌ No secrets stored in source code

📸 *Reference screenshots included in repo*

---

## 🌐 DNS Configuration Notes

### Record Types Used:
- 🔗 **CNAME** → Maps custom domain to Azure App Service
- 📍 **A Record** → Maps domain to App Service IP
- 🔍 **nslookup** → DNS verification

📸 *Reference screenshots included in repo*


## 📸 Project Evidence & Screenshots
🚀 Application Deployment (Azure App Service)
![Deployed Node.js App](CD-Release%20Classic%20Pipeline/app.png)

🔄 CD – Release Pipeline (Azure DevOps Classic)
![Release Pipeline Configuration](CD-Release%20Classic%20Pipeline/release-pipeline.png)
![CD Deployment Logs](CD-Release%20Classic%20Pipeline/log-stream.png)

🔁 CI – Build Pipeline (Azure DevOps Classic)
![CI Pipeline Overview](CI%20Classic%20Pipeline/classic.png)
![CI Pipeline Tasks](CI%20Classic%20Pipeline/classic-1.png)
![Artifact Publish Step](CI%20Classic%20Pipeline/publish.png)
![Universal Package Publish](CI%20Classic%20Pipeline/publish1.png)

📦 Build Artifacts
![Artifact Folder Structure](CD-Release%20Classic%20Pipeline/artifact-folder.png)

🔐 Service Principal & Authentication
![Service Principal UI Setup](Service%20Principal%20UI%20Setup/ssh.png)

🌱 Environment Variables (Azure App Service)
![App Service Environment Variables](CI%20Classic%20Pipeline/app-env.png)

⚙️ Azure App Service Configuration
![Azure App Service Configuration](CD-Release%20Classic%20Pipeline/app.png)

🌐 DNS Configuration & Verification
![DNS Records Setup](DNS%20Notes/image.png)

📘 Reference Notes (Docs Used in This Project)
![Classic Pipeline Reference](CI%20Classic%20Pipeline/classic.png)

## 🎯 Key Highlights

- ✅ Classic CI & CD pipelines (enterprise-style)
- ✅ Node.js **and** Java deployments
- ✅ Secure Azure authentication
- ✅ Artifact-driven releases
- ✅ Production-ready Azure PaaS workflow

---
