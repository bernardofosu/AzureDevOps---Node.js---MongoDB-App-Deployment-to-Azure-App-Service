# 🚀 Azure App Service – Clean & Redeploy Guide 🧹🔁

Below is the **clean and safe way** to wipe everything inside `/site/wwwroot` and redeploy your Node.js app again. 😊🔥

---

## 🧹 **1. Clear Everything Inside /site/wwwroot**

Use SSH in App Service and run:

```bash
cd /home/site/wwwroot
rm -rf *
```

✨ This deletes ALL files in the webroot.

⚠️ **Your app will break temporarily** until you redeploy.

---

## 🔄 **2. Folder Should Now Be Empty**

Check:

```bash
ls
```

You should see **nothing**.

---

## 🚀 **3. Redeploy Your App**

You may deploy using any of these:

### ✔ ZIP Deploy

```bash
az webapp deployment source config-zip \
  --resource-group <RG> \
  --name <APP_NAME> \
  --src myapp.zip
```

### ✔ VS Code Deploy

Right‑click your folder → **Deploy to Web App** 💻

### ✔ GitHub Actions / CI/CD

Push your code → Azure builds automatically ⚙️

---

## 💡 **Tip:** Deploy Your App Directly Into `/site/wwwroot` Only

Do **NOT** deploy into a subfolder like `/site/wwwroot/a`.

Correct structure:

```
/site/wwwroot
 ├── app.js
 ├── package.json
 ├── routes/
 ├── models/
 ├── views/
 └── public/
```

---

## 🎉 Done!

Your App Service is now **clean**, **fresh**, and ready for a new deployment! 💪🔥

If you want, I can write the **full automation script**, **deployment YAML**, or **VS Code workflow** with emojis too! 😄

steps:

- task: NodeTool@0
  inputs:
  versionSource: 'spec'
  versionSpec: '20'

- task: Npm@1
  inputs:
  command: 'install'
  workingDir: '.'

steps:

- task: CopyFiles@2
  inputs:
  SourceFolder: '$(Build.SourcesDirectory)'
    Contents: '**'
    TargetFolder: '$(Build.ArtifactStagingDirectory)'
