# contacts

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
```

---

## 💻 Environment Setup

### 📦 Prerequisites
- PHP 8.x
- MySQL (via MAMP)
- VS Code

### 🛠 Installation Steps

1. **Clone the Repository**
   ```bash
   git clone https://github.com/your-username/contact-uploader.git
   ```

2. **Move to MAMP's `htdocs` Folder**
   ```bash
   mv contact-uploader /Applications/MAMP/htdocs/
   ```

3. **Start MAMP & Create Database**
   - Create a new MySQL database (e.g., `contacts_db`).
   - Update DB credentials in `config.php`.

4. **Install PHP Extensions (if not enabled)**

   Enable these PHP extensions in `php.ini`:
   - `pdo_mysql`
   - `fileinfo`
   - `mbstring`
   - `zip`
   - `xml`
   - `curl`

5. **Install Required Composer Packages**
   ```bash
   composer require phpoffice/phpspreadsheet
   ```

---

## 🚀 How to Use

1. Navigate to:
   ```
   http://localhost/contact-uploader/index.php
   ```

2. Upload your `.xls`, `.xlsx`, or `.csv` file.

3. If multiple sheets: select one.

4. Submit and review the **summary report**.

---

## 📋 Summary Report Format (Sample Output)

```
✅ Inserted Rows: 158  
🟡 Empty Rows Skipped: 12  
🔁 Duplicates Skipped: 7  
❗ Columns not mapped to DB: ['Unmapped Column A', 'RandomField']
📁 Log File: /logs/upload_2025-08-07.log
```

---

## 📑 Field Definitions

| **Field Name**            | **Data Type**       | **Description / Notes**                       |
| ------------------------- | ------------------- | --------------------------------------------- |
| ID                        | `INTEGER` or `UUID` | Unique identifier for each record.            |
| DATA SOURCE               | `VARCHAR`           | Text source identifier (e.g., "form", "CRM"). |
| EMAIL                     | `VARCHAR`           | Valid email address.                          |
| FULL NAME                 | `VARCHAR`           | Full name string.                             |
| FIRST NAME                | `VARCHAR`           | First name only.                              |
| MIDDLE NAME               | `VARCHAR`           | Middle name (optional).                       |
| LAST NAME                 | `VARCHAR`           | Last name only.                               |
| PROFESION                 | `VARCHAR`           | Job title or occupation.                      |
| DATE OF BIRTH             | `DATE`              | Format: `YYYY-MM-DD`.                         |
| GENDER                    | `VARCHAR`           | e.g., 'Male', 'Female', 'Other'.              |
| PROFILE PICTURE           | `VARCHAR (URL)`     | Link to profile image.                        |
| NATIONALITY               | `VARCHAR`           | Country of citizenship.                       |
| RESIDANT COUNTRY          | `VARCHAR`           | Country of residence.                         |
| RESIDANT STATE            | `VARCHAR`           | State or province.                            |
| RESIDANT CITY             | `VARCHAR`           | City of residence.                            |
| PHYSICAL ADRESS           | `TEXT`              | Full postal/mailing address.                  |
| PREFERED LANGUAGE         | `VARCHAR`           | Preferred communication language.             |
| PHONE NUMBER COUNTRY CODE | `INTEGER`           | Numeric only (e.g., 1, 44, 966).              |
| PHONE NUMBER              | `BIGINT`            | Use `BIGINT` to handle long phone numbers.    |
| WHATSAPP COUNTRY CODE     | `INTEGER`           | Numeric only (no `+` prefix).                 |
| WHATSAPP NUMBER           | `BIGINT`            | WhatsApp phone number.                        |
| FACEBOOK                  | `VARCHAR (URL)`     | Facebook profile URL or handle.               |
| INSTAGRAM                 | `VARCHAR (URL)`     | Instagram profile URL or handle.              |
| X                         | `VARCHAR (URL)`     | X (formerly Twitter) profile URL or handle.   |
| YOUTUBE                   | `VARCHAR (URL)`     | YouTube channel or profile URL.               |
| TELEGRAM                  | `VARCHAR (URL)`     | Telegram handle or link.                      |
| SNAPCHAT                  | `VARCHAR`           | Snapchat username.                            |
| EMAIL STATUS              | `VARCHAR`           | Status like 'Valid', 'Bounced', etc.          |
| FULL NAME STATUS          | `VARCHAR`           | e.g., 'Complete', 'Incomplete'.               |
| EMAIL DUPLICATES          | `BOOLEAN`           | `TRUE` if email is duplicated.                |
| # EMAIL DUPLICATES        | `INTEGER`           | Number of email duplicates.                   |
| FULL NAME DUPLICATES      | `BOOLEAN`           | `TRUE` if name is duplicated.                 |
| # FULL NAME DUPLICATES    | `INTEGER`           | Number of full name duplicates.               |
| BLACKLIST                 | `BOOLEAN`           | Whether user is blacklisted.                  |
| # BLACKLIST               | `INTEGER`           | Count of blacklist occurrences (optional).    |
| NAME LANGUAGE             | `VARCHAR`           | Language of the name (e.g., Arabic, English). |
| NAME FORMAT               | `VARCHAR`           | e.g., 'First Last', 'Last, First'.            |

---

## 🤝 License

MIT License. Feel free to modify and use for any purpose.

---

## 👨‍💻 Author

Husam Addin Karman  
[tkif.org](https://tkif.org) | `@hkarman`

