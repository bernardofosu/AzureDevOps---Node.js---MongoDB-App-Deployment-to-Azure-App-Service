# 🟦 METHOD 1 — Use `az artifacts universal download` + App Service Deploy Task (Recommended) 🚀

This is the **simplest and cleanest method** to deploy your ZIP from Azure Artifacts Feed to Azure App Service.

---

## ✔️ Step 1 — Add a Task to Download From the Feed 📥

Add **Universal Download** task in the Release or Build pipeline.

### 💻 CLI Equivalent (for understanding):

```
az artifacts universal download \
  --organization "https://dev.azure.com/ofosubernard2026/" \
  --project "<your-project-id>" \
  --scope project \
  --feed "AzureDevOps-Feed" \
  --name "my-app-artifact" \
  --version "0.0.1" \
  --path "$(System.DefaultWorkingDirectory)/package"
```

👉 But don't type this manually — use the built-in task.

### 🧩 Azure DevOps Built‑In Task:

**Universal packages → Download**

| Field            | Value                                       |
| ---------------- | ------------------------------------------- |
| **Command**      | Download                                    |
| **Feed**         | AzureDevOps-Feed                            |
| **Package name** | my-app-artifact                             |
| **Version**      | 0.0.1 (or latest)                           |
| **Path**         | `$(System.DefaultWorkingDirectory)/package` |

This will download and extract the ZIP into the folder.

---

## ✔️ Step 2 — Deploy ZIP to App Service 🚀

Add **Azure Web App Deploy** task:

| Field            | Value                                                  |
| ---------------- | ------------------------------------------------------ |
| **Package/File** | `$(System.DefaultWorkingDirectory)/package/output.zip` |

(Adjust filename if needed.)

---

## 🟢 Your Pipeline Structure (Correct) ✅

1️⃣ **Download Universal Package** (from Feed)

2️⃣ **Azure Web App Deploy** (use the downloaded ZIP)

---

# 🟧 METHOD 2 — Use YAML With `az CLI` (Full Control) 🧩

Add an Azure CLI task:

```yaml
- task: AzureCLI@2
  inputs:
    azureSubscription: "<your-service-connection>"
    scriptType: "bash"
    scriptLocation: "inlineScript"
    inlineScript: |
      mkdir artifact
      az artifacts universal download \
        --organization "https://dev.azure.com/ofosubernard2026/" \
        --project "f2318cd5-97b6-4a33-81cb-f1ec52672021" \
        --scope project \
        --feed "AzureDevOps-Feed" \
        --name "my-app-artifact" \
        --version "0.0.1" \
        --path artifact

      # 🚀 Deploy ZIP to Azure App Service
      az webapp deployment source config-zip \
        --resource-group YourRG \
        --name YourAppServiceName \
        --src artifact/output.zip
```

---

# 🟩 METHOD 3 — Use Release Pipeline (Classic GUI) 🎬

If you're using a Release Pipeline:

1️⃣ Add **Universal Download** task

2️⃣ Add **Azure App Service Deploy** task

3️⃣ Point deploy task to the downloaded ZIP

💡 Works great for **production deployments**.

---

# 🧠 Why You MUST Download the Package First 🤔

✔️ App Service deploy requires a **real physical ZIP** file.

✔️ Azure Artifacts Feed stores files inside `.upack` format.

So your pipeline must:

1. ⬇️ **Download the UPack**
2. 📦 **Extract the ZIP inside it**
3. 🚀 **Deploy the ZIP**

➡️ You cannot deploy directly from the feed without downloading.

---

# ⭐ FINAL ANSWER ⭐

To deploy ZIP **from Artifacts Feed → App Service**, you must:

✔️ Add **Universal Download** task 📥
✔️ Download Universal Package into a folder 📁
✔️ Deploy extracted ZIP with **Azure Web App Deploy** 🚀

This method avoids the **drop** artifact completely and gives you a clean feed‑based deployment pipeline. 💙
