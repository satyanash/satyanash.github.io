---
layout: post
title: "5 Minute WordPress Migration"
date: 2012-03-30T19:30:00+05:30
tags: software
---

I wanted to migrate this very blog to my other server.
A 15 Minute job that I had been delaying for the past 3 Months.
I finally decided to do it today.
The migration is as quick and simple as WordPress’s popular 5 minute installation.

These are the steps to do a quick and dirty WordPress blog migration from one server to other.
With no changes to the directory structure or anything else (except passwords).
The servers both run Ubuntu 10.04 LTS and the steps should be similar if not same for any other Debian based distribution.

Take a dump of the WordPress database using the mysqldump tool:

```
mysqldump -uwordpress_user -p wordpress_db > wordpress_backup.sql
```

Create a new database on the new server.
And also create a new user that WordPress will be using to carry out it’s activities in the database.

```
mysql> CREATE DATABASE wordpress_db;
mysql> GRANT ALL ON wordpress_db.* TO wordpress_user IDENTIFIED BY 'pass';
```

Now load the .sql file created earlier into this new database:

```
$ mysql -uwordpress_user -p -D wordpress_db < wordpress_backup.sql
```

```
## Change the old domain to the new one
$ mysql -uwordpress_user -p -D wordpress_db
mysql> USE wordpress_db;
mysql> UPDATE wp_options SET option_value = '<newdomain>' WHERE option_value = '<olddomain>';
```

Next copy all of the WordPress Website files off the default location in /var/www/ on the old server to the other server.
Also change the old values in wp-config.php to the new values for the new server.

Restarting the web-server is not required if the website is already configured in Apache2.
Apache will simply start serving the new website for any new requests from that point onwards.
MySQL hardly needs a restart.
But you may restart Apache2 and MySQL just to be sure.

```
/etc/init.d/mysql restart
/etc/init.d/apache2 restart
```

However do make sure MySQL is always running in the background.
If it is not running you may get an error saying something like:

```
    Database connection could not be established.
```

Once this is done, your WordPress blog should start working on the new server without any problems.

This process can also be used to restore from backups taken earlier in the same manner.
Essentially, migration involves backing on one server and restoring it to another.
While restoring would involve restoring from the backup on the same server.
