# 🚀 Azure DevOps Deployment Tasks — Old vs New (With Full YAML) 🤓✨

This document explains the **two Azure DevOps deployment tasks** that can deploy a Java Spring Boot JAR to Azure App Service:

- 🆕 **AzureWebApp@1** (New Task — Recommended)
- 🧓 **AzureRmWebAppDeployment@5** (Old Task — Still Works)

Both tasks work, but each has different behavior, pros, and use cases.

---

# 🌟 1. NEW Deployment Task — `AzureWebApp@1` (Recommended) 🚀

### ✅ Best for modern Linux App Services

### ✅ Supports direct JAR deployment

### ❌ Does NOT use ZIP Deploy

### ✔ Simple and clean configuration

### **Example:**

```yaml
- task: AzureWebApp@1
  displayName: "Deploy Spring Boot JAR"
  inputs:
    azureSubscription: "webapp-conn"
    appType: "webAppLinux"
    appName: "javaapp"
    package: "$(Pipeline.Workspace)/drop/*.jar"
    runtimeStack: "JAVA|11-java11"
```

### ⭐ Why it's better

- Directly deploys JARs
- No unexpected ZIP extraction
- Less error‑prone
- Recommended by Microsoft for YAML pipelines

---

# 🧓 2. OLD Deployment Task — `AzureRmWebAppDeployment@5` 🏷️

### ✔ Still works for JAR deployment

### ❗ Originally designed for ZIP Deploy

### ✔ Useful for older pipelines

### ⚠️ More fragile (ZIP assumptions)

### **Example:**

```yaml
- task: AzureRmWebAppDeployment@5
  displayName: "Deploy Spring Boot JAR"
  inputs:
    ConnectionType: "AzureRM"
    azureSubscription: "webapp-conn"
    appType: "webAppLinux"
    WebAppName: "javaapp"
    packageForLinux: "$(Pipeline.Workspace)/drop/*.jar"
    RuntimeStack: "JAVA|11-java11"
```

### ⚠️ Why it can fail

- Tries to treat the JAR like a ZIP
- Produces Kudu ZIP errors:

  - _rsync failed_
  - _No such file or directory_
  - _ZIP Deploy failed_

- More sensitive to path issues

---

# 🎯 Summary: When to Use Each Task

| Feature           | `AzureWebApp@1` (New) | `AzureRmWebAppDeployment@5` (Old) |
| ----------------- | --------------------- | --------------------------------- |
| Recommended       | ⭐ YES                | ⚠️ Legacy only                    |
| Direct JAR deploy | ✅ Yes                | ⚠️ Works but not native           |
| ZIP Deploy        | ❌ Not used           | ✅ Built for ZIP                  |
| Reliability       | ⭐ High               | ⚠️ Medium                         |
| Best for          | Linux Java apps       | Classic ZIP deployments           |

---

# 📦 FULL YAML — INCLUDING BOTH DEPLOYMENT TASKS

Below is a complete pipeline including:

- Maven build
- Copy JAR
- Publish artifact
- **Two deploy stages** (new + old)

---

## 🧪 **FULL YAML (Both Deployment Methods)**

```yaml
trigger:
  branches:
    include:
      - main

pool:
  name: nakodtech
  demands:
    - agent.name -equals Agent-1

variables:
  artifactName: drop

stages:
  # -------------------------------------------------------
  # STAGE 1: BUILD JAVA APP
  # -------------------------------------------------------
  - stage: Build
    displayName: "Build Java App"

    jobs:
      - job: BuildJob
        displayName: "Maven Build & Publish JAR"

        steps:
          - task: Maven@4
            displayName: "Maven Build"
            inputs:
              mavenPomFile: "pom.xml"
              goals: "package"
              publishJUnitResults: false

          - task: CopyFiles@2
            displayName: "Copy JAR to Artifact Folder"
            inputs:
              SourceFolder: "$(Build.SourcesDirectory)/target"
              Contents: "*.jar"
              TargetFolder: "$(Build.ArtifactStagingDirectory)"

          - task: PublishBuildArtifacts@1
            displayName: "Publish JAR Artifact"
            inputs:
              pathToPublish: "$(Build.ArtifactStagingDirectory)"
              artifactName: "$(artifactName)"

  # -------------------------------------------------------
  # STAGE 2: DEPLOY — NEW TASK (AzureWebApp@1)
  # -------------------------------------------------------
  - stage: Deploy_New
    displayName: "Deploy with AzureWebApp@1"
    dependsOn: Build

    jobs:
      - job: DeployJob_New
        displayName: "Deploy using NEW Task"

        steps:
          - download: current
            artifact: drop

          - task: AzureWebApp@1
            displayName: "Deploy Spring Boot JAR (New Task)"
            inputs:
              azureSubscription: "webapp-conn"
              appType: "webAppLinux"
              appName: "javaapp"
              package: "$(Pipeline.Workspace)/drop/*.jar"
              runtimeStack: "JAVA|11-java11"

  # -------------------------------------------------------
  # STAGE 3: DEPLOY — OLD TASK (AzureRmWebAppDeployment@5)
  # -------------------------------------------------------
  - stage: Deploy_Old
    displayName: "Deploy with AzureRmWebAppDeployment@5"
    dependsOn: Build

    jobs:
      - job: DeployJob_Old
        displayName: "Deploy using OLD Task"

        steps:
          - download: current
            artifact: drop

          - task: AzureRmWebAppDeployment@5
            displayName: "Deploy Spring Boot JAR (Old Task)"
            inputs:
              ConnectionType: "AzureRM"
              azureSubscription: "webapp-conn"
              appType: "webAppLinux"
              WebAppName: "javaapp"
              packageForLinux: "$(Pipeline.Workspace)/drop/*.jar"
              RuntimeStack: "JAVA|11-java11"
```

---

# 🎉 Final Notes

- Both tasks **deploy successfully**, but the **new task is cleaner and more reliable**.
- Old task is mostly for **ZIP deployments**, not JAR.
- Your Java App Service automatically starts the JAR because of the `JAVA|11` runtime.

If you want, I can also:
✔ Add **slot deployment**
✔ Add **approval gates**
✔ Add **environment variables** YAML
✔ Create **Node.js or Python versions**

Just let me know! 😊🚀
