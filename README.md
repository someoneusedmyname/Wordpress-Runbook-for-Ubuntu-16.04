# Wordpress-Runbook-for-Ubuntu-16.04
A complete copy &amp; paste command line install for apache2, mysql, php &amp; Wordpress on Ubuntu 16.04

## Step 1 - Logging In, Getting Updated & Installing Apache2

ssh your-user@your.ip.goes.here -p 443 (443 is used for public wifi, genereally is would be "-p 22")

1.1 Procede to next step after copying & pasting the code below:

```
sudo apt-get update && sudo apt-get upgrade && sudo apt-get install apache2 && systemctl status apache2
```
1.2a Enter the root user password, (stuff will load),

1.2b Do you want to continue? [Y/n] enter "y", (stuff will load),

1.2c Do you want to continue? [Y/n] enter "y", (stuff will load),

1.2d Then press "ctrl + c", you should see "active (running)" in green text.

1.2e Right click on the link and open in a new tab: http://167.114.55.93 to check for apache2 home page.

## Step 2 - mySQL install

2.1 Copy & paste the code below:

```
sudo apt-get install mysql-server 
```
2.2a Do you want to continue? [Y/n] enter "y"

2.2b Purple screen --> enter a new password, re-enter password to confirm.

## Step 3 - Install PHP

3.1 Copy & paste the code below:

```
sudo apt-get install php7.0 libapache2-mod-php7.0 php7.0-mysql php7.0-curl php7.0-mbstring php7.0-gd php7.0-xml php7.0-xmlrpc php7.0-intl php7.0-soap php7.0-zip

```
	
3.2 Do you want to continue? [Y/n] enter "y".

```
sudo nano /var/www/html/info.php 
```

3.3 Copy and paste this text into the file editor window:

```
<?php
phpinfo();
?>
```

3.4 Now press: "ctrl + o", press enter to write file, then "ctrl + x" to exit.

3.5 Right click on the link and open in a new tab: http://167.114.55.93/info.php to check for the php test page.

## Step 4 - Install WordPress

4.1 Copy & paste the code below:
```
cd /var/www/html && sudo wget -c http://wordpress.org/latest.tar.gz && sudo tar -xzvf latest.tar.gz
```
4.2 enter the root user password

5.2 sudo wget -c http://wordpress.org/latest.tar.gz

5.3 sudo tar -xzvf latest.tar.gz

4.3 Copy & paste the code below(setting permissions):
```
sudo chown -R www-data:www-data /var/www/html/wordpress
```
## Step 5 - Creating Database in mySQL>>>

5.1 Copy & paste the code below to enter into mySQL:
```
sudo mysql -u root -p 
```

5.2 Enter database password from step 2.2b

5.3 Copy & paste the code below, but replace the text in 'quotes' with the names you want.(i.e. 'wordpress_db' is replaced with 'myfirstwordpress_db'). The text in quotes is needed later, so make sure you have it recorded somewhere.

```
CREATE DATABASE wordpress_db; GRANT ALL PRIVILEGES ON wordpress_db.* TO 'wordpress_user'@'localhost' IDENTIFIED BY 'PASSWORD'; FLUSH PRIVILEGES; exit;
```
The database name will be used in the next command below.


**(wordpress_db, 'wordpress_user', 'PASSWORD', should be changed to something of your choice)**

```
mv wp-config-sample.php wp-config.php 
```
(make sure you are here:  /var/www/html/wordpress, you may need to enter "cd wordpress")
```
sudo nano wp-config.php
```

// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define('DB_NAME', 'wordpress_db');                (your database name)

/** MySQL database username */
define('DB_USER', 'wordpress_user');              (your username)

/** MySQL database password */
define('DB_PASSWORD', 'PASSWORD');                (your password)

--> "CTRL + O" to write file, press enter, then "CTRL + X" to exit

```
systemctl restart apache2 && systemctl restart mysql
```
6.6 Enter the root user password, you'll be asked twice




now visit http://167.114.55.93/wordpress to finish wordpress install


/////////////////////////////////////////////////////////////////////////////
