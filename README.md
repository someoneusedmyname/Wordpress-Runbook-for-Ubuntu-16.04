# Wordpress-Runbook-for-Ubuntu-16.04
A complete copy &amp; paste command line install for apache2, mysql, php &amp; Wordpress on Ubuntu 16.04 (This should take about 10 minutes)

## Step 1 - Logging In, Getting Updated & Installing Apache2

You will need to ssh into your Ubuntu 16.04 server before starting.

1.1 Procede to next step after copying & pasting the code below:

```
sudo apt-get update && sudo apt-get upgrade && sudo apt-get install apache2 && systemctl status apache2
```
1.2a Enter the root user password, (stuff will load),

1.2b Do you want to continue? [Y/n] enter "y", (stuff will load),

1.2c Do you want to continue? [Y/n] enter "y", (stuff will load),

1.2d Then press "ctrl + c", you should see "active (running)" in green text.

1.2e Go to: http://your.ip.address.here to check for Apache2 Ubuntu Default Page.

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

3.3 Copy and paste this text into the GNU nano 5.2.3 file editor window:

```
<?php
phpinfo();
?>
```

3.4 Now press: "ctrl + o", press enter to write file, then "ctrl + x" to exit.

3.5 Go to: http://your.ip.address.here/info.php to check for the php info page.

## Step 4 - Install WordPress

4.1 Copy & paste the code below:
```
cd /var/www/html && sudo wget -c http://wordpress.org/latest.tar.gz && sudo tar -xzvf latest.tar.gz && 
sudo chown -R www-data:www-data /var/www/html/wordpress
```

## Step 5 - Creating Database in mySQL>>>

5.1 Copy & paste the code below to enter into mySQL:
```
sudo mysql -u root -p 
```

5.2 Enter database password from step 2.2b

5.3 Copy & paste the code below, but replace the bold text: **wordpress_db**(with something like: **myfirstwordpress_db**). This is done twice, but use the same name for both. Also, create your own username '**wordpress_user**' and your own **PASSWORD**. The new bold text is needed for the next step, so make sure you have it recorded somewhere.

```
CREATE DATABASE wordpress_db; GRANT ALL PRIVILEGES ON wordpress_db.* TO 'wordpress_user'@'localhost' IDENTIFIED BY 'PASSWORD'; FLUSH PRIVILEGES; exit;
```

**wordpress_db, 'wordpress_user', 'PASSWORD', should be changed to something of your choice. Do not add or remove any of the quotations marks**

```
cd /var/www/html/wordpress && sudo mv wp-config-sample.php wp-config.php && sudo nano wp-config.php
```

5.4 Refer to the items you changed above and change the appropriate text(in **bold**) as shown below
in the GNU nano 5.2.3 file editor window:

________________________________________________________________________

// ** MySQL settings - You can get this info from your web host ** //

/** The name of the database for WordPress */

define('DB_NAME', '**wordpress_db**');                

/** MySQL database username */

define('DB_USER', '**wordpress_user**');             

/** MySQL database password */

define('DB_PASSWORD', '**PASSWORD**');        

________________________________________________________________________

5.5 Press "CTRL + O" to write file, press enter, then "CTRL + X" to exit.

5.6 We're almost done, just copy and paste the code from below:
```
systemctl restart apache2 && systemctl restart mysql
```
5.7 Enter the root user password, you'll be asked twice.

_______________________________________________________________________________________________

We are done working in the command line. We will finish the WordPress install in the browser.

________________________________________________________________________________________________

## Step 6 - WordPress Completion

6.1 Now go to: http://your.ip.address.here/wordpress to finish wordpress install. You should see the WordPress installation page where you select your language and continue.

6.2 Create a 'Site Title', 'Username' and 'Password' & enter a valid email address. Check the "Discourage search engines from indexing this site" and click 'Install Wordpress'.

6.3 Now login with the credentials you just created and start customizing your new WordPress website!

______________________________________________________________________________________________________

Thanks for checking out my WordPress runbook!!
