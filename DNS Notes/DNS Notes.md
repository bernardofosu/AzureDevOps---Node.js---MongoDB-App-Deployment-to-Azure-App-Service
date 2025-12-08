# 🌐 DNS Notes: CNAME, A Records & nslookup Usage

---

## 🔵 1. What a CNAME Record Is

A **CNAME (Canonical Name Record)** maps your **custom domain** ➝ **another domain name**.

### ✅ Example:

```
www.mywebsite.com  ➝  myapp.azurewebsites.net
```

### ⭐ Key Points:

* CNAME **cannot** point to an IP address.
* It **must** point to another **hostname/domain**.
* DNS automatically resolves the IP in the background.

---

## 🟢 2. What an A Record Is

An **A Record** maps your domain ➝ **a fixed IPv4 address**.

### ✅ Example:

```
@ (root domain)  ➝  52.228.12.45
```

### ⭐ When to use A Record:

* When Azure gives you a **static IP** (Dedicated/Standard/Premium App Service Plan).
* When setting up **root domain** (example.com) because CNAME cannot be used at root unless using ANAME/ALIAS.
* When configuring **firewalls**, **reverse proxies**, or **third‑party load balancers**.

---

## 🟣 3. How nslookup Works

`nslookup` is used to resolve a **hostname** → **IP**.

### ❌ Wrong:

```
nslookup https://myapp.azurewebsites.net/
```

Because nslookup **cannot** process `https://` or `/`.

### ✅ Correct:

```
nslookup myapp.azurewebsites.net
```

### Example Output:

```
Non-authoritative answer:
Name: waws-prod-blu-123.azurewebsites.net
Address: 52.228.xx.xx
```

---

## 🟡 4. Azure App Service — Why IP May Be Shared

Azure App Service uses a **shared load balancer** unless you're on:

* Standard Plan ⭐
* Premium Plan ⭐⭐
* Isolated/ASE ⭐⭐⭐

So:

* Your Web App **may not have a unique IP**.
* Backend IPs can change.
* This is why **CNAME is recommended** for WebApps.

---

## 🔴 5. Testing Your App Using Its IP (Important!)

Azure App Service **requires the Host header**.

Direct IP access:

```
http://52.228.xx.xx
```

Will ❌ NOT load your app.

### ✔ Must send Host header:

```
curl -H "Host: myapp.azurewebsites.net" http://52.228.xx.xx
```

Because Azure routes websites based on **hostname**, not IP.

---

## 🟤 6. When to Use CNAME vs A Record

### ✔ Use **CNAME** for:

* `www.yourdomain.com`
* `app.yourdomain.com`
* When hosting App Service on **shared infrastructure**

### ✔ Use **A Record** for:

* `yourdomain.com` (root domain)
* When you have a **static IP**
* When firewalls need **an IP allowlist**

---

## 🧭 7. Example DNS Setup for Azure Web App

### 🌍 Host Azure App URL:

```
myapp.azurewebsites.net
```

### 🟦 CNAME Record:

```
www → myapp.azurewebsites.net
```

### 🟥 A Record (only if you have Static IP):

```
@ → 52.228.xx.xx
```

---

## 🎉 Summary (Easy to Remember)

* 🔹 CNAME → Points to a domain
* 🔹 A Record → Points to an IP
* 🔹 nslookup needs hostname only
* 🔹 Azure WebApps usually require CNAME
* 🔹 Root domain needs A Record unless DNS supports ALIAS/ANAME

---

If you want, I can add:
✨ A visual diagram (DNS → Azure Load Balancer → Web App)
✨ Step-by-step instructions for Azure Custom Domains
✨ Cloudflare DNS automation notes
