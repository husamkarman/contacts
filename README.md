# contacts

✅ Summary of Requirements
Here's a quick breakdown to confirm we're aligned before I generate the PHP code:

📁 File Handling
Accept .xls, .xlsx, and .csv files.

First row is always the header.

If multiple sheets: list sheet names and allow user to select one.

Skip empty and duplicate rows (based on EMAIL and FULL NAME).

At the end, report:

Number of inserted rows.

Number of empty rows.

Number of duplicated rows.

🧠 Logic & Mapping
If column names match, map all columns.

Notify the user of any Excel columns that do not exist in DB.

Create table contacts if not exists with specified schema.

Use MySQL via PDO.

If table exists: insert only new records.

🌐 Web Interface
Form-based upload on a webpage.

Perform file validation (extension, size).

Handle temporary storage.

⚠️ Error Handling
Log errors: failed inserts, validation issues.

Provide a summary report after upload.

💻 Environment
Plain PHP (no framework).

MAMP + VS Code.

Add installation/setup instructions.

✅ What’s Next
I’ll now prepare:

PHP Script for Frontend Upload Form

PHP Backend Script for:

Handling file upload & validation

Reading Excel/CSV

Creating table if not exists

Inserting data with duplicate detection

Logging/reporting

MySQL Table Schema

Installation Notes (MAMP + VS Code)

List of PHP Extensions and Composer Packages Required
