# 💼 Azure DevOps Agent Working Directory Explained (with Emojis)

When you run pipelines on a **self‑hosted Azure DevOps agent**, the agent creates structured folders inside:

```
~/myagent/_work/
```

Each pipeline job gets its own workspace such as **1**, **2**, **3**, etc.

Below is the full explanation of what **1, 2, a, b, s** contain inside the working directory.

---

## 🔵 1️⃣ & 2️⃣ — Job Workspaces

These are folders automatically created for each pipeline run.

### 📌 Meaning:

- **1/** → Workspace for Job Run #1
- **2/** → Workspace for Job Run #2

Each workspace contains subfolders used during execution.

Structure example:

```
_work/
 ├── 1/
 │   ├── a/
 │   ├── b/
 │   └── s/
 ├── 2/
     ├── a/
     ├── b/
     └── s/
```

---

## 🟢 a/ — Artifact Staging Directory

**a = Artifacts**

This folder contains files that will be packaged or published.

### 📦 Contains:

- ZIP files (example: `output-82.zip`)
- Files copied using `CopyFiles@2`
- Build outputs prepared for `PublishPipelineArtifact`

Example content:

```
output.zip
static files
copied build assets
```

Emoji summary: 🧳📦🚚

---

## 🟡 b/ — Build Output Directory

**b = Build binaries**

This folder stores the compiled output from your build.

### ⚙️ Contains:

For Node.js:

- `node_modules/`
- transpiled/processed JS files

For Java (Maven):

- `target/`
- `.class`, `.jar` files

Emoji summary: 🛠️⚗️🏗️

---

## 🔵 s/ — Source Directory

**s = Source code**

This is where Azure DevOps downloads your repository.

### 📁 Contains:

Your entire repo, such as:

```
app.js
package.json
routes/
models/
views/
azure.yaml
az-pipeline.yaml
output-82.zip (if generated in repo)
```

Emoji summary: 📂🧩📝

---

## 🧠 Quick Summary Table

| Folder | Meaning          | What It Contains                  |
| ------ | ---------------- | --------------------------------- |
| **1/** | Job #1 workspace | All files for pipeline job 1      |
| **2/** | Job #2 workspace | All files for pipeline job 2      |
| **a/** | Artifact staging | ZIPs, build outputs to publish    |
| **b/** | Build directory  | Compiled output / built artifacts |
| **s/** | Source directory | Git repo files                    |

---

## ⭐ Final Explanation

Every time a pipeline runs:

- Azure DevOps creates a numbered folder (**1, 2, 3…**)
- Inside it, the agent splits the work into:

  - **s/** → download source
  - **b/** → build output
  - **a/** → artifacts staging

This keeps jobs isolated and clean. Workflow emojis: 🧹⚙️📦🚀

---

If you want, I can also:
✨ Draw a visual diagram
✨ Explain cleanup policies
✨ Show how to safely delete `_work` folders
✨ Document this for training materials

Just tell me! 😄
