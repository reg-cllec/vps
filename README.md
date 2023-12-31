Get your Always Free Oracle Cloud Server ready
----------------------------------------------

To get your OCI server ready for hosting WordPress site you will need to complete the following steps. Log-in to your Oracle Cloud Console, launch a new instance, open ports 80 and 443 in your default security list, reserve free public IP and assign the IP to your virtual server. If you need help with any of it you can use my video tutorial above to follow along.

Create public DNS record
------------------------

The exact process in this step will depend on who your Domain Name provider is. Luckily the concept is the same, and all you need to do is create an A record that points your domain to the reserved IP you have assigned to your virtual server on Oracle Cloud. In my video tutorial I am creating a DNS record with Namecheap, the process should be similar with other providers.

Open ports 80 HTTP and 443 HTTPS in iptables
--------------------------------------------

Iptables is by default installed and active on Ubuntu server on Oracle Cloud, and you will need to take an extra step and open ports 80 and 443 on it as well. You can do it by running the following commands.

    iptables -I INPUT -p tcp -m tcp --dport 80 -j ACCEPT
    iptables -I INPUT -p tcp -m tcp --dport 443 -j ACCEPT
    iptables-save > /etc/iptables/rules.v4

Install Prerequisites (PHP, MariaDB, PHP modules, etc.)
-------------------------------------------------------

You will need to run the commands below to update your system, and install the listed packages as they are required by WordPress.

    apt update && apt -y upgrade
    apt install apache2 ghostscript libapache2-mod-php mariadb-server php php-bcmath php-curl php-imagick php-intl php-json php-mbstring  php-mysql php-xml php-zip wget unzip

Configure MariaDB Database
--------------------------

Connect to MariaDB database server.

    sudo mysql -u root -p

Once you connect successfully to the database server, create WordPress database and user. You can do it by running the following commands. Make sure to replace “password1” with better, more secure password.

    CREATE DATABASE wp_db;
    CREATE USER wp_user@localhost IDENTIFIED BY 'password1';
    GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER ON wp_db.* TO wp_user@localhost;
    FLUSH PRIVILEGES;
    quit

Install WordPress
-----------------

The next step would be to download, install, and set appropriate file permissions on latest WordPress. To do that, run the following commands.

    wget https://wordpress.org/latest.zip
    unzip latest.zip
    mv wordpress/ /var/www/html/
    chown www-data:www-data -R /var/www/html/wordpress/
    chmod -R 755 /var/www/html/wordpress/

Configure Apache Virtual Host
-----------------------------

Create new vhost in “/etc/apache2/sites-available/” by running the command below.

    nano /etc/apache2/sites-available/wordpress.conf

Add the content from the box below to your wordpress.conf make sure to replace the ServerName directive with your domain name. That will be the same name you created public record for in the “Create public DNS record” step.

    <VirtualHost *:80>
    
        DocumentRoot /var/www/html/wordpress/
        ServerName wp.techtutelage.net
    
    <Directory /var/www/html/wordpress/>
    
        Options FollowSymLinks
        AllowOverride All
        Require all granted
    
    </Directory>
    
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
    
    </VirtualHost>

Once you have you vhost file created go ahead and disable the default virtual host, enable the virtual host you just created, along with apache rewrite mode by running the following commands.

    a2dissite 000-default
    a2ensite wordpress
    a2enmod rewrite
    service apache2 reload

Complete WordPress Installation
-------------------------------

At this point you should be able to access your WordPress installation page in your web browser. Once there you can follow along the installation wizard. If you need assistance you can use my video tutorial and follow along.

Get Free Let’s Encrypt SSL Certificate
--------------------------------------

The easiest way to get free Let’s Encrypt Certificate and secure your WordPress site is to use apache plugin “python3-certbot-apache”. To get the plugin and install certificates run the following commands.

    apt install python3-certbot-apache
    certbot --apache

Follow the onscreen instructions to complete SSL certificate creation and installation.

For more details and to see this setup in action check out my video on youtube:
