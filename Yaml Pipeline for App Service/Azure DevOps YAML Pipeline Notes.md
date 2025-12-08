# 🚀 Azure DevOps Pipeline Notes — Steps, Jobs & Stages Explained 🎯📘

---

## 🧱 1️⃣ Pipeline Hierarchy (Most Important Rule)

Azure DevOps pipelines follow this structure:

```
Stages 🟦
   └── Jobs 🟩
        └── Steps (Tasks) 🟨
```

✔ A pipeline → has **stages**
✔ A stage → contains **jobs**
✔ A job → contains **steps** (your tasks)

---

## 🪜 2️⃣ Using ONLY `steps:` (Simple Pipelines)

If you write:

```yaml
steps:
  - task: NodeTool@0
  - task: Npm@1
  - task: CopyFiles@2
```

You did **NOT** define:

- ❌ Any stage
- ❌ Any job

So Azure creates them **automatically**.

---

## 🤖 3️⃣ What Azure Creates Automatically

Azure DevOps generates:

- **1 implicit stage**
- **1 implicit job**
- All tasks grouped under that job 🎒

Internally Azure treats your YAML as:

```yaml
stages:
  - stage: Stage_1
    displayName: "Stage 1"
    jobs:
      - job: Job_1
        displayName: "Job"
        steps:
          - task: NodeTool@0
          - task: Npm@1
          - task: CopyFiles@2
```

---

## 🏷️ 4️⃣ Default Display Names

Since you didn’t name anything:

- Stage name = **Stage 1** ⭐
- Job name = **Job** 🧩

These appear in the Azure UI.

---

## 🔁 5️⃣ Multiple Tasks ≠ Multiple Stages or Jobs

This YAML:

```yaml
steps:
  - task: A
  - task: B
  - task: C
```

Produces **ONE** stage, **ONE** job, and **THREE** steps:

```
Stage 1
  └── Job
        ├── Step A
        ├── Step B
        └── Step C
```

✔ Tasks stay within the same job.
✔ Azure never splits tasks into stages or jobs.

---

## 🚫 6️⃣ You Cannot Use Two `steps:` Blocks

Invalid:

```yaml
steps:
- task: A

steps:  # ❌ Duplicate key
- task: B
```

YAML does **not** allow duplicate `steps:` keys.
One job = one steps block only.

---

## 🧰 7️⃣ Creating Multiple Jobs (Manually)

```yaml
jobs:
  - job: Build
    steps:
      - task: NodeTool@0
      - task: Npm@1

  - job: Package
    steps:
      - task: CopyFiles@2
```

🎉 Azure shows:

- Job: Build
- Job: Package

---

## 🗂️ 8️⃣ Creating Multiple Stages (Manually)

```yaml
stages:
  - stage: Build
    jobs:
      - job: BuildJob
        steps:
          - task: NodeTool@0
          - task: Npm@1

  - stage: Package
    jobs:
      - job: PackageJob
        steps:
          - task: CopyFiles@2
```

Azure UI displays:

- Stage: Build 🟦
- Stage: Package 🟧

---

## 📝 9️⃣ Summary Table

| What You Write           | What Azure Creates       | Notes                                         |
| ------------------------ | ------------------------ | --------------------------------------------- |
| `steps:` only            | 1 stage, 1 job           | All tasks in one place ✔                      |
| `jobs:` only             | 1 stage w/ multiple jobs | Useful for parallel builds ⚡                 |
| `stages:`                | Full control             | Multi-environment or multi-phase pipelines 🌍 |
| multiple `steps:` blocks | ❌ Error                 | Only one per job                              |
| multiple tasks           | ✔ Many steps             | Still inside one job                          |

---

## 🎯 🔟 Final Understanding

### ✔ `steps:` only → **ONE stage, ONE job, MANY tasks**

### ✔ To create multiple stages → **write `stages:` explicitly**

### ✔ To create multiple jobs → **write `jobs:` explicitly**

Azure **never** creates extra stages or jobs automatically.

---

If you want, I can convert these notes into:
📄 PDF, 📝 Markdown, 🎨 formatted Canva-style designs, or 📘 a cheat sheet!
