# How to setup multinetwork wordpress website with two different domains?
I will explain how you can use same based code of WordPress website with 2 different domains.This is something called Multi-Networking in wordpress.

#### 1. Backup your files and database:
First of all, you need to take a backup of your website files and database. Although There is only one change in file that is wp-config.But still you have to be very careful.

#### 2. Open wp-config.php from root directory of your wordpress:
Edit the file wp-config.php, and add the following line just before That’s all, stop editing! Happy blogging.
```php
/* Multisite */
define('WP_ALLOW_MULTISITE', true);
```
Save your wp-config.php file and log in to your WordPress website. Go to Tools » Network Setup. This is the place where you will configure and set up your WordPress Multi-site Network.

`You will be asked to de-activate all of your plugins before enabling multi-networking.Do de-activate all activated plugins.`

![alt text](https://github.com/virtualforce/how-to-setup-multinetwork-wordpress-website/blob/master/images/step1.png "Enabling Multi-Networking")

After "Clicking" install button, You will see second screen as below to add below extra lines to your wp-config.php file and save.

`define('MULTISITE', true);
define('SUBDOMAIN_INSTALL', false);
define('DOMAIN_CURRENT_SITE', 'localhost');
define('PATH_CURRENT_SITE', '/cdpr/');
define('SITE_ID_CURRENT_SITE', 1);
define('BLOG_ID_CURRENT_SITE', 1);`

Add the following lines to your .htaccess and save.

`RewriteEngine On
RewriteBase /website-folder-name/
RewriteRule ^index\.php$ - [L]
# add a trailing slash to /wp-admin
RewriteRule ^([_0-9a-zA-Z-]+/)?wp-admin$ $1wp-admin/ [R=301,L]
RewriteCond %{REQUEST_FILENAME} -f [OR]
RewriteCond %{REQUEST_FILENAME} -d
RewriteRule ^ - [L]
RewriteRule ^([_0-9a-zA-Z-]+/)?(wp-(content|admin|includes).*) $2 [L]
RewriteRule ^([_0-9a-zA-Z-]+/)?(.*\.php)$ $2 [L]
RewriteRule . index.php [L]`


![alt text](https://github.com/virtualforce/how-to-setup-multinetwork-wordpress-website/blob/master/images/step2.png ".htaccess and wp-config extra lines.")

#### 3. Login to your wordpress admin panel:
Once you complete these steps, your network is enabled and configured. You will have to log in again. Log In.After login,you will be able to see screen like below.


#### 4. Enabling Sub-Domains/Domains in Multisite Network:
You’ll need to create a subdomain with `*` as the subdomain name. For example, if your WordPress is installed at www.example.com then you need to create a subdomain subdomain.example.com. However, this subdomain should point to the same directory where your WordPress is installed. We will show you how to create a wildcard subdomain in cPanel.

![alt text](https://github.com/virtualforce/how-to-setup-multinetwork-wordpress-website/blob/master/images/step3.png "Addin domain or subdomains")

Log in to your cPanel dashboard and then under the Domains section click on Subdomains. On the next screen simply enter * in the subdomain field. Make sure that the document root field is pointing to the directory where you have WordPress installed. This is the directory where wp-config.php file resides. Hit the create button to add the subdomain.




media upload limit
Server Side:
sudo a2enmod rewrite
<Directory /var/www/>
                Options Indexes FollowSymLinks MultiViews
                AllowOverride All
                Order allow,deny
                allow from all
</Directory>

sudo service apache2 restart

