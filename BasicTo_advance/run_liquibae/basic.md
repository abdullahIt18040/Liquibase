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
