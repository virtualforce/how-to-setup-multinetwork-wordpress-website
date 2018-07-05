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

```php
define('MULTISITE', true);
define('SUBDOMAIN_INSTALL', false);
define('DOMAIN_CURRENT_SITE', 'localhost.test.com');
define('PATH_CURRENT_SITE', '/cdpr/');
define('SITE_ID_CURRENT_SITE', 1);
define('BLOG_ID_CURRENT_SITE', 1);
define('COOKIE_DOMAIN', '');
define('ADMIN_COOKIE_PATH', '/');
define('COOKIEPATH', '/');
define('SITECOOKIEPATH', '/');
```

Add the following lines to your .htaccess and save.

```php
RewriteEngine On
RewriteBase /website-folder-name/
RewriteRule ^index\.php$ - [L]
# add a trailing slash to /wp-admin
RewriteRule ^([_0-9a-zA-Z-]+/)?wp-admin$ $1wp-admin/ [R=301,L]
RewriteCond %{REQUEST_FILENAME} -f [OR]
RewriteCond %{REQUEST_FILENAME} -d
RewriteRule ^ - [L]
RewriteRule ^([_0-9a-zA-Z-]+/)?(wp-(content|admin|includes).*) $2 [L]
RewriteRule ^([_0-9a-zA-Z-]+/)?(.*\.php)$ $2 [L]
RewriteRule . index.php [L]
```

![alt text](https://github.com/virtualforce/how-to-setup-multinetwork-wordpress-website/blob/master/images/step2.png ".htaccess and wp-config extra lines.")

#### 3. Login to your wordpress admin panel:
Once you complete these steps, your network is enabled and configured. You will have to Log In again.After login,You need to go to Plugins and activate the plugins that you require as Network Activate.You can activate/de-activate plugins later too if you want.


#### 4. Enabling Sub-Domains/Domains in Multisite Network:
You’ll need to create a subdomain with `*` as the subdomain name. For example, if your WordPress is installed at www.test.com then you need to create a subdomain ![example.test.com](example.test.com "example.test.com"). However, this subdomain should point to the same directory where your WordPress is installed. 

I suggest you to put anything(example.test.com) here so you can atleast go to next step and create a sub-website.

![alt text](https://github.com/virtualforce/how-to-setup-multinetwork-wordpress-website/blob/master/images/step3.png "Addin domain or subdomains")

Once you have setup the sub-site,You can change the base url of your sub-site like www.test.net You can make settings for this particular new sub-site.You can add users and themes.

![alt text](https://github.com/virtualforce/how-to-setup-multinetwork-wordpress-website/blob/master/images/step4.png "settings of new sub-site")

#### 5. You are done.
That's all.

#### Virtuals hosts and other basic configurations.
You have to point your secondary domain(www.test.net) to the same IP addresss to which your main domain(www.test.com) is pointed.

Your virtual hosts file should look like:
```php
##virtual host for your test.com
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html/test.com
    ServerName www.test.com
	<Directory "/var/www/html/test.com">
        Options Indexes FollowSymLinks Includes ExecCGI
        AllowOverride All
        Order allow,deny
        Allow from all
    </Directory>
</VirtualHost>
##virtual host for your test.net 
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html/test.com
    ServerName www.test.net
	<Directory "/var/www/html/test.com">
        Options Indexes FollowSymLinks Includes ExecCGI
        AllowOverride All
        Order allow,deny
        Allow from all
    </Directory>
</VirtualHost>
```

There are some basic configurations for a Network website like maximum upload size to media,type of files allowed etc.Please see the below screenshot.

![alt text](https://github.com/virtualforce/how-to-setup-multinetwork-wordpress-website/blob/master/images/step4.png "settings of new sub-site")

Make sure `rewrite module` is enabled on your server.Run following command to enable it.

`sudo a2enmod rewrite`

Don't forget to restart your server after you have made changes to PHP.INI or virtual hosts file.

`sudo service apache2 restart`


### References:

 * [Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-set-up-multiple-wordpress-sites-using-multisite)
 * [WPBEGINNER](https://www.wpbeginner.com/glossary/multisite/)
