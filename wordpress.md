# Clean Reinstallation of WordPress

## Backup Your Website

Before proceeding with any changes, ensure you have a backup of your website, particularly the database, to restore your site in case of any mishaps.

## Access MySQL to Delete Database

1. Log in to MySQL using the command-line:
    ```bash
    mysql -u root -p
    ```

2. List all databases:
    ```sql
    SHOW DATABASES;
    ```

3. Identify and select your WordPress database.

4. Delete the WordPress database (replace `your_database_name` with your database's name):
    ```sql
    DROP DATABASE your_database_name;
    ```

5. Exit MySQL:
    ```sql
    EXIT;
    ```

## Delete WordPress Files

1. Navigate to the directory where WordPress resides on your server.
2. Remove all WordPress files and directories, excluding custom directories like `wp-content`.

## Reinstall WordPress

1. Download the latest version of WordPress from the [official website](https://wordpress.org/download/).
2. Upload the WordPress files to your server using FTP or another method.
3. Create a new MySQL database and user for WordPress. Make a note of the database name, username, and password.
4. Access your domain in a web browser to initiate the WordPress installation.
5. Follow the on-screen instructions, providing the database details when prompted.

## Restore Your Content (if required)

If you have a backup of your WordPress content, follow these steps:

1. Import your backup using appropriate methods to restore your posts, pages, media, etc., ensuring you don't overwrite the newly installed content.

## Secure Your Website

After reinstallation, prioritize the security of your website:

- Remove default themes or unused plugins.
- Install security plugins such as Wordfence or Sucuri Security.
- Regularly update WordPress, themes, and plugins.
- Enforce strong passwords for all user accounts.
