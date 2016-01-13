---
node_id: 1456
title: Create DNS Records for cloud servers with the Control Panel
permalink: article/creating-a-dns-records-for-cloud-servers-next-generation-control-panel
type: article
created_date: '2012-07-13 16:46:26'
created_by: RackKCAdmin
last_modified_date: '2015-12-30 22:0535'
last_modified_by: kyle.laffoon
products: Cloud Servers
body_format: full_html
---

### Previous section

[Getting Started with Cloud
Servers](https://www.rackspace.com/knowledge_center/article/getting-started-with-cloud-servers-0)

 

Creating DNS records for your domain is easy to do within the Cloud
Control Panel. This article provides instructions for creating a DNS
zone for your domain and adding basic A, MX, and CNAME records by using
the Cloud Control Panel. Read [Getting started with Cloud Sites &ndash;
Managing DNS
records](http://www.rackspace.com/knowledge_center/article/getting-started-with-cloud-sites-managing-dns-records)
to learn more about A, MX, and CNAME records for Cloud Sites.

**Contents:**

-   [What are the DNS servers for my Cloud Server?](#H)
-   [Create a DNS zone for your domain](#A)
-   [Add a Domain](#B)
-   [Add an A Record](#C)
-   [Add a CNAME Record](#D)
-   [Add an MX Record](#E)
-   [Delete a Record](#F)
-   [Delete a Domain](#G)

What are the DNS servers for my Cloud Server?
---------------------------------------------

Your DNS servers for Cloud Servers are the following:

-   dns1.stabletransit.com
-   dns2.stabletransit.com

Create a DNS zone for your domain
---------------------------------

Log in to the [Cloud Control Panel](https://mycloud.rackspace.com).

Select **Networking \> Cloud DNS**.

![](/knowledge_center/sites/default/files/field/image/Screen%20Shot%202015-01-16%20at%201.12.55%20PM.png)

Continue with the following procedures to create the records for your
domain's DNS zone.

### Add a Domain

1.  Click **Create Domain**.
2.  In the popup dialog box, enter the following information:
    -   Name of your domain.
    -   Email address publicly associated as the admin and contact for
        the domain.
    -   Time to live (TTL) for the domain.

3.  Click **Create Domain**.

### Add an A Record

An A is an IPv4 address record that you use to point your domain to an
IP address. It is also known as an A name.

1.  On the Cloud DNS page, click the gear icon next to your domain and
    select **Add DNS Record**.
2.  In the popup dialog box, select **A/AAAA Record** for the record
    type.
3.  Enter the following information:
    -   The hostname for your domain (optional).
    -   Target (IP address of the server).
    -   Time to live (TTL). The TTL refers to the time it will take for
        your computer to refresh DNS information. It is referred to in
        seconds of time.

4.  Click **Add Record**.

### Add a CNAME Record

A CNAME record, also known as a canonical name record, is a record type
in the DNS that you use to indicate that your domain name is an alias
for your domain's canonical name. Subdomains and IP addresses for your
domain are defined by the canonical domain.

Use the Common Name (CNAME) record to point to another record.

Click the action gear next to your domain and click **Add DNS Record**.

Select **CNAME Record** for the record type.

-   The hostname for your domain (optional).
-   Target (for your domain)
-   Time to live (TTL).
-   The TTL refers to the time it will take for your computer to refresh
    DNS information. It is referred to in seconds of time.

Click **Add Record**

### Add an MX Record

Use the Mail Exchange (MX) is a DNS record that points to the server
that handles your domain-related email delivery. You create an MX record
for your domain that allows you to set up an email address. For example,
you can create an MX record to create the email address
*user@yourdomain.com*

1.  On the Cloud DNS page, click the gear icon next to your domain and
    select **Add DNS Record**.
2.  In the popup dialog box, select **MX Record** for the record type.
3.  Enter the following information:
    -   The hostname for your domain (optional).
    -   Domain of the mail server.
    -   Priority. The MX record priority is a setting you will use when
        your domain name uses more than one mail server. The priority
        that you set for your MX record affects the load sharing and the
        order in which multiple mail servers are used, and also allows
        the use of primary and backup mail servers.
    -   Time to live (TTL). TTL refers to the time it will take for your
        computer to refresh DNS information. It is referred to in
        seconds of time.

4.  Click **Add Record**.

### Delete a record from your domain

1.  On the Cloud DNS page, click the name of the domain.
2.  On the domain page, scroll down to the Records section, and choose
    one of the following methods to delete a record:
    -   Select the check box next to the record that you want to delete,
        click Actions, and select Delete records. You can use this
        method to delete multiple records at once.

        ![](/knowledge_center/sites/default/files/field/image/Screen%20Shot%202015-01-16%20at%205.29.36%20PM.png)

    -   Click the gear icon next to the record and select Delete Record.

        ![](/knowledge_center/sites/default/files/field/image/Screen%20Shot%202015-01-16%20at%203.27.52%20PM_0.png)

### Delete a domain

Use one of the following methods to delete a domain on the Cloud DNS
page.

Click the gear icon next to the domain, and select **Delete Domain**.

![](/knowledge_center/sites/default/files/field/image/Screen%20Shot%202015-01-16%20at%205.13.13%20PM.png)

Select the check box next to the domain and click **Delete** at the top
of the domain list.

![](/knowledge_center/sites/default/files/field/image/Screen%20Shot%202015-01-16%20at%205.12.52%20PM.png)

 

### Next section

[Using Dig for DNS
Troubleshooting](http://www.rackspace.com/knowledge_center/article/rackspace-cloud-essentials-using-dig-for-dns-verification-and-troubleshooting)
