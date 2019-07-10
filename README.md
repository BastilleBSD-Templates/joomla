# joomla
Bastille Template for a Joomla Content Management Jail

APACHE INSTALL

As instructed by the post-install message, add the following lines to 
/usr/local/etc/apache24/httpd.conf:

	<FilesMatch "\.php$">
	    SetHandler application/x-httpd-php
	</FilesMatch>
	<FilesMatch "\.phps$">
	    SetHandler application/x-httpd-php-source
	</FilesMatch>
	
Also modify the line:

	DirectoryIndex index.html

changing it to:

	DirectoryIndex index.php index.html


PHP INSTALL

Create a new php.ini file by copying one of the sample files.

	cd /usr/local/etc/
	cp php.ini-production php.ini

Open and edit /usr/local/etc/php.ini and adjust the following values:

	memory_limit:  Minimum: 64M   Recommended: 128M or more
	upload_max_filesize:  Minimum: 20M
	post_max_size:  Minimum: 20M
	max_execution_time:  At Least 120   Recommended: 300 or higher

After installing and configuring PHP restart the Apache service.

	service apache24 restart


MYSQL SERVER INSTALL

Edit /usr/local/etc/mysql/my.cnf and add the following line to the [mysqld] section:

	default_authentication_plugin   = mysql_native_password

Start the MySQL server.

	service mysql-server start

Upon initial installation, the MySQL 8.0 server's root user has no password.

Login to the mysql server on the command line as root and set your desired password.

	mysql -u root
	root@localhost [(none)]>ALTER USER 'root'@'localhost' IDENTIFIED BY 'password';

Create a database for the Joomla web site with your preferred database name.

	root@localhost [(none)]>create database joomladb;

Create a dedicated MySQL user with your preferred username and password.

	root@localhost [(none)]>create user 'joomlauser'@'localhost' identified by 'password';

Grant the user all privileges to the Joomla database.

	root@localhost [(none)]>grant all privileges on joomladb.* to 'joomlauser'@'localhost';

exit to close the connection to MySQL server.


JOOMLA SERVER INSTALL

Open and direct your web browser to one of the following...

If browsing directly on the server: 
	http://localhost

If browsing from a remote system: 
	http://<ip_address> or http://<fully.qualified.domain.name> (if configured)

You will see the Joomla Web Installer page.


In step 1 Configuration:
	fill in the fields as required.

In step 2 Database:
	Username: <joomlauser>
	Password: <joomlauser password>
	Database name: <joomladb>


Leave the other settings unchanged:
	Database Type: MySQLi
	Hostname: localhost
	Table Prefix: unchanged


The final step of the web installer will be to delete the installation folder.
Once that is done you can browse to your newly installed Joomla! web site!


