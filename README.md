# Wordpress-Runbook-for-Ubuntu-16.04
A complete copy &amp; paste command line install for apache2, mysql, php &amp; Wordpress on Ubuntu 16.04

## Step 1 - Logging In, Getting Updated & Installing Apache2

ssh your-user@your.ip.goes.here -p 443 (443 is used for public wifi, genereally is would be "-p 22")

Procede to next step after copying & pasting the code below.

```
sudo apt-get update && sudo apt-get upgrade && sudo apt-get install apache2 && systemctl status apache2
```
-Enter the root user password, (stuff will load),

-Do you want to continue? [Y/n] enter "y", (stuff will load),

-Do you want to continue? [Y/n] enter "y", (stuff will load),

-Then press "ctrl + c", you should see "active (running)" in green text.

-Check 167.114.55.93 for apache2 home page

## Step 2 - mySQL install

Copy & paste the code below:

```
sudo apt-get install mysql-server 
```
Do you want to continue? [Y/n] enter "y"

3.2 purple screen --> enter a new password, re-enter password to confirm (i used "mypassword")

-might need this? sudo service mysql restart??

(enter the root user password, in this case its mine)

## Step 3 - Install PHP

Copy & paste the code below:

```

4.1 sudo apt-get install php7.0 libapache2-mod-php7.0 php7.0-mysql php7.0-curl php7.0-mbstring php7.0-gd php7.0-xml php7.0-xmlrpc php7.0-intl php7.0-soap php7.0-zip

```
	
 (enter root user password)?? --> (Do you want to continue? [Y/n] enter "y")

4.2 sudo nano /var/www/html/info.php 

4.3 copy and paste this text into the file editor window:
```
<?php
phpinfo();
?>
```

then, "ctrl + o", press enter to write file, then "ctrl + x" to exit

4.4 systemctl restart apache2 (enter the root user password, in this case its mine)

checking for the php test page, visit: http://167.114.55.93/info.php

<<<Install WordPress>>>

5.1 cd /var/www/html

5.2 sudo wget -c http://wordpress.org/latest.tar.gz

5.3 sudo tar -xzvf latest.tar.gz

5.4 sudo chown -R www-data:www-data /var/www/html/wordpress (setting permissions)

<<<creating database in mySQL>>>

6.1 sudo mysql -u root -p (enter database password from step 3.2)EXIT


6.2a CREATE DATABASE wordpress_db; 

6.2b GRANT ALL PRIVILEGES ON wordpress_db.* TO 'wordpress_user'@'localhost' IDENTIFIED BY 'PASSWORD'; 

*****("wordpress_db", "wordpress_user", "PASSWORD", should be changed)*****

6.2c FLUSH PRIVILEGES;

6.2d exit;

6.3 mv wp-config-sample.php wp-config.php (make sure you are here:  /var/www/html/wordpress, you may need to enter "cd wordpress")

6.4 sudo nano wp-config.php

// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define('DB_NAME', 'wordpress_db');                (your database name)

/** MySQL database username */
define('DB_USER', 'wordpress_user');              (your username)

/** MySQL database password */
define('DB_PASSWORD', 'PASSWORD');                (your password)

--> "CTRL + O" to write file, press enter, then "CTRL + X" to exit

6.5 systemctl restart apache2 (enter the root user password, in this case its mine)

6.6 systemctl restart mysql (enter the root user password, in this case its mine)




now visit http://167.114.55.93/wordpress to finish wordpress install


/////////////////////////////////////////////////////////////////////////////
