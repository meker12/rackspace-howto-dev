---
node_id: 360
title: Installing an SSL certificate on Apache
permalink: article/installing-an-ssl-certificate-on-apache
type: article
created_date: '2011-03-16 21:57:40'
created_by: RackKCAdmin
last_modified_date: '2013-08-14 21:0325'
last_modified_by: rose.contreras
products: Cloud Servers
body_format: tinymce
---

This article is a continuation of [Generate a
CSR](/knowledge_center/index.php/Generate_a_CSR "Generate a CSR") and
will take you from creating and receiving your SSL cert from your
authority of choice to installing it in apache. I've chosen to Apache
since it is the most common web server on Linux and the Internet. Again,
I'm pulling the majority of this documentation from RapidSSL.com which
is a great place to buy a certificate if you haven't already chosen:

[http://www.rapidssl.com/ssl-certificate-support/install-ssl-certificate/apache\_2x.htm](http://www.rapidssl.com/ssl-certificate-support/install-ssl-certificate/apache_2x.htm "http://www.rapidssl.com/ssl-certificate-support/install-ssl-certificate/apache_2x.htm")

* * * * *

+--------------------------------------------------------------------------+
| Contents                                                                 |
| --------                                                                 |
|                                                                          |
| -   [1 Prerequisites](#Prerequisites)                                    |
| -   [2 Installing your SSL                                               |
|     Certificate](#Installing_your_SSL_Certificate)                       |
|     -   [2.1 Copy the files in into the default                          |
|         locale](#Copy_the_files_in_into_the_default_locale)              |
|     -   [2.2 Edit the httpd.conf](#Edit_the_httpd.conf)                  |
| -   [3 iptables](#iptables)                                              |
| -   [4 Restart Apache](#Restart_Apache)                                  |
+--------------------------------------------------------------------------+

Prerequisites
-------------

Keep in mind besides having apache and mod\_ssl installed, you will need
to have an IP address for this SSL cert and a unique IP address for each
SSL that you want to host. Certificate authorities and browsers require
that all SSL certs be on their own IP address.

Installing your SSL Certificate
-------------------------------

### Copy the files in into the default locale

When you receive your SSL certificate from your authority, upload it to
your server and place it in \~/domain.com.ssl/domain.com.crt

-   Copy the certificate, key, and csr into the Apache server directory
    in which you plan to store your certificates (by default:
    /usr/local/apache/conf/ssl.crt/ or /etc/httpd/conf/ssl.crt/).

**Note: Copy the entire contents of the certificate from (and including)
the -----BEGIN CERTIFICATE----- and -----END CERTIFICATE----- lines.**

### Edit the httpd.conf

Open the Apache httpd.conf file in a text editor(I prefer VIM, the true
editor).

Create the following Virtual Host:

    <VirtualHost 123.45.67.89:443>
    ServerName www.domain.com
    DocumentRoot /path/to/your/document/root/htdocs

    SSLEngine ON
    SSLCertificateFile /etc/httpd/conf/ssl.crt/domain.com.crt
    SSLCertificateKeyFile /etc/httpd/conf/ssl.key/domain.com.key

    ErrorLog logs/ssl.domain.com.error_log
    CustomLog logs/ssl.domain.com.access_log combined
    </VirtualHost>

-   **keep in mind that the paths to the certificate files will need to
    be changed to where ever you choose to place your certificate.**

Save the changes and exit the editor.

Save the changes and exit the editor.

iptables
--------

You may need to open a port in your firewall to allow SSL connections to
port 443.  To check, get a list of your firewall rules:

    sudo /sbin/iptables -L

If you have iptables active but it doesn't have any exceptions for port
443, we'll have to add some:

    sudo /sbin/iptables -I INPUT -p tcp --dport 443 -m state --state NEW,ESTABLISHED -j ACCEPT
    sudo /sbin/iptables -I OUTPUT -p tcp --sport 443 -m state --state ESTABLISHED -j ACCEPT

Remember to add the rules to your iptables config file or, on Red
Hat-based distributions, run:

    sudo /sbin/service iptables save

Restart Apache
--------------

Restart your apache web server:

    # /etc/init.d/httpd restart
    or
    # /etc/init.d/apache2 restart

Test your certificate by using a browser to connect to your server. Use
the https protocol directive (e.g. https://your server/) to indicate you
wish to use secure HTTP.

Note: The padlock icon on your browser will be displayed in the locked
position if your certificates are installed correctly and the server is
properly configured for SSL.
