# Owncloud Quick Start Guide
## Installing Owncloud server
You can install the Owncloud server to share your files and data and control access. You should install the Owncloud server by using the ownCloud tarball, which is the most suitable and customizable installation option for production environments. 
### Before you begin
You must have the following PHP versions and extensions available: 
* PHP versions 5.6 and later, 7.0, 7.1, and 7.2
* PHP extensions: See the list of PHP extensions and their functions at: https://doc.owncloud.org/server/latest/admin_manual/installation/source_installation.html#prerequisites
**Steps**
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
