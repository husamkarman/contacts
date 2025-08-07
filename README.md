# contacts

📌 Project overview

📁 Features

⚙️ Installation instructions (MAMP + VS Code)

📜 MySQL table schema

💡 PHP dependencies

🚀 Usage steps

📋 Post-upload report format

✅ Error handling

markdown
Copy
Edit
# 📤 Excel/CSV Contact Uploader – PHP & MySQL

A plain PHP application to upload `.xls`, `.xlsx`, or `.csv` files containing contact data into a MySQL database using **PDO**. Built for MAMP and VS Code environments.

---

## ✅ Features

### 📁 File Handling
- Accepts `.xls`, `.xlsx`, and `.csv` files.
- First row is always treated as the **header**.
- If multiple sheets exist (Excel only):
  - Display available sheet names.
  - Allow the user to select a sheet.
- Skips:
  - Empty rows.
  - Duplicate rows (based on `EMAIL` and `FULL NAME`).
- Reports summary after upload:
  - ✅ Number of inserted rows.
  - 🟡 Number of empty rows.
  - 🔁 Number of duplicated rows.

### 🧠 Logic & Column Mapping
- Maps all columns **automatically** if names match schema.
- Notifies user of **unmapped columns** (if Excel contains columns not in DB).
- Creates `contacts` table if it does not exist.
- Inserts **only new records** when table exists (based on deduplication logic).

### 🌐 Web Interface
- Simple form-based upload.
- File validation:
  - Allowed extensions: `.xls`, `.xlsx`, `.csv`
  - Max size (configurable)
- Uses PHP's temporary storage for upload processing.

### ⚠️ Error Handling
- Logs:
  - Failed inserts
  - Validation issues
- Displays a full **summary report** after upload:
  - Inserted / Duplicate / Skipped Rows
  - Errors (if any)

---

## 📊 MySQL Table Schema (`contacts`)

```sql
CREATE TABLE IF NOT EXISTS contacts (
  ID INT AUTO_INCREMENT PRIMARY KEY,
  DATA_SOURCE VARCHAR(255),
  EMAIL VARCHAR(255),
  FULL_NAME VARCHAR(255),
  FIRST_NAME VARCHAR(255),
  MIDDLE_NAME VARCHAR(255),
  LAST_NAME VARCHAR(255),
  PROFESION VARCHAR(255),
  DATE_OF_BIRTH DATE,
  GENDER VARCHAR(20),
  PROFILE_PICTURE VARCHAR(255),
  NATIONALITY VARCHAR(100),
  RESIDANT_COUNTRY VARCHAR(100),
  RESIDANT_STATE VARCHAR(100),
  RESIDANT_CITY VARCHAR(100),
  PHYSICAL_ADRESS TEXT,
  PREFERED_LANGUAGE VARCHAR(100),
  PHONE_NUMBER_COUNTRY_CODE INT,
  PHONE_NUMBER BIGINT,
  WHATSAPP_COUNTRY_CODE INT,
  WHATSAPP_NUMBER BIGINT,
  FACEBOOK VARCHAR(255),
  INSTAGRAM VARCHAR(255),
  X VARCHAR(255),
  YOUTUBE VARCHAR(255),
  TELEGRAM VARCHAR(255),
  SNAPCHAT VARCHAR(255),
  EMAIL_STATUS VARCHAR(50),
  FULL_NAME_STATUS VARCHAR(50),
  EMAIL_DUPLICATES BOOLEAN,
  EMAIL_DUPLICATES_COUNT INT,
  FULL_NAME_DUPLICATES BOOLEAN,
  FULL_NAME_DUPLICATES_COUNT INT,
  BLACKLIST BOOLEAN,
  BLACKLIST_COUNT INT,
  NAME_LANGUAGE VARCHAR(50),
  NAME_FORMAT VARCHAR(50)
);
💻 Environment Setup
📦 Prerequisites
PHP 8.x

MySQL (via MAMP)

VS Code

🛠 Installation Steps
Clone the Repository

bash
Copy
Edit
git clone https://github.com/your-username/contact-uploader.git
Move to MAMP's htdocs Folder

bash
Copy
Edit
mv contact-uploader /Applications/MAMP/htdocs/
Start MAMP & Create Database

Create a new MySQL database (e.g., contacts_db).

Update DB credentials in config.php.

Install PHP Extensions (if not enabled)

Enable these PHP extensions in php.ini:

pdo_mysql

fileinfo

mbstring

zip

xml

curl

Install Required Composer Packages

bash
Copy
Edit
composer require phpoffice/phpspreadsheet
🚀 How to Use
Navigate to:

arduino
Copy
Edit
http://localhost/contact-uploader/index.php
Upload your .xls, .xlsx, or .csv file.

If multiple sheets: select one.

Submit and review the summary report.

📋 Summary Report Format (Sample Output)
pgsql
Copy
Edit
✅ Inserted Rows: 158  
🟡 Empty Rows Skipped: 12  
🔁 Duplicates Skipped: 7  
❗ Columns not mapped to DB: ['Unmapped Column A', 'RandomField']
📁 Log File: /logs/upload_2025-08-07.log
🧾 Logging
Logs are saved per upload in /logs/.

Includes:

Timestamp

Failed rows with reasons

Skipped entries

🤝 License
MIT License. Feel free to modify and use for any purpose.

👨‍💻 Author
Husam Addin Karman
tkif.org | @hkarman

vbnet
Copy
Edit

Let me know if you’d like this as a downloadable file or bundled with the actual PHP scripts you're working on.








Ask ChatGPT

