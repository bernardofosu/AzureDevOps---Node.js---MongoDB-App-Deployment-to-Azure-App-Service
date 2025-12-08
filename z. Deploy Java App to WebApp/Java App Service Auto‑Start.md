# ☕️ Java App Service Auto‑Start Explained (Azure) 🚀

This document explains **why your Java App on Azure App Service runs even without a Startup Command or Runtime Stack configured**, and what happens behind the scenes. 👇

---

## 🔥 1. Why Your Java App Runs Without a Startup Command

Azure App Service for **Java on Linux** includes a **built‑in Java runtime** and a **built‑in startup process**.

When you deploy a `.jar` file, Azure automatically:

1. Detects that you uploaded a Java JAR file 📦
2. Uses its internal command:

   ```sh
   java -jar yourfile.jar
   ```

3. Starts the Spring Boot or Java application automatically 🚀

💡 **So even if you do NOT configure any Startup Command, Azure knows how to start your JAR.**

---

## ⚙️ 2. Why You Didn’t Need to Choose a Runtime Stack

For Java apps, Azure App Service automatically uses:

- The **default Java version** installed on the Web App
- The **default Tomcat / Java environment**

Because you deployed a Spring Boot JAR (not a WAR for Tomcat), Azure knows:

👉 "Run this as a standalone Java app using the built‑in Java runtime."

So, no manual runtime selection is needed. 🔥

---

## 🧪 3. How Azure Automatically Starts Your Java App

Behind the scenes, Azure runs something like:

```sh
java -cp /home/site/wwwroot/app.jar:azure.appservice.lib \
     -Duser.dir=/home/site/wwwroot \
     -Dserver.port=80 \
     org.springframework.boot.loader.JarLauncher
```

This explains why:

- Your app starts on **port 80** 🌐
- **Spring Boot logs** appear in `/home/LogFiles/Application/*` 📝

---

## 🕵️ 4. How to Check If the Java App Is Running

From App Service SSH:

```sh
ps aux | grep java
```

If you see something like this:

```
java -cp /home/site/wwwroot/secretsanta-0.0.1-SNAPSHOT.jar ...
```

🎉 **Your Java process is running correctly.**

---

## 🛑 5. How to Stop the Java App

Azure App Service runs Java inside a sandbox and you cannot stop the main process manually.
But you CAN:

### ✔ Restart the entire App Service

From portal:

- **Restart → App Service** 🔄

### ✔ Restart from SSH

```sh
kill -9 <PID>
```

⚠️ Azure will immediately restart it again.

---

## 🧹 6. How to Delete Only the `.jar` File

From SSH:

```sh
cd /home/site/wwwroot
rm -f *.jar
```

This removes only the JAR file but keeps the rest of your folders (logs, etc.).

---

## 🎯 Summary

| Feature         | Behavior                                       |
| --------------- | ---------------------------------------------- |
| Startup Command | ❌ Not needed for JAR apps                     |
| Runtime Stack   | ❌ Not required for standalone Spring Boot JAR |
| Auto‑Detection  | ✔ Azure sees the JAR and auto‑runs it          |
| Java Process    | ✔ Can be checked with `ps aux`                 |
| Stop App        | 🔄 Restart App Service                         |
| Delete JAR      | 🗑 `rm -f *.jar`                                |

---

If you want, I can also add:

- ⭐ Notes for **WAR deployment (Tomcat)**
- 🐳 Notes for **running Java in a Docker container**
- 🔐 Connecting Java App to Azure MySQL/PostgreSQL

Just tell me! 😄
