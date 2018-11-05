# Owncloud Quick Start Guide

## Installing the Oncloud server
You can install the Owncloud server to share your files and data and control access. You should install the Owncloud server by using the ownCloud tarball, which is the most suitable and customizable installation option for production environments. 
### Before you begin
You must have the following PHP versions and extensions available: 
* PHP versions 5.6 and later, 7.0, 7.1, and 7.2
* PHP extensions: See the list of PHP extensions and their functions at: 
https://doc.owncloud.org/server/latest/admin_manual/installation/source_installation.html#prerequisites
### Steps
1.	Download the Owncloud tarball from the Owncloud website:
https://owncloud.org/download/
You can download either the tar.bz2 or .zip archive. 
The name of the downloaded file is owncloud-x.y.z.tar.bz2 or owncloud-x.y.z.zip (where x.y.z is the version number).
2.	Download the corresponding checksum file.
For example, owncloud-x.y.z.tar.bz2.md5, or owncloud-x.y.z.tar.bz2.sha256.
3.	Verify the MD5 or SHA256 sum:
```
md5sum -c owncloud-x.y.z.tar.bz2.md5 < owncloud-x.y.z.tar.bz2
sha256sum -c owncloud-x.y.z.tar.bz2.sha256 < owncloud-x.y.z.tar.bz2
md5sum -c owncloud-x.y.z.zip.md5 < owncloud-x.y.z.zip
sha256sum -c owncloud-x.y.z.zip.sha256 < owncloud-x.y.z.zip
```
4.	Verify the PGP signature:
```
wget https://download.owncloud.org/community/owncloud-x.y.z.tar.bz2.asc
wget https://owncloud.org/owncloud.asc
gpg --import owncloud.asc
gpg --verify owncloud-x.y.z.tar.bz2.asc owncloud-x.y.z.tar.bz2
```
5.	Extract the archive contents by using the unpacking command for your archive type:
```
tar -xjf owncloud-x.y.z.tar.bz2
unzip owncloud-x.y.z.zip
```
6.	Copy the ownCloud directory to a destination folder. 
When you are running the Apache HTTP server, you can install ownCloud in your Apache document root:
```
cp -r owncloud /path/to/webserver/document-root
```
where /path/to/webserver/document-root is replaced by the document root of your Web server.

## Configuring the Apache Web Server
To configure the Apache web server, you need to create a configuration file and create a symlink to it.

### Steps
1. Create a `/etc/apache2/sites-available/owncloud.conf` file with the following content:
```
Alias /owncloud "/var/www/owncloud/"
Directory /var/www/owncloud/
  Options +FollowSymlinks
  AllowOverride All
 <IfModule mod_dav.c>
  Dav off
 </IfModule>
 SetEnv HOME /var/www/owncloud
 SetEnv HTTP_HOME /var/www/owncloud
Directory
```
Replace the Directory and file paths with your file paths.
2. Create a symlink to the configuration file:
```
ln -s /etc/apache2/sites-available/owncloud.conf /etc/apache2/sites-enabled/owncloud.conf
```
3. Enable the required Apache module by running the following commands:
```
a2enmod rewrite
a2enmod headers
a2enmod env
a2enmod dir
a2enmod mime
```
4. Restart the Apache web server.
```
service apache2 restart
```

## Enabling SSL
You should use SSL/TLS to encrypt all of your server traffic, and to protect user’s logins and data in transit.
### Steps
1. Enable the `ssl` module and the default site:
```
a2enmod ssl
a2ensite default-ssl
service apache2 reload
```

## Completing the installation of the Owncloud server
You must complete the installation of the Owncloud server by running the Graphical Installation Wizard.
### About this task
You can also use the command line with the occ command to complete this task.
For more details, see https://doc.owncloud.org/server/latest/admin_manual/installation/command_line_installation.html
### Steps
1. Temporarily change the ownership on your ownCloud directories to your HTTP user:
```
chown -R www-data:www-data /var/www/owncloud/
```
2. Point your web browser to http://localhost/owncloud
3. Enter your desired administrator’s username and password and click **Finish Setup**.
### After your finish
Set up your ownCloud server for best performance and security. 
https://doc.owncloud.org/server/latest/admin_manual/installation/installation_wizard.html


## Adding a user account to OwnCloud server
As an Owncloud administrator, you can create user accounts and add them to the Owncloud server.
### Steps
1. Under **Administration**, click **System and domain settings**.  
2. Login with your administrator user name and password. 
3. Click **User: Add**  to create the users who have access to your OwnCloud server. 
You can set the checkbox next to **Change Password for next login** to **true** for enabling users to create their own password. 
### Result
By default, users can access the Owncloud server by using HTTP on a web browser. 

## Connecting to the Owncloud server using a desktop client
You can use the OwnCloud Desktop Synchronization client to automatically synchronize your files between the ownCloud server and your local system. The ownCloud Desktop Synchronization client enables you to do the following: 
- Specify one or more directories on your computer that you want to synchronize to the ownCloud server.
- Always have the latest files synchronized, wherever they are located.
### Steps
1. Download the Owncloud Desktop Synchronization client for your operating system from the following location: 
https://owncloud.com/download/#desktop-clients
2. Follow the step-by-step instructions in the installation wizard. 
3. For connecting to the Owncloud server from the client, perform the following steps:
   - Enter the URL of your ownCloud server in the **Server Address** field. 
   - Click **Next** and enter your ownCloud login.
   - Click **Next**. 
   - On the “Local Folder Option” screen, select to sync all of your files on the ownCloud server or select individual folders. 
   - Click **Connect**.
   
When the client successfully connects to your ownCloud server, the file synchronization begins and you can see the following two options:
- one to connect to your ownCloud Web GUI
- one to open your local folder

## Connecting to the Owncloud server using a mobile client
You can use the OwnCloud mobile app (iOS or Android) to automatically synchronize your files between the ownCloud server and your mobile phone. 
### Steps
1. Download the OwnCloud mobile application from the AppStore on your iOS device or from the Google PlayStore on your Android device. 
2. Open the application and enter the following details:
- Server URL
- Login name
- Password
3. Click **Connect**. 
