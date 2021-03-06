---
node_id: 390
title: Migrating your Drupal database to Cloud Servers
type: article
created_date: '2011-04-04'
created_by: Rackspace Support
last_modified_date: '2016-01-13'
last_modified_by: Stephanie Fillmon
product: Cloud Servers
product_url: cloud-servers
---

This article will walk you through migrating your Drupal database from
Cloud Sites to Cloud Servers.

-   [<span class="toctext">Creating Your Cloud
    Server</span>](#Creating_Your_Cloud_Server)
-   [<span class="toctext">Connecting to the
    server</span>](#Connecting_to_the_server)
-   [<span class="toctext">Change Root
    Password</span>](#Change_Root_Password)
-   [<span class="toctext">Performing System
    Updates</span>](#Performing_System_Updates)
-   [<span class="toctext">Configure Time
    Zone</span>](#Configure_Time_Zone)
-   [<span class="toctext">Configure
    Firewall (iptables)</span>](#Configure_Firewall_.28iptables.29)
-   [<span class="toctext">Installing Apache</span>](#Installing_Apache)
-   [<span class="toctext">Install MySQL</span>](#Install_MySQL)
-   [<span class="toctext">Install
    phpMyAdmin</span>](#Install_phpMyAdmin)
-   [<span class="toctext">Download Your Drupal
    Database</span>](#Download_Your_Drupal_Database)
-   [<span class="toctext">Import Your Drupal
    Database</span>](#Import_Your_Drupal_Database)
-   [<span class="toctext">Setup Drupal User</span>](#Setup_Drupal_User)
-   [<span class="toctext">Modifying
    settings.php</span>](#Modifying_settings.php)
-   [<span class="toctext">Modify MySQL
    Configuration</span>](#Modify_MySQL_Configuration)
-   [<span class="toctext">Test Your
    Installation</span>](#Test_Your_Installation)

A few pieces of advice that should be noted before beginning:

-   Cloud Servers does not have a direct way to talk to Cloud Sites.
    Because of this you may incur expensive bandwidth charges while
    running over the public interface (eth0).
-   This tutorial assumes you have a basic understanding of how to
    operate in the Linux environment. If you do not, please research
    this first and then return to this tutorial. Failure to properly
    understand the Linux environment may lead to data loss or your
    server and/or data becoming compromised.
-   This tutorial was built on a Cloud Server running Ubuntu
    9.10 (Karmic) with 512MB RAM. While this will work as a minimal
    setup it is recommended that you run a larger server (1GB
    or higher).



<span class="mw-headline">Creating Your Cloud Server</span>
-----------------------------------------------------------

To begin we will need to create your Cloud Server via the control panel
(<https://mycloud.rackspace.com>).  For more information, refer to [this
article on creating a new Cloud
Server](/how-to/cloud-servers).



<span class="mw-headline">Connecting to the server</span>
---------------------------------------------------------

Once the server has finished building you will be presented with an
overview screen. You have two different ways of connecting to the
server: SSH or Console. SSH is by far the superior way to connect
because it gives you a better, more reliable connection. The Console
uses your web browser and may not always be compatible with your current
environment -- it is considered a last resort method of connecting.


For our tutorial we will assume that you are using SSH to connect to
your server. Each operating system has it's own way to connecting either
native or with a helper application. If you are using Windows you can
use an application called *PuTTY* which can be freely downloaded on the
Internet. If you are on a Macintosh or Linux-based computer you can use
the *ssh* application that comes pre-installed with the computer.


(You can access the *ssh* application on your Macintosh through Terminal
(Macintosh HD -&gt; Utilities -&gt; Terminal)


To connect from your Windows computer with PuTTY please use the
following article to help you: [Connecting with
PuTTY](/how-to/connecting-to-linux-from-windows-by-using-putty "Logging in via Putty")

To connect with your Macintosh or Linux computer simply type the
following:

    $ ssh root@12.34.56.78

Be sure to replace *12.34.56.78* with the IP address of your Cloud
Server. You can see this on the overview screen of your server or in the
e-mail that you'll receive after it is setup. You may be prompted to
accept the RSA key, simply type **yes**.

Your screen should look similar to this once connected:

![sites\_mysql\_ssh\_login.png](http://c0042672.cdn.cloudfiles.rackspacecloud.com/sites_mysql_ssh_login.png)



<span class="mw-headline">Change Root Password</span>
-----------------------------------------------------

The first thing we need to do is change our root password. To do this
type the following command:

    # passwd

You will be prompted for your new password twice, please enter it. *You
will not see the characters on the screen as you type!*



<span class="mw-headline">Performing System Updates</span>
----------------------------------------------------------

Next we need to do is make sure that our system is update to date. We
will use the *apt-get* program to do this. Type the following command to
make sure our update catalogs are up-to-date:

    # apt-get update

Once that finishes we need to tell our server to update it's software.
To do this type the following command:

    # apt-get upgrade



<span class="mw-headline">Configure Time Zone</span>
----------------------------------------------------

The next thing we need to do is configure our time zone data so our
server has the correct time for logs. To do this we'll type the
following:

    # dpkg-reconfigure tzdata

You'll be presented with a screen that looks like the image below.
Select your geographical location to select your time zone and then
select **&lt;Ok&gt;**.

![sites\_mysql\_tzdata\_reconfig.png](http://c0042672.cdn.cloudfiles.rackspacecloud.com/sites_mysql_tzdata_reconfig.png)

Once you have set your time zone you'll be sent back to the command
prompt and you'll see something similar to the following:

    Current default time zone: 'US/Central'
    Local time is now:      Thu Jan 14 09:47:05 CST 2010.
    Universal Time is now:  Thu Jan 14 15:47:05 UTC 2010.



<span class="mw-headline">Configure Firewall (iptables)</span>
--------------------------------------------------------------

Next we need to configure our firewall to keep our server protected on
the Internet. The firewall that is built into your server is called
*iptables* and works very well. By default Ubuntu does not have any
firewall rules configured so we will need to configure them.


We will configure our rules based on the following assumptions:

-   We will accept all traffic that is established
-   We will accept SSH traffic (port 22/tcp)
-   We will accept incoming MySQL requests (port 3306/tcp)
-   We will accept incoming HTTP traffic (port 80/tcp)
-   We will drop everything else sent to us


Let's begin adding rules to our firewall and get secured! Keep in mind
that when you enter these rules they are added real-time and **can lock
you out of your server!** If you do this you must use the console as the
*root* user and type **ipconfig -F** to flush your iptables rules.
Please note that these are basic rules and may not cover all situations
or server configurations.


For more information about iptables rules with Ubuntu, check out the
following link: <https://help.ubuntu.com/community/IptablesHowTo>


Let's start by adding a rule to allow established traffic to our server:

    # iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT


Next we need to add a line to allow incoming SSH traffic. Type the
following line to do this:

    # iptables -A INPUT -p tcp --dport ssh -j ACCEPT


Now we need to add a line to allow incoming MySQL traffic. Type the
following line to do this:

    # iptables -A INPUT -p tcp --dport mysql -j ACCEPT


Next we need to add a line to allow incoming HTTP traffic. Type the
following line to do this:

    # iptables -A INPUT -p tcp --dport www -j ACCEPT


Finally we need to set all other traffic to block. Type the following to
to do this:

    # iptables -A INPUT -j DROP


If you look at your resulting rule set (by typing **iptables -L**) it
should look like this:

    Chain INPUT (policy ACCEPT)
    target     prot opt source               destination
    ACCEPT     all  --  anywhere             anywhere            state RELATED,ESTABLISHED
    ACCEPT     tcp  --  anywhere             anywhere            tcp dpt:ssh
    ACCEPT     tcp  --  anywhere             anywhere            tcp dpt:mysql
    ACCEPT     tcp  --  anywhere             anywhere            tcp dpt:www
    DROP       all  --  anywhere             anywhere

    Chain FORWARD (policy ACCEPT)
    target     prot opt source               destination

    Chain OUTPUT (policy ACCEPT)
    target     prot opt source               destination


If all looks well we are ready to save our rules. To save our rules
simply type the following:

    # iptables-save > /etc/iptables.rules


The next step is making sure that our rules are loaded when the server
reboots. This involves creating a script that is executed when the
server boots up. Type the following to create the file:

    # nano /etc/network/if-pre-up.d/iptables-load

You will be presented with a text editor on the screen. Type or copy in
the following text:

    #!/bin/sh
    iptables-restore < /etc/iptables.rules
    exit 0

Save the file by pressing **CTRL-X** followed by **Y**. You will be
prompted for the filename, simply press **Enter**.

Finally we need to make sure the script is executable:

    # chmod +x /etc/network/if-pre-up.d/iptables-load

To test our rules, let's issue a reboot to our server and make sure they
are applying as we expect:

    # reboot

Once the server comes back up please connect again with SSH and login as
the *root* user. You can issue **iptables -L** on your server and you
should see your rules listed. If you do not see them, be sure that you
created the script above correctly.



<span class="mw-headline">Installing Apache</span>
--------------------------------------------------

Next we need to install Apache to handle phpMyAdmin, our web-based
management system for MySQL. To install Apache simply type the
following:

    # apt-get install apache2


Once you have the server installed you can go to your server's IP
address in a web-browser and you should see something like this:

![sites\_mysql\_apache\_test.png](http://c0042672.cdn.cloudfiles.rackspacecloud.com/sites_mysql_apache_test.png)



<span class="mw-headline">Install MySQL</span>
----------------------------------------------

Next we need to install our MySQL server. To do this simply type:

    # apt-get install mysql-server

You will be prompted to enter your MySQL root password. Please choose
this password carefully! *This user will have full control of your MySQL
server and have permissions to ALL data!* You will be asked for this
twice.

![sites\_mysql\_mysql\_root\_password.png](http://c0042672.cdn.cloudfiles.rackspacecloud.com/sites_mysql_mysql_root_password.png)



<span class="mw-headline">Install phpMyAdmin</span>
---------------------------------------------------

Next we need to install phpMyAdmin which will be used to manage your
MySQL server from a website. This is the same interface used with Cloud
Sites to interact with your MySQL databases. To install it on your Cloud
Server type the following:

    # apt-get install phpmyadmin

Once the installation finishes you should be presented with a prompt
asking you which web-server to auto configure. We will select
**apache2** by pressing the space bar and pressing **Enter**. A
screenshot is below:

![sites\_mysql\_phpmyadmin\_webserver\_config.png](http://c0042672.cdn.cloudfiles.rackspacecloud.com/sites_mysql_phpmyadmin_webserver_config.png)


You will be prompted to configure a database required for phpMyAdmin to
function. Select **Yes** and press **Enter**.

![sites\_mysql\_config\_phpmyadmin\_db.png](http://c0042672.cdn.cloudfiles.rackspacecloud.com/sites_mysql_config_phpmyadmin_db.png)


You will be asked for the *root* password for the database to create the
associated database and tables. Type this in and press **Enter**.

![sites\_mysql\_configure\_phpmyadmin\_root\_pw.png](http://c0042672.cdn.cloudfiles.rackspacecloud.com/sites_mysql_configure_phpmyadmin_root_pw.png)

You will be prompted for the password that you'd like to set for the
*phpmyadmin* user. Since we will never use this account to login we will
allow it to generate a random password. Press **Enter** to allow this.

![sites\_mysql\_phpmyadmin\_pw.png](http://c0042672.cdn.cloudfiles.rackspacecloud.com/sites_mysql_phpmyadmin_pw.png)


Once the install finishes we need to test our phpMyAdmin installation.
Point your web browser to **<http://12.34.56.78/phpmyadmin>** (change to
your Server's IP). You should see a screen like the one below:

![sites\_mysql\_phpmyadmin\_test.png](http://c0042672.cdn.cloudfiles.rackspacecloud.com/sites_mysql_phpmyadmin_test.png)

You may test your login by using the *root* user and entering your MySQL
root password.



<span class="mw-headline">Download Your Drupal Database</span>
--------------------------------------------------------------

We are ready to get a database dump from your Cloud Sites account. To do
this we will need to have you login to phpMyAdmin on the Cloud Sites
system. The location you need connect to depends on where your site is
located. Please refer to the Control Panel to determine what data center
your site is hosted in.

-   DFW: <https://mysql.dfw1-1.websitesettings.com/>
-   SAT: <https://mysql.websitesettings.com/>

For the sake of demonstration we will assume you are using the DFW data
center.


When you click on the link you will have a phpMyAdmin login screen
appear. You will need to type in your database user name and password
associated with your Drupal website. You will also need to select the
appropriate MySQL attached to your database. You can find all of this in
the Control Panel on your site's *Features* tab.

![sites\_mysql\_dfw\_pma\_login.png](http://c0042672.cdn.cloudfiles.rackspacecloud.com/sites_mysql_dfw_pma_login.png)


Once you are logged in we need to begin pulling a copy of the database.
To do this scroll down on the right window pane and find the **Export**
link; click this.

![sites\_mysql\_pma\_export.png](http://c0042672.cdn.cloudfiles.rackspacecloud.com/sites_mysql_pma_export.png)


You will be presented with an export screen. On the left side under
*Export* select your Drupal database (eg: 388488\_drupal). Scroll down
to the bottom and check the checkbox labeled **Save as file** -- this
will save your database output to a file. Finally click the **Go**
button on the bottom right. You may get prompted where to save your
file... save it somewhere on your computer.

![sites\_mysql\_pma\_dump\_choosedb.png](http://c0042672.cdn.cloudfiles.rackspacecloud.com/sites_mysql_pma_dump_choosedb.png)
![sites\_mysql\_pma\_dump\_savefile.png](http://c0042672.cdn.cloudfiles.rackspacecloud.com/sites_mysql_pma_dump_savefile.png)
![sites\_mysql\_pma\_dump\_gobutton.png](http://c0042672.cdn.cloudfiles.rackspacecloud.com/sites_mysql_pma_dump_gobutton.png)

Once you have your database file (it may take a while to download) you
can close phpMyAdmin.



<span class="mw-headline">Import Your Drupal Database</span>
------------------------------------------------------------

Now we are ready to import your database into your Cloud Server. Let's
pull up phpMyAdmin that is hosted on your Cloud Server. Point your
web-browser to <http://12.34.56.78/phpmyadmin/>. *Be sure to change
12.34.56.78 to your IP address!*

You should see the login screen. Type in **root** for the login and type
in your MySQL root password that we chose earlier. Click **Go** to
login.

![sites\_mysql\_cs\_pma\_login.png](http://c0042672.cdn.cloudfiles.rackspacecloud.com/sites_mysql_cs_pma_login.png)

Once you are logged in you will need to click on the **Import** tab at
the top.

![sites\_mysql\_cs\_pma\_importlink.png](http://c0042672.cdn.cloudfiles.rackspacecloud.com/sites_mysql_cs_pma_importlink.png)


You will be presented with an import screen asking for some variables.
Click on the **Choose File** button and choose your backup file that we
downloaded earlier. Scroll down and then click the **Go** button to
begin the import.

**NOTE:** phpMyAdmin will only allow database import less than 2MB in
size. If your database is larger than this it will have to be executed
from the command line or through the SQL window.

![sites\_mysql\_cs\_pma\_import1.png](http://c0042672.cdn.cloudfiles.rackspacecloud.com/sites_mysql_cs_pma_import1.png)
![sites\_mysql\_cs\_pma\_import2.png](http://c0042672.cdn.cloudfiles.rackspacecloud.com/sites_mysql_cs_pma_import2.png)


If your import worked successfully you will see something like the
picture below. You may close the window.

![sites\_mysql\_cs\_pma\_import3.png](http://c0042672.cdn.cloudfiles.rackspacecloud.com/sites_mysql_cs_pma_import3.png)


**Importing databases over 2MB:**

If your database is larger than 2MB in size you will have to copy your
file to your server and import it using an SSH command line. This is an
advanced task but we will give you a quick run-through. You can upload
your file using *WinSCP* or the *scp* command, if available. Simply
login with the *root* user if you'd like and copy your SQL file. Once
the file is copied you will need to connect to your server and login as
the *root* user (since you copied with it). You can import your file
with the mysql command-line tools. If your file is named
*database\_backup.sql*, the command you would type is as follows:

    # mysql -u root -p < database_backup.sql

Please note that you will be prompted for your MySQL root password.



<span class="mw-headline">Setup Drupal User</span>
--------------------------------------------------

At this point we simply have the database copied but have not created
the Drupal user yet. We can add these permissions easily with
phpMyAdmin. Return back to the phpMyAdmin window that we have open and
click on the **Privileges** tab.

![sites\_mysql\_cs\_pma\_priv\_tab.png](http://c0042672.cdn.cloudfiles.rackspacecloud.com/sites_mysql_cs_pma_priv_tab.png)

Once you click on the tab you will be presented with a list of users.
Click on the **Add a new user** link near the bottom.

![sites\_mysql\_cs\_pma\_priv\_addlink.png](http://c0042672.cdn.cloudfiles.rackspacecloud.com/sites_mysql_cs_pma_priv_addlink.png)

You will be presented with a form asking several pieces of information.
We are going to duplicate the user information that was used on your
Cloud Sites database. For **User Name:** type in your user name. Jump
down to the **Password:** line and type in the password for your Drupal
user in Cloud Sites. Type it again in the box that follows. Once you
have this filled in scroll down to the bottom and click **Go**. Refer to
the examples below:

![sites\_mysql\_cs\_pma\_adduser\_details.png](http://c0042672.cdn.cloudfiles.rackspacecloud.com/sites_mysql_cs_pma_adduser_details.png)
![sites\_mysql\_cs\_pma\_adduser\_gobutton.png](http://c0042672.cdn.cloudfiles.rackspacecloud.com/sites_mysql_cs_pma_adduser_gobutton.png)


Once the user is created you will be asked what permissions to grant
this user. Scroll down to **Database-specific Privileges' and type your
Drupal database name in the text box. Once you have done this click
the** Go **button.**
![sites\_mysql\_cs\_pma\_dbspec\_privs.png](http://c0042672.cdn.cloudfiles.rackspacecloud.com/sites_mysql_cs_pma_dbspec_privs.png)

Locate the box titled *Data* and check the following boxes:

-   SELECT
-   INSERT
-   UPDATE
-   DELETE

The image below shows the boxes that should be checked. Scroll down and
click the **Go** button.

![sites\_mysql\_cs\_pma\_dbspec\_privs\_add.png](http://c0042672.cdn.cloudfiles.rackspacecloud.com/sites_mysql_cs_pma_dbspec_privs_add.png)

You should now have the correct user setup for your Drupal installation.
Next we need to modify your settings.php file to connect to your new
Cloud Server database.



<span class="mw-headline">Modifying settings.php</span>
-------------------------------------------------------

We need to modify the settings.php file of your existing Drupal
installation and tell it to point to a new database server. The file
will be located in **/yoursite.com/web/content/sites/default/**. If you
have created your Drupal installation under a sub-directory your path
may be slightly different. Download the **settings.php** file to your
local computer and open it in your favorite text editor. If you are on
Windows you can simply use Notepad, TextEdit works on the Macintosh.

The line that we are looking for looks similar to this:

    $db_url = 'mysqli://388448_drupal:MySecurePassword@mysql50-61.wc1.dfw1.stabletransit.com/388448_drupal';

The line should be around line number 92 if your editor counts lines.

You will need to change the portion that reads
*mysql50-61.wc1.dfw1.stabletransit.com* to match your Cloud Server's IP
address. An example of a newly formatted connection string would look
like this:

    $db_url = 'mysqli://388448_drupal:MySecurePassword@67.23.6.28/388448_drupal';

Once you make the change save your file. Upload it to your website and
replace the existing *settings.php* file. *If you receive an error
overwriting the file you may need to change the permissions to 744 with
your FTP program.*



<span class="mw-headline">Modify MySQL Configuration</span>
-----------------------------------------------------------

If you were to try your site right now it would not work and would
eventually tell you the site is offline. MySQL by default does not allow
external connections -- we need to change this! To do this we will
modify the MySQL configuration and tell it to no longer bind to
localhost only. To do this you will need to SSH to your server as we did
previously, in fact you may still have it open. On your server type the
following command to modify the configuration:

    # nano /etc/mysql/my.cnf

*Be sure to run this as the root user!*

You will be presented with the nano text editor and your MySQL
configuration file. Scroll down to the line that looks like this:

    bind-address            = 127.0.0.1

We need to comment out this line by placing a pound symbol (\#) in front
of it. The new line should look like this:

    #bind-address            = 127.0.0.1

Save the file by pressing **CTRL-X** followed by **Y**. When asked for
the file name just press **Enter**.

Now we need to restart the MySQL service. You can do this by simply
typing:

    # /etc/init.d/mysql restart

You should see the following output:

     * Stopping MySQL database server mysqld                                 [ OK ]
     * Starting MySQL database server mysqld                                 [ OK ]
     * Checking for corrupt, not cleanly closed and upgrade needing tables.

If you see any errors or \[FAIL\] you may have mistyped in the
configuration file.



<span class="mw-headline">Test Your Installation</span>
-------------------------------------------------------

It is now time to test your installation. Jump to your Drupal website
and you should be able to login. It may take some time the first
go-around to login -- this is normal.

