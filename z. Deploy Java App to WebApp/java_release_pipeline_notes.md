# 🚀 Azure DevOps Release Pipeline — Deploy Java JAR to Azure App Service

This guide explains how to correctly configure an **Azure DevOps Release Pipeline** to deploy a **Java JAR** file to **Azure Web App for Linux**, matching the exact configuration shown in your screenshots.  

---

## 🎯 **1. Stage Overview – Deploy Jar App**
- **Stage name:** `Deploy Jar App`
- The stage contains:
  - 🧩 **Run on agent** (your self‑hosted pool)
  - ☕ **Deploy Jar to Azure App Service task**

---

## 🧑‍💻 **2. Configure the Agent Job**
### ✔️ Select Your Agent Pool
- Go to **Run on agent**
- Choose:
  - **Agent pool:** `nakodtech`  
  - This ensures the release uses your **self‑hosted agent**.

### ✔️ No demands required  
Your agent already supports Java builds & deployments.

---

## ☕ **3. Configure “Deploy Jar to Azure App Service” Task**
This is the core step that deploys your **Spring Boot JAR**.

### 🔧 **Task Name**
`Deploy Jar to Azure App Service`

### 🏗 **Connection Settings**
| Field | Value |
|------|--------|
| **Connection type** | Azure Resource Manager |
| **Azure subscription** | `webapp-conn` |
| **App Service type** | Web App on Linux |
| **App Service name** | `javaapp` |

---

## 📦 **4. Package or Folder Path**
This must point to the **JAR file inside the drop folder** created during CI.

From your screenshot:

```
$(System.DefaultWorkingDirectory)/_Azure DevOps JAVA Project-CI/drop/target/secretsanta-0.0.1-SNAPSHOT.jar
```

✔️ This is correct because:  
- CI pipeline publishes the entire `target/` folder  
- The release pipeline downloads it into:  
  `$(System.DefaultWorkingDirectory)/_PipelineName/drop/`

---

## 🔥 **5. Stack & Startup Command**
### ✔️ **Runtime Stack**
You did NOT configure it — and that is fine.

Azure App Service automatically detects Java because:
- You deployed a `.jar`
- Java 11 runtime is enabled by default for Java Linux Web Apps

### ✔️ **Startup Command (Optional)**
You left it empty — and it still worked 🎉  
Azure automatically runs:

```
java -jar yourfile.jar
```

But if needed, you can manually set:

```
java -jar secretsanta-0.0.1-SNAPSHOT.jar
```

---

## 🎉 **6. Summary**
Your release pipeline works because:

### ✅ Azure App Service auto-detects Java  
### ✅ Your JAR is uploaded to `/home/site/wwwroot`  
### ✅ App Service automatically starts the JAR  
### ✅ No need for zip packaging like Node.js  
### ✅ No startup command required unless custom behavior is needed  

---

## 📝 Final Notes
- Node.js apps deploy as **zip packages** → require packaging step.  
- Java apps deploy using **.jar** directly → App Service runs the JAR automatically.  
- Your release pipeline is correctly configured exactly as expected.  

---

If you want, I can also prepare:
✅ A full CI/CD YAML version  
✅ A printable PDF  
✅ A diagram for the entire pipeline  

Just tell me! 😄  
