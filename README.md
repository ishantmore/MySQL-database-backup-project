# MySQL Database Management and Backup on Ubuntu

## Project Overview

This project demonstrates MySQL database administration on an Ubuntu server. It covers creating databases and tables, inserting and updating student records, modifying table structures, sorting records, and backing up database data using MySQL dump utilities.

## Objectives

- Run MySQL on a Linux-based AWS EC2 instance.
- Create and manage databases and tables.
- Insert, view, update, and sort student records.
- Add a new column to an existing table while preserving existing records.
- Export a database to an SQL backup file.
- Create a separate database and inspect the imported backup data.

## Technologies Used

- **Operating System:** Ubuntu Linux (as shown in the terminal screenshots)
- **Database:** MySQL
- **Backup utility:** `mysqldump`
- **Command line:** Linux terminal and MySQL CLI

## Architecture / Workflow

1. Open a terminal on the Ubuntu server.
2. Access the MySQL command-line client.
3. Create/select a database (`mydb`).
4. Create and manage the `students` table.
5. Insert, update, and query student records.
6. Add a `marks` column with a default value.
7. Export the database/table data to an SQL file.
8. Create a separate database (`backup_db`) and verify the `students` table and records.

## Database Schema

The `students` table contains the following columns:

| Column | Data type | Purpose |
|---|---|---|
| `roll_no` | `INT` | Student roll number |
| `name` | `VARCHAR(20)` | Student name |
| `contact_no` | `BIGINT` | Contact number |
| `city` | `VARCHAR(20)` | Student city |
| `marks` | `INT` | Student marks; default value shown as `75` |

> Note: The screenshots show the columns allowing `NULL`. The `marks` column was added after the table had already been created.

## Commands Used

### 1. Select the database and inspect the table

```sql
SHOW DATABASES;
USE mydb;
SHOW TABLES;
DESC students;
```

### 2. Insert student records

Example based on the table structure shown in the project:

```sql
INSERT INTO students (roll_no, name, contact_no, city)
VALUES (59, 'vipin', 7695885548, 'tekadi');
```

Use your own values when inserting records. Avoid publishing real personal contact numbers in a public repository.

### 3. View all records

```sql
SELECT * FROM students;
```

### 4. Add a column to an existing table

```sql
ALTER TABLE students
ADD COLUMN marks INT(3) DEFAULT 75;
```

The existing rows remain in the table. For rows where `marks` was not previously set, MySQL applies the default value when the column is added, as shown in the project screenshots.

### 5. Sort records by roll number

```sql
SELECT * FROM students
ORDER BY roll_no ASC;
```

### 6. Update a student's contact number

```sql
UPDATE students
SET contact_no = 960409716
WHERE name = 'piyush';
```

Always use a suitable `WHERE` condition when updating records. Check the target row with a `SELECT` query before running an update.

### 7. Export a database backup

The screenshots show a `mysqldump` command creating `students_backup.sql` from the `students` table:

```bash
mysqldump -u root -p mydb students > students_backup.sql
```

Enter the MySQL password when prompted. The SQL dump file contains the table definition and data needed for restoration.

### 8. Create and verify a separate database

```sql
CREATE DATABASE backup_db;
SHOW DATABASES;
```

### 9. Restore the SQL backup

If you want to restore the dump into `backup_db`, run this from the Linux shell:

```bash
mysql -u root -p backup_db < students_backup.sql
```

Then verify the restored table:

```sql
USE backup_db;
SHOW TABLES;
DESC students;
SELECT * FROM students;
```

**Important:** The screenshots show the SQL backup file being opened and `backup_db` being created, followed by verification of a `students` table and its records. The restoration command above is the standard way to import a dump into that database; adapt it to your actual file path and MySQL account.

## What I Learned

- Connecting to and managing MySQL from a Linux terminal.
- Creating databases and tables and inspecting their structure.
- Inserting, updating, selecting, and sorting records.
- Altering an existing table without recreating it.
- Creating SQL backups with `mysqldump`.
- Verifying a database backup in a separate database.

## Screenshots

Add your project screenshots to a folder named `screenshots/` in this repository. Then display them here, for example:

```markdown
![EC2 instance](screenshots/ec2-instance.png)
![Student table](screenshots/student-table.png)
![Database backup](screenshots/database-backup.png)
```

Use the actual image filenames in your repository.

## Repository Structure

```text
mysql-database-backup-aws-ec2/
├── README.md
├── students_backup.sql
└── screenshots/
    ├── ec2-instance.png
    ├── student-table.png
    └── database-backup.png
```

This is a suggested structure. Include only the files and screenshots you actually upload.

## Security Notes

- Never upload passwords, private keys, or AWS access keys to GitHub.
- Use test or anonymized data in public repositories.
- Restrict SSH access to your own IP and allow only the ports required by your setup.
- Store database backups securely; SQL dumps can contain sensitive data.

## Conclusion

This project provides practical experience with MySQL database operations and SQL backup workflows on Ubuntu. It demonstrates basic database administration tasks and how to verify data in a separate database.
