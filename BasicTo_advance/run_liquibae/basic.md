## for intellige idea :
select Maven project :

<img width="1904" height="1015" alt="image" src="https://github.com/user-attachments/assets/dd6d6d1a-2ca4-4100-a89e-8c40982972be" />

### setup 
```
তোমার validate ছিল:

liquibase:validate -Pdev -Dliquibase.password=${env.DB_PASSWORD}

👉 এখন update হবে:

liquibase:update -Pdev -Dliquibase.password=${env.DB_PASSWORD}
```
-----------------for run powershell----------------------
## for powersell
## for validate
```
Basic validate command
mvn liquibase:validate "-Dliquibase.password=$env:DB_PASSWORD"
🚀 2. Full recommended (with profile)

যদি তুমি dev profile use করো:

mvn liquibase:validate -Pdev "-Dliquibase.password=$env:DB_PASSWORD"
🔐 3. First set password (if not set)
$env:DB_PASSWORD="SB5leEsp4"
⚡ 4. One-line safe command
$env:DB_PASSWORD="SB5leEsp4"; mvn liquibase:validate -Pdev "-Dliquibase.password=$env:DB_PASSWORD"
```
### for Run
```
PS D:\CBS_BULK_UPLOAD_DEV\liquibase-bulk> $env:DB_PASSWORD="SB5leEsp4"
mvn liquibase:update "-Dliquibase.password=$env:DB_PASSWORD"
```
### BEST PRACTICE (more stable)
```
Option A — one line (clean)
$env:DB_PASSWORD="SB5leEsp4"; mvn liquibase:update "-Dliquibase.password=$env:DB_PASSWORD"
```
### iquibase Production Safe Workflow
```
1️⃣ VALIDATE (safety check)

👉 আগে নিশ্চিত হও সব ঠিক আছে (no DB change)

mvn liquibase:validate -Pdev "-Dliquibase.password=$env:DB_PASSWORD"
✔ What it does:
XML / YAML syntax check
duplicate changeset check
file reference check
context/profile check

❌ DB change করে না

2️⃣ UPDATE SQL (DRY RUN / preview)

👉 এখানে Liquibase আসল SQL generate করবে

mvn liquibase:updateSQL -Pdev "-Dliquibase.password=$env:DB_PASSWORD"
✔ What it does:
actual SQL script তৈরি করে
কোন changes execute হবে সেটা দেখায়
DB change করে না

👉 Output example:

-- Changeset 001
ALTER TABLE customer ADD age NUMBER;
🔥 PRO TIP (very important)

👉 এটা production এ mandatory step
👉 DBA/DevOps আগে SQL review করে approve করে

3️⃣ UPDATE (real execution)

👉 সব OK হলে actual DB change run করবে

mvn liquibase:update -Pdev "-Dliquibase.password=$env:DB_PASSWORD"
✔ What it does:
changeset execute করে
DATABASECHANGELOG update করে
lock acquire/release করে
🧠 Complete Flow (best practice)
validate
   ↓
updateSQL
   ↓
review SQL (manual / DBA)
   ↓
update
```
### One-line PowerShell safe workflow example
```

$env:DB_PASSWORD="SB5leEsp4";
mvn liquibase:validate -Pdev "-Dliquibase.password=$env:DB_PASSWORD";
mvn liquibase:updateSQL -Pdev "-Dliquibase.password=$env:DB_PASSWORD";
mvn liquibase:update -Pdev "-Dliquibase.password=$env:DB_PASSWORD"
📊 Summary

👉 validate = check
👉 updateSQL = preview
👉 update = apply\
```
## Liquibase Rollback Strategy (Production Safe)
```
Liquibase এ rollback করার 2টা main approach আছে:

1️⃣ TAG-BASED ROLLBACK (BEST PRACTICE ⭐)

👉 এটা সবচেয়ে safe এবং production standard

🏷️ Step 1: Before deployment tag দাও
mvn liquibase:tag -Dliquibase.tag=v1.0.0 -Pprod "-Dliquibase.password=$env:DB_PASSWORD"

👉 মানে: এই point কে “safe restore point” হিসেবে mark করা হলো

🚀 Step 2: New release deploy করো
mvn liquibase:update -Pprod "-Dliquibase.password=$env:DB_PASSWORD"
💥 Step 3: সমস্যা হলে rollback to tag
mvn liquibase:rollback -Dliquibase.tag=v1.0.0 -Pprod "-Dliquibase.password=$env:DB_PASSWORD"
✔ What happens:
DB আগের safe state এ ফিরে যাবে
latest changeset rollback হবে
DATABASECHANGELOG update হবে
2️⃣ COUNT-BASED ROLLBACK (Emergency quick fix)

👉 যখন tag নেই বা দ্রুত rollback দরকার

🔄 Example: last 2 changes rollback
mvn liquibase:rollbackCount -Dliquibase.rollbackCount=2 -Pprod "-Dliquibase.password=$env:DB_PASSWORD"
✔ Use case:
last deployment broken
quick recovery needed
no tagging available
3️⃣ DATE-BASED ROLLBACK (rare use)
mvn liquibase:rollbackToDate -Dliquibase.rollbackToDate="2026-05-20T10:00:00" -Pprod "-Dliquibase.password=$env:DB_PASSWORD"
🚨 Production Best Strategy (REAL WORLD)
1. tag release (v1.0.0)
2. deploy update
3. monitor
4. if issue → rollback to tag
🧠 Why TAG rollback is BEST?

✔ precise control
✔ safe restore point
✔ audit-friendly
✔ no guessing (unlike rollbackCount)

⚠️ Important Notes
rollback works only if:
changeset has rollback logic OR
Liquibase can auto-generate rollback
Always test rollback in DEV first
```
##  🔥 Pro Production Pattern
```
# 1. Tag before release
mvn liquibase:tag -Dliquibase.tag=release_2026_05_23_v1.0.0 -Pprod

# 2. Deploy
mvn liquibase:update -Pprod

# 3. Emergency rollback
mvn liquibase:rollback -Dliquibase.tag=release_2026_05_23_v1.0.0 -Pprod
🚀 Summary
```

👉 tag rollback = safest (recommended)
👉 rollbackCount = quick emergency fix
👉 rollbackToDate = time-based recovery
