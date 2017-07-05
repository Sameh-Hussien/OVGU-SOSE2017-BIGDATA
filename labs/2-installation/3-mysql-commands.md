### MySQL installation

The steps below are MySQL-specific. If you are using RHEL/CentOS 7.x, use MariaDB.

* Download and implement the `official MariaDB repo`
    * Enable the repo to install MariaDB 5.5
	```
	$ curl -sS https://downloads.mariadb.com/MariaDB/mariadb_repo_setup |
	>     sudo bash -s -- --mariadb-server-version=mariadb-5.5.55
	[sudo] password for manaa: 
	[INFO] Repository file successfully written to /etc/yum.repos.d/mariadb.repo.
	[INFO] Adding trusted package signing keys...
	[INFO] Succeessfully added trusted package signing keys.
	```
	
    * Install `mariadb-server` on the server
	```
	$ yum install MariaDB-server
	Loaded plugins: fastestmirror, langpacks
	You need to be root to perform this command.
	[manaa@localhost1 ~]$ sudo yum install MariaDB-server
	Loaded plugins: fastestmirror, langpacks
	base                                                     | 3.6 kB     00:00     
	extras                                                   | 3.4 kB     00:00     
	mariadb-main                                             | 2.9 kB     00:00     
	mariadb-maxscale                                         | 2.4 kB     00:00     
	mariadb-tools                                            | 2.9 kB     00:00     
	updates                                                  | 3.4 kB     00:00     
	(1/5): extras/7/x86_64/primary_db                          | 167 kB   00:00     
	(2/5): updates/7/x86_64/primary_db                         | 5.6 MB   00:00     
	(3/5): mariadb-main/7/x86_64/primary_db                    |  19 kB   00:02     
	(4/5): mariadb-maxscale/7/x86_64/primary_db                | 4.5 kB   00:02     
	(5/5): mariadb-tools/7/x86_64/primary_db                   | 5.6 kB   00:02     
	Loading mirror speeds from cached hostfile
	* base: centos.mirrors.as250.net
	* extras: centos.mirrors.as250.net
	* updates: ftp.rrzn.uni-hannover.de
	Resolving Dependencies
	--> Running transaction check
	---> Package MariaDB-server.x86_64 0:5.5.55-1.el7.centos will be installed
	--> Processing Dependency: MariaDB-client for package: MariaDB-server-5.5.55-1.el7.centos.x86_64
	--> Processing Dependency: perl(DBI) for package: MariaDB-server-5.5.55-1.el7.centos.x86_64
	--> Processing Dependency: MariaDB-common for package: MariaDB-server-5.5.55-1.el7.centos.x86_64
	--> Running transaction check
	---> Package MariaDB-client.x86_64 0:5.5.55-1.el7.centos will be installed
	---> Package MariaDB-common.x86_64 0:5.5.55-1.el7.centos will be installed
	---> Package perl-DBI.x86_64 0:1.627-4.el7 will be installed
	--> Processing Dependency: perl(RPC::PlServer) >= 0.2001 for package: perl-DBI-1.627-4.el7.x86_64
	--> Processing Dependency: perl(RPC::PlClient) >= 0.2000 for package: perl-DBI-1.627-4.el7.x86_64
	--> Running transaction check
	---> Package perl-PlRPC.noarch 0:0.2020-14.el7 will be installed
	--> Processing Dependency: perl(Net::Daemon) >= 0.13 for package: perl-PlRPC-0.2020-14.el7.noarch
	--> Processing Dependency: perl(Net::Daemon::Test) for package: perl-PlRPC-0.2020-14.el7.noarch
	--> Processing Dependency: perl(Net::Daemon::Log) for package: perl-PlRPC-0.2020-14.el7.noarch
	--> Processing Dependency: perl(Compress::Zlib) for package: perl-PlRPC-0.2020-14.el7.noarch
	--> Running transaction check
	---> Package perl-IO-Compress.noarch 0:2.061-2.el7 will be installed
	--> Processing Dependency: perl(Compress::Raw::Zlib) >= 2.061 for package: perl-IO-Compress-2.061-2.el7.noarch
	--> Processing Dependency: perl(Compress::Raw::Bzip2) >= 2.061 for package: perl-IO-Compress-2.061-2.el7.noarch
	---> Package perl-Net-Daemon.noarch 0:0.48-5.el7 will be installed
	--> Running transaction check
	---> Package perl-Compress-Raw-Bzip2.x86_64 0:2.061-3.el7 will be installed
	---> Package perl-Compress-Raw-Zlib.x86_64 1:2.061-4.el7 will be installed
	--> Processing Conflict: MariaDB-common-5.5.55-1.el7.centos.x86_64 conflicts mariadb-libs < 1:5.5.55-1.el7.centos
	--> Restarting Dependency Resolution with new changes.
	--> Running transaction check
	---> Package MariaDB-shared.x86_64 0:5.5.55-1.el7.centos will be obsoleting
	---> Package mariadb-libs.x86_64 1:5.5.52-1.el7 will be obsoleted
	--> Finished Dependency Resolution
	
	Dependencies Resolved
	
	================================================================================
	Package                   Arch     Version                Repository      Size
	================================================================================
	Installing:
	MariaDB-server            x86_64   5.5.55-1.el7.centos    mariadb-main    40 M
	MariaDB-shared            x86_64   5.5.55-1.el7.centos    mariadb-main   1.0 M
		replacing  mariadb-libs.x86_64 1:5.5.52-1.el7
	Installing for dependencies:
	MariaDB-client            x86_64   5.5.55-1.el7.centos    mariadb-main   8.6 M
	MariaDB-common            x86_64   5.5.55-1.el7.centos    mariadb-main    23 k
	perl-Compress-Raw-Bzip2   x86_64   2.061-3.el7            base            32 k
	perl-Compress-Raw-Zlib    x86_64   1:2.061-4.el7          base            57 k
	perl-DBI                  x86_64   1.627-4.el7            base           802 k
	perl-IO-Compress          noarch   2.061-2.el7            base           260 k
	perl-Net-Daemon           noarch   0.48-5.el7             base            51 k
	perl-PlRPC                noarch   0.2020-14.el7          base            36 k
	
	Transaction Summary
	================================================================================
	Install  2 Packages (+8 Dependent packages)
	
	Total download size: 51 M
	Is this ok [y/d/N]: y
	Downloading packages:
	(1/10): MariaDB-5.5.55-centos7-x86_64-common.rpm           |  23 kB   00:02     
	(2/10): MariaDB-5.5.55-centos7-x86_64-client.rpm           | 8.6 MB   00:05     
	(3/10): perl-Compress-Raw-Bzip2-2.061-3.el7.x86_64.rpm     |  32 kB   00:00     
	(4/10): perl-Compress-Raw-Zlib-2.061-4.el7.x86_64.rpm      |  57 kB   00:00     
	(5/10): perl-IO-Compress-2.061-2.el7.noarch.rpm            | 260 kB   00:00     
	(6/10): perl-Net-Daemon-0.48-5.el7.noarch.rpm              |  51 kB   00:00     
	(7/10): perl-PlRPC-0.2020-14.el7.noarch.rpm                |  36 kB   00:00     
	(8/10): perl-DBI-1.627-4.el7.x86_64.rpm                    | 802 kB   00:00     
	(9/10): MariaDB-5.5.55-centos7-x86_64-shared.rpm           | 1.0 MB   00:02     
	(10/10): MariaDB-5.5.55-centos7-x86_64-server.rpm          |  40 MB   00:17     
	--------------------------------------------------------------------------------
	Total                                              2.6 MB/s |  51 MB  00:19     
	Running transaction check
	Running transaction test
	Transaction test succeeded
	Running transaction
	Installing : MariaDB-common-5.5.55-1.el7.centos.x86_64                   1/11 
	Installing : MariaDB-client-5.5.55-1.el7.centos.x86_64                   2/11 
	Installing : 1:perl-Compress-Raw-Zlib-2.061-4.el7.x86_64                 3/11 
	Installing : perl-Net-Daemon-0.48-5.el7.noarch                           4/11 
	Installing : perl-Compress-Raw-Bzip2-2.061-3.el7.x86_64                  5/11 
	Installing : perl-IO-Compress-2.061-2.el7.noarch                         6/11 
	Installing : perl-PlRPC-0.2020-14.el7.noarch                             7/11 
	Installing : perl-DBI-1.627-4.el7.x86_64                                 8/11 
	Installing : MariaDB-server-5.5.55-1.el7.centos.x86_64                   9/11 
	chown: cannot access ‘/var/lib/mysql’: No such file or directory
	170527 17:45:33 [Note] /usr/sbin/mysqld (mysqld 5.5.55-MariaDB) starting as process 2999 ...
	170527 17:45:33 [Note] /usr/sbin/mysqld (mysqld 5.5.55-MariaDB) starting as process 3007 ...
	
	PLEASE REMEMBER TO SET A PASSWORD FOR THE MariaDB root USER !
	To do so, start the server, then issue the following commands:
	
	'/usr/bin/mysqladmin' -u root password 'new-password'
	'/usr/bin/mysqladmin' -u root -h localhost1.localdomain password 'new-password'
	
	Alternatively you can run:
	'/usr/bin/mysql_secure_installation'
	
	which will also give you the option of removing the test
	databases and anonymous user created by default.  This is
	strongly recommended for production servers.
	
	See the MariaDB Knowledgebase at http://mariadb.com/kb or the
	MySQL manual for more instructions.
	
	Please report any problems at http://mariadb.org/jira
	
	The latest information about MariaDB is available at http://mariadb.org/.
	You can find additional information about the MySQL part at:
	http://dev.mysql.com
	Consider joining MariaDB's strong and vibrant community:
	https://mariadb.org/get-involved/
	
	Installing : MariaDB-shared-5.5.55-1.el7.centos.x86_64                  10/11 
	Erasing    : 1:mariadb-libs-5.5.52-1.el7.x86_64                         11/11 
	Verifying  : perl-Compress-Raw-Bzip2-2.061-3.el7.x86_64                  1/11 
	Verifying  : perl-Net-Daemon-0.48-5.el7.noarch                           2/11 
	Verifying  : MariaDB-server-5.5.55-1.el7.centos.x86_64                   3/11 
	Verifying  : MariaDB-shared-5.5.55-1.el7.centos.x86_64                   4/11 
	Verifying  : perl-PlRPC-0.2020-14.el7.noarch                             5/11 
	Verifying  : 1:perl-Compress-Raw-Zlib-2.061-4.el7.x86_64                 6/11 
	Verifying  : MariaDB-common-5.5.55-1.el7.centos.x86_64                   7/11 
	Verifying  : MariaDB-client-5.5.55-1.el7.centos.x86_64                   8/11 
	Verifying  : perl-IO-Compress-2.061-2.el7.noarch                         9/11 
	Verifying  : perl-DBI-1.627-4.el7.x86_64                                10/11 
	Verifying  : 1:mariadb-libs-5.5.52-1.el7.x86_64                         11/11 
	
	Installed:
	MariaDB-server.x86_64 0:5.5.55-1.el7.centos                                   
	MariaDB-shared.x86_64 0:5.5.55-1.el7.centos                                   
	
	Dependency Installed:
	MariaDB-client.x86_64 0:5.5.55-1.el7.centos                                   
	MariaDB-common.x86_64 0:5.5.55-1.el7.centos                                   
	perl-Compress-Raw-Bzip2.x86_64 0:2.061-3.el7                                  
	perl-Compress-Raw-Zlib.x86_64 1:2.061-4.el7                                   
	perl-DBI.x86_64 0:1.627-4.el7                                                 
	perl-IO-Compress.noarch 0:2.061-2.el7                                         
	perl-Net-Daemon.noarch 0:0.48-5.el7                                           
	perl-PlRPC.noarch 0:0.2020-14.el7                                             
	
	Replaced:
	mariadb-libs.x86_64 1:5.5.52-1.el7                                            
	
	Complete!
	```
	
    * Download and copy `the JDBC connector`
	```
	$ export CLASSPATH=/lib/mariadb/mariadb-java-client-2.0.1.jar:$CLASSPATH
	```
	
* Start the `mysql` service.
```
$ sudo systemctl start mysql
```
* Use `/usr/bin/mysql_secure_installation` to:
    * Set password protection for the server
    * Revoke permissions for anonymous users
    * Permit remote privileged login
    * Remove test databases
    * Refresh privileges in memory
    * Refreshes the `mysqld` service
```
$ sudo mysql_secure_installation
/bin/mysql_secure_installation: line 393: find_mysql_client: command not found

NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
      SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!

In order to log into MariaDB to secure it, we'll need the current
password for the root user.  If you've just installed MariaDB, and
you haven't set the root password yet, the password will be blank,
so you should just press enter here.

Enter current password for root (enter for none): 
ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: YES)
Enter current password for root (enter for none): 
OK, successfully used password, moving on...

Setting the root password ensures that nobody can log into the MariaDB
root user without the proper authorisation.

Set root password? [Y/n] y
New password: 
Re-enter new password: 
Password updated successfully!
Reloading privilege tables..
 ... Success!


By default, a MariaDB installation has an anonymous user, allowing anyone
to log into MariaDB without having to have a user account created for
them.  This is intended only for testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.

Remove anonymous users? [Y/n] y
 ... Success!

Normally, root should only be allowed to connect from 'localhost'.  This
ensures that someone cannot guess at the root password from the network.

Disallow root login remotely? [Y/n] n
 ... skipping.

By default, MariaDB comes with a database named 'test' that anyone can
access.  This is also intended only for testing, and should be removed
before moving into a production environment.

Remove test database and access to it? [Y/n] y
 - Dropping test database...
 ... Success!
 - Removing privileges on test database...
 ... Success!

Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.

Reload privilege tables now? [Y/n] y
 ... Success!

Cleaning up...

All done!  If you've completed all of the above steps, your MariaDB
installation should now be secure.

Thanks for using MariaDB!




$ sudo service mysql restart
Shutting down MySQL. SUCCESS! 
Starting MySQL.. SUCCESS! 

```

* MySQL version and all databases

```
[manaa@localhost1 ~]$ mysql -u root -p
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 6
Server version: 5.5.55-MariaDB MariaDB Server

Copyright (c) 2000, 2017, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
+--------------------+
3 rows in set (0.00 sec)
```




