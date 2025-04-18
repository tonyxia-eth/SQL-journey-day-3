# SQL-journey-day-3
Day 3: Tracing a Package from Tileston to Maple
# 📦 SQL Journey – Day 3: Tracing a Package from Tileston to Maple

## 🔍 Objective
Today I traced a package delivery from a **Tileston Street** address to a **Maple Place** address using SQL queries on the `packages.db` database.

---

## 🧠 What I Learned
- How to find address IDs from partial street names.
- How to trace package delivery history using the `packages`, `scans`, and `addresses` tables.
- How to troubleshoot common bash and SQLite mistakes along the way.

---

## 🗂️ Step-by-Step Breakdown

### Step 1: Find Address IDs

#### 🏡 Maple Place Addresses:
```sql
SELECT * FROM addresses
WHERE address LIKE '%Maple%';
🏢 Tileston Addresses:
 


SELECT * FROM addresses
WHERE address LIKE '%Tileston%';
From these queries, I identified:

From Address ID: 9873 (109 Tileston Street)

To Address ID: 4983 (728 Maple Place)

Step 2: Look Up the Package



SELECT * FROM packages
WHERE from_address_id = 9873
  AND to_address_id = 4983;
✅ Result:


ID	Contents	From Address ID	To Address ID
9523	Flowers	9873	4983
Step 3: Trace the Package Scan History
sql
Copy
Edit
SELECT * FROM scans
WHERE package_id = 9523
ORDER BY timestamp;
✅ Result:


ID	Driver ID	Package ID	Address ID	Action	Timestamp
10432	11	9523	9873	Pick	2023-08-16 21:41:43.219831
10500	11	9523	7432	Drop	2023-08-17 03:31:36.856889
12432	17	9523	7432	Pick	2023-08-23 19:41:47.913410
Looks like it was dropped at a warehouse and later picked up again.

Step 4: Find Final Destination



SELECT * FROM addresses
WHERE id = 7432;
✅ Result:

Address: 950 Brannon Harris Way

Type: Warehouse

📝 Conclusion
The package containing flowers started at 109 Tileston Street, was initially dropped off at a warehouse (950 Brannon Harris Way), and then picked up again later — likely en route to its final destination at 728 Maple Place.

💻 Commands & Errors I Encountered (Learning Moments)
bash
Copy
Edit
$ .cd          # Incorrect command
$ cd.          # Incorrect syntax
$ cd..         # Incorrect syntax, should be 'cd ..'
$ SELECT       # SQL commands must be run within sqlite3
📅 Daily Progress
This marks Day 3 of my SQL journey. I’m getting more confident writing SQL queries, reading from multiple tables, and tracing relational data. 🚀



---

### 🧭 Uploading This to GitHub – Quick Guide

1. **Open your text editor** (VS Code, Notepad++, etc.)
   - Paste the above markdown content into a new file.
   - Save the file as: `Day_3_SQL.md`.

2. **Log in to GitHub**, and open the correct repository or create a new one (e.g., `sql-journey`).

3. Click **Add file → Upload files**.

4. Drag and drop your `Day_3_SQL.md` into the upload window.

5. Click **Commit changes** to upload.

That’s it! You now have your third daily SQL log nicely documented on GitHub. Want me to help you create
