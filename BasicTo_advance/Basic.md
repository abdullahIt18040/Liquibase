## why used liquibase

## Liquibase কী?

Liquibase হলো একটি টুল, যা ডাটাবেসের পরিবর্তন (table, column, data) সহজভাবে ম্যানেজ ও ট্র্যাক করতে সাহায্য করে।
```
🔹 কেন ব্যবহার করা হয়?
✅ 1. ডাটাবেস Version Control

যেমন Git দিয়ে কোড ম্যানেজ করা হয়,
তেমনি Liquibase দিয়ে DB change track করা হয়।

✅ 2. Automatic Update

অ্যাপ রান করলে Liquibase নিজে নিজে:

নতুন change খুঁজে বের করে
DB তে apply করে

👉 Manual SQL চালাতে হয় না

✅ 3. Duplicate Execution বন্ধ করে

একই SQL বারবার রান হয় না
👉 Liquibase নিজেই track রাখে
```
### when we are used liquibase:
```
1.DDL 
2. c data
3. data migration (data transfer from one table to another table)
Liquibase কোথায় ব্যবহার করা হয়?

Liquibase প্রধানত ৩ ধরনের কাজে ব্যবহার করা হয়:

✅ 1. DDL (Database Structure)

👉 Table, Column, Index, Constraint তৈরি/পরিবর্তন

✔ এটা Liquibase-এর মূল কাজ
✔ সবচেয়ে বেশি ব্যবহার হয়

✅ 2. Data (Insert / Seed Data)

👉 Initial বা static data insert করা

✔ যেমন:

Admin user
Role / Config data

⚠️ বড় ডেটার জন্য ব্যবহার করা ঠিক না

✅ 3. Data Migration

👉 এক টেবিল থেকে অন্য টেবিলে ডেটা নেওয়া

✔ SQL ব্যবহার করে করা যায়

⚠️ খুব বড় বা জটিল migration হলে আলাদা script/tool ভালো
```
