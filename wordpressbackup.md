# WordPress Website Backup Procedure

## 1. Database Backup

- Access your MySQL database using a tool like phpMyAdmin or the command line.
- Export the database to a SQL file using the following command:
Connect to MariaDB database server.

```bash
mysql -u wp_user -p -e "SHOW DATABASES;"
```
```bash
sudo mysqldump -u root -p wp_db > backup.sql
```

- Replace "username" with your MySQL username.
- Replace "dbname" with your WordPress database name.

## 2. WordPress Files Backup

- Connect to your VPS via SSH.
- Navigate to your WordPress installation directory. Usually under `/var/www/html/` or `/var/www/`.
```bash
cd /var/www/html/
ll
```
```bash
cd
```
- Create a compressed archive of all your WordPress files using the command:
```bash
tar -czvf cangku_wp_backup.tar.gz /var/www/html/wordpress
```

- Replace "/var/www/html/wordpress" with the actual path to your WordPress files.

## 3. Transfer Backups

- Download the SQL dump and the compressed file to your local machine using secure methods like SCP or SFTP.
```bash
/Users/mikeng/Documents/apps/google-cloud-sdk/bin/gcloud compute scp mikeng@wpfairprice:/home/mikeng/backup.sql /Users/mikeng/Downloads
```
```bash
scp -i /Users/mikeng/.ssh/ssh-key-2024-01-14.key ubuntu@wordpress.com:/home/ubuntu/cangku_wp_backup.tar.gz /Users/mikeng/Downloads/
```

## 4. Verify Backups

- Before proceeding, ensure that your backups are complete and can be restored. Test the database backup by importing it into a test database.

## 5. Automate the Backup Process (Optional)

- Set up automated backups using tools like cron jobs. Schedule regular backups to ensure your data is always up to date.

## 6. Backup Storage

- Store your backups in a secure location. Consider using cloud storage, an external server, or another secure location separate from your VPS.

## 7. Document Your Backup Procedure

- Keep documentation of the backup process, including the steps taken and any relevant information. This will be useful in case you need to restore your website.
