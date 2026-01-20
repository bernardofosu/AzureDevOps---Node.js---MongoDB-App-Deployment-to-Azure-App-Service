🚀 Azure DevOps: Node.js + MongoDB App Deployment to Azure App Service

This project demonstrates an end-to-end CI/CD pipeline using Azure DevOps Classic Pipelines to deploy a Node.js + MongoDB application to Azure App Service, including Service Principal authentication, environment variables, artifact publishing, and DNS configuration.

🧩 Architecture Overview

Frontend / Backend: Node.js (Express)

Database: MongoDB (Cosmos DB API)

CI/CD: Azure DevOps (Classic CI & CD Pipelines)

Hosting: Azure App Service (Linux)

Authentication: Azure Service Principal

Artifacts: Azure DevOps Artifacts (Universal Packages)

DNS: CNAME & A Records

🛠️ Tools & Technologies Used

🟦 Azure DevOps (Classic Pipelines)

🟩 Node.js (v24)

🍃 MongoDB / Cosmos DB

🔐 Azure Service Principal

📦 Azure Artifacts (Universal Publish)

🌐 Azure App Service

🧠 Environment Variables

🌍 DNS (CNAME, A Records)

🔄 CI Pipeline (Build)
CI Steps:

Checkout source code

Install Node.js

Run npm install

Archive build output

Publish artifacts

📸 CI Pipeline Screenshots








🚀 CD Pipeline (Release)
CD Steps:

Consume build artifacts

Authenticate using Service Principal

Deploy to Azure App Service

Run startup command (cd a && npm start)

Verify deployment

📸 CD Pipeline Screenshots




🔐 Service Principal Configuration

Used for secure, non-interactive authentication between Azure DevOps and Azure.

Included:

App Registration

Client ID & Secret

Subscription access

Role assignment

📸 Reference:


🌱 Environment Variables (App Service)

Sensitive configuration is injected via Azure App Service Environment Variables.

AZURE_COSMOS_CONNECTIONSTRING

No secrets stored in code

📸 Reference:


🌐 DNS Configuration Notes
Record Types Used:

CNAME → Maps domain to Azure App Service

A Record → Maps domain to IP

nslookup → DNS verification

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
