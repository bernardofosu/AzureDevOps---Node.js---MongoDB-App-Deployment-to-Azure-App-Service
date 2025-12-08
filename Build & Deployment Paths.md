# 📁 Azure DevOps Build & Deployment Paths — Explained with Emojis

Below are the **five most important directory variables** you use in Azure DevOps pipelines when building and deploying Java, Node, Python, or any app.
Each one is explained with **where it points**, **when it is used**, and **real examples**.

---

## 1️⃣ `$(Build.ArtifactStagingDirectory)`

📌 **Where files are staged before publishing as artifacts**

🟦 **Meaning:**
This is the **temporary folder** where you place files you want to publish as artifacts.

🛠️ **Used in BUILD stage**
You copy your _JAR_, _ZIP_, or _dist folder_ here → then publish it.

📂 **Examples:**

```yaml
TargetFolder: "$(Build.ArtifactStagingDirectory)"
```

```yaml
pathToPublish: "$(Build.ArtifactStagingDirectory)"
```

📝 **Think of it like:**
📦 “This is the box where you place your output before shipping it.”

---

## 2️⃣ `$(System.DefaultWorkingDirectory)`

📌 **Where artifacts are downloaded during the DEPLOY stage**

🟦 **Meaning:**
In the **Deploy stage**, Azure DevOps downloads your artifact here.

🛠️ **Used in DEPLOY stage**

```yaml
packageForLinux: "$(System.DefaultWorkingDirectory)/**/*.zip"
```

📂 **Contains:**

```
/drop/javaapp.zip
/drop/*.jar
```

📝 **Think of it like:**
📥 “This is where Azure places the files you've shipped to be deployed.”

---

## 3️⃣ `$(Pipeline.Workspace)/drop/*.jar`

📌 **Same purpose as DefaultWorkingDirectory but cleaner**

🟦 **Meaning:**
Another path pointing to downloaded artifacts, but scoped per pipeline.

🛠️ Used when deploying pure JAR:

```yaml
packageForLinux: "$(Pipeline.Workspace)/drop/*.jar"
```

📂 Example folder:

```
/workspace/1/drop/myapp.jar
```

📝 **Think of it like:**
📦 “A clean pipeline workspace that contains all artifacts.”

---

## 4️⃣ `$(Build.SourcesDirectory)`

📌 **Where your Git repo is checked out**

🟦 **Meaning:**
Your _source project folder_ — the entire repository.

🌱 Contains your code:

```
/repo/src
/repo/pom.xml
/repo/target/
```

🛠️ Used in BUILD stage:

```yaml
mavenPomFile: "$(Build.SourcesDirectory)/pom.xml"
```

📝 **Think of it like:**
🗂️ “Your actual source code folder.”

---

## 5️⃣ `$(Build.SourcesDirectory)/target`

📌 **Where Maven outputs the JAR file**

🟦 **Meaning:**
When Maven builds your app, it creates:

```
target/myapp-0.0.1-SNAPSHOT.jar
```

🛠️ You normally copy the JAR from here:

```yaml
SourceFolder: "$(Build.SourcesDirectory)/target"
Contents: "*.jar"
```

📝 **Think of it like:**
🏭 “The build factory output of Maven.”

---

# 🎯 Quick Summary Table

| Variable                            | Meaning                                  | Stage  | Example Use          |
| ----------------------------------- | ---------------------------------------- | ------ | -------------------- |
| `$(Build.ArtifactStagingDirectory)` | Temp folder for publishing artifacts     | BUILD  | Copy & publish files |
| `$(System.DefaultWorkingDirectory)` | Where artifacts land during DEPLOY       | DEPLOY | Deploy ZIP/JAR       |
| `$(Pipeline.Workspace)/drop/*.jar`  | Clean workspace for downloaded artifacts | DEPLOY | JAR OneDeploy        |
| `$(Build.SourcesDirectory)`         | Git repo checkout folder                 | BUILD  | Maven build          |
| `$(Build.SourcesDirectory)/target`  | Maven output folder                      | BUILD  | Copy JAR             |

---

If you want, I can also create:

- 🔹 A diagram of file movement between folders
- 🔹 A full pipeline YAML using all variables
- 🔹 A comparison table for Java vs Node vs Python

Just tell me! 🎉
