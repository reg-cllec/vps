# Restore WordPress Database from Backup

## 1. Access MySQL Server

Log in to your MySQL server using the command line. You will be prompted to enter your MySQL user password.

```
mysql -u root -p
```

Replace `username` with your MySQL username.

## 2. Create a New Database (Optional)

If you want to restore your backup to a new database, you can create one:

```sql
CREATE DATABASE wp_db;
```

Replace `new_database_name` with the desired name for your new database.

## 3. Select the Database

Switch to the database where you want to restore your backup:

```sql
USE wp_db;
```

Replace `database_name` with the name of the database you want to use.

## 4. Restore Database from Backup

Run the following command to restore the database from your backup file:

```
mysql -u wp_user -p wp_db < /Users/mikeng/Documents/website/uscangku/backup/20240125/backup.sql
```

Replace:
- `username`: Your MySQL username.
- `database_name`: The name of the database you want to restore to.
- `/path/to/backup.sql`: The full path to your backup file (`backup.sql`).

### Example:

```
mysql -u root -p wp_db < /path/to/backup.sql
```

## 5. Verify the Restoration

Log in to MySQL again and check if the tables and data have been successfully restored:

```
mysql -u root -p
USE wp_db;
SHOW TABLES;
```

Replace `username` and `database_name` with your MySQL username and the name of your database.

That's it! Your WordPress database should now be restored. Make sure to update the `wp-config.php` file in your WordPress installation directory with the correct database credentials if needed.
