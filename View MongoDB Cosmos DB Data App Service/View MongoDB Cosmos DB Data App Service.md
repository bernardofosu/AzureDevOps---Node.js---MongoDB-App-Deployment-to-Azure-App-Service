# 📘 Three Ways to View MongoDB / Cosmos DB Data

---

## 🔵 1. **View Data Using App Service Log Stream**

### ✔ What You See

- Database connection logs
- Tasks being added, updated, or deleted
- Console logs from your Node.js app

### ✔ How to Access

**Azure Portal → App Service → Log Stream**

### ✔ Example Output

```
Connected to database
Total tasks: 2 Current: 2 Completed: 0
Adding a new task eat...
Added new task eat
```

### ⭐ Best For

- Real‑time debugging
- Verifying deployment
- Confirming DB connectivity

---

## 🔵 2. **Query the Data Manually via App Service SSH**

### ✔ What It Is

You open the App Service container through SSH and run Node.js commands directly to inspect the database.

### ✔ How to Access

**Azure Portal → App Service → SSH**

### ✔ Command Used

```bash
node -e "
const mongoose=require('mongoose');
const uri=process.env.AZURE_COSMOS_CONNECTIONSTRING || process.env.MONGODB_URI;
mongoose.connect(uri).then(()=>{
  console.log('Connected');
  mongoose.connection.db.collection('tasks').find().toArray().then(console.log);
});
"
```

### ✔ Example Output

```
Connected
[
  { taskName: 'eat', createDate: ..., _id: ... },
  { taskName: 'dance', createDate: ..., _id: ... }
]
```

### ⭐ Best For

- Viewing raw documents
- Debugging backend logic
- Confirming environment variables are correct

---

## 🔵 3. **View Data in Azure Cosmos DB Data Explorer**

### ✔ What You See

- Databases
- Collections
- Documents
- GUI queries

### ✔ How to Access

**Azure Portal → Cosmos DB → Data Explorer**

### ✔ Query All Documents

```json
{}
```

### ⭐ Best For

- Clean UI viewing
- Editing documents visually
- Non‑technical browsing

---

# ✅ Summary Table

| Method           | Difficulty | Best For              | Notes                           |
| ---------------- | ---------- | --------------------- | ------------------------------- |
| 🔵 Log Stream    | Easy       | Real‑time debugging   | Shows app logs + DB actions     |
| 🔵 SSH Query     | Medium     | Raw DB inspection     | Works anytime, direct DB access |
| 🔵 Data Explorer | Easy       | GUI document browsing | Requires refresh sometimes      |

---

If you want, I can also create a **README.md** or **DevOps documentation** for this. 🚀
