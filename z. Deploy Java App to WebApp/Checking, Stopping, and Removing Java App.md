# ☕🚀 Checking, Stopping, and Removing Java App on Azure App Service

Below are the **three essential operations** you will use when managing your Java application running on Azure App Service.

---

## 🟢 **1. How to Check If the Java App Is Running**

### ✅ **A. Check running Java processes**

Run:

```
ps aux | grep java
```

👀 **If you see a Java command with your JAR file, the app is running.**

---

### ✅ **B. Check Spring Boot logs**

```
cd /home/LogFiles/Application/
cat *.log
```

📄 Look for:

- `Tomcat started on port 80`
- `Started YourApplication`

This confirms the app is healthy.

---

### ✅ **C. Test the app endpoint**

```
curl http://localhost:80
```

🌍 If you get a response → **Your app is active.**

---

## 🔴 **2. How to Stop the Java App**

Azure App Service automatically runs the Java process. You can stop it manually:

### ❌ **A. Kill the Java process**

1️⃣ First find the PID:

```
ps aux | grep java
```

Example output:

```
183 root  java ...
```

2️⃣ Kill it:

```
kill -9 183
```

💥 **This temporarily stops the Java app**, but Azure may restart it automatically.

---

### ❌ **B. Stop the whole App Service (recommended)**

Run in Azure CLI:

```
az webapp stop --name <appname> --resource-group <rgname>
```

🛑 This completely stops the web app and all processes.

---

## 🗑️ **3. How to Remove ONLY the Java File (JAR)**

Your JAR file is located here:

```
/home/site/wwwroot/
```

### ❗ Delete only the JAR file

```
cd /home/site/wwwroot
rm -f yourfile.jar
```

🧹 Removes the JAR safely without touching logs or folders.

---

## ⭐ Summary

| Action            | Command                                | Emoji      |     |
| ----------------- | -------------------------------------- | ---------- | --- |
| Check running app | `ps aux                                | grep java` | 🔍  |
| View logs         | `cat /home/LogFiles/Application/*.log` | 📄         |     |
| Test app          | `curl localhost:80`                    | 🌍         |     |
| Stop Java process | `kill -9 <PID>`                        | 🛑         |     |
| Stop app service  | `az webapp stop`                       | ⛔         |     |
| Remove JAR file   | `rm -f *.jar`                          | 🗑️         |     |

---

If you want, I can also add:
✨ Commands to restart the Java app
✨ How to redeploy a clean JAR
✨ How to automate cleanup every deployment

Just tell me! 😊
