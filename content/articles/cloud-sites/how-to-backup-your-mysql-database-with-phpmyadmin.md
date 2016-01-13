---
node_id: 661
title: How to backup your MySQL database with phpMyAdmin
permalink: article/how-to-backup-your-mysql-database-with-phpmyadmin
type: article
created_date: '2011-03-16 21:57:40'
created_by: RackKCAdmin
last_modified_date: '2015-12-29 20:3555'
last_modified_by: stephanie.fillmon
products: Cloud Sites
body_format: tinymce
---

Backing Up Your MySQL Database
------------------------------

1.  To manage your MySQL database, you'll first need to [login to the
    online manager
    (phpMyAdmin)](http://www.rackspace.com/knowledge_center/article/rackspace-cloud-sites-essentials-phpmyadmin-database-management-interface).
2.  After you are logged into the online manager, click on a database or
    table in the left frame as shown in this example:\
     \
     ![phpMyAdmin
    Databases](http://c5018549.r49.cf2.rackcdn.com/phpmyadmin-dbs.png)\
     \
     The properties for this database or table will be displayed.\
      
3.  Then on the menu, click **Export**:\
     \
     ![phpMyAdmin Export
    tab](http://c5018549.r49.cf2.rackcdn.com/phpmyadmin-export.png)\
     \
     This interface will generate a backup file that can be used to
    recreate your database or table (it's actually just a file
    containing standard SQL statements).\
      
4.  To save the backup, you will need to check the box marked **Save as
    file**, so that phpMyAdmin will prompt you to download the resulting
    backup file. You can also change the name of the backup file and the
    compression--though the defaults are both fine if you would rather
    not change anything. If you do choose to use compression this will
    allow you to have a smaller backup file on your desktop if you are
    planning to keep it as a personal archive. The recommended setting
    is "**gzipped**":\
     \
     ![phpMyAdmin Save As
    File](http://c5018549.r49.cf2.rackcdn.com/phpmyadmin-saveasfile.png)\
      
5.  Finish by pressing the **Go** button; this may take a few moments to
    complete. You will then be prompted to save the file to your
    desktop.

Finish Line
-----------

Congratulations! You have just created a backup of your MySQL database!

If you experience a problem or you have further questions or concerns,
please do not hesitate to contact our technical support 24x7 via phone,
chat or by submitting a ticket through your control panel.
