---
node_id: 3572
title: Provisioning cloud resources when migrating from Amazon Web Services
permalink: article/provisioning-cloud-services-to-migrate-from-amazon-web-services
type: article
created_date: '2013-07-02 13:40:58'
created_by: RackKCAdmin
last_modified_date: '2015-01-12 22:2441'
last_modified_by: kyle.laffoon
products: 'Cloud Hosting,Cloud Servers'
categories: Migrations
body_format: markdown_w_tinymce
---

This article describes how to provision your Rackspace Cloud services when migrating from Amazon Web Services (AWS). For the purposes of this article, it is assumed that you are familiar with the [equivalent services between AWS and Rackspace Cloud](http://www.rackspace.com/knowledge_center/article/mapping-of-amazon-web-services-resources-to-rackspace-resources) and that you are generally familiar with the <steps involved in a migration>.

Perform the following procedures to provision and configure your cloud instances:

- [Provision a cloud server]("#provision")
- [Create a customer password (optional)]("#root")
- [Add Cloud Block Storage (optional)]("#addblock")
- [Create a Cloud Files container (optional)]("#filecontainer")
- [Create a Cloud Database instance (optional)]("#createinstance")
- [Connect to the cloud server]("#connectserver")
- [Migrate your data]("migrate")

<a name="provision"> </a>
### Provision a new cloud server

1. Log in to the [Rackspace Cloud Control Panel](https://mycloud.rackspace.com)

2. On the Cloud Servers page, click **Create Server**.

3. Name the server and select a region for it.

4. Select an OS that matches your OS from AWS.

    **Note**: If your Amazon Elastic Compute Cloud (EC2) instance is Amazon Linux, select CentOS 5.0 or later. Amazon Linux is based on Red Hat Enterprise Linux 5.
   
5. Select the size (flavor) that matches your EC2 instance (RAM and disk space), and click **Create Server**.
    For information about instance size mapping, see [Mapping of Amazon Web Services resources to Rackspace resources](/knowledge_center/article/mapping-of-amazon-web-services-resources-to-rackspace-resources#instancetypes).
	
	**Note**: You can add more storage to your cloud server after it is created by adding a Cloud Block Storage volume. For instructions, see [Add Cloud Block Storage]("#addblock") (below).
6. When your root admin password is displayed, copy the password to a secure location, and then click **Dismiss Password**.

<a name="root"> </a>

It is important that you copy and save your root admin password for future reference. You need this password to log in to your server. After you click **Dismiss Password**, the password will not be displayed again.

### Create a custom password (optional)

You can create a custom password for you sever.

1. On the Cloud Servers page in the Cloud Control Panel, click the gear icon next to the server in the server list and select **Change Password**. 
2. Enter a new password and click **Change Password**.

<a name="addblock"> </a>
### Add a Cloud Block Storage (optional)

If you had additional Amazon Elastic Book Store (EBS) volumes attached to your server, or if you prefer to have more storage space for your server, add additional Cloud Block Storage volumes as follows:</p>

1. In the Cloud Control Panel, open the server's detail page.
2. In the **Storage Volumes** section, click **Create Volume**.
3. Name the volume, select its type (SATA or SSD), and select the size.
4. Click **Create Volume**.

    <img alt="" height="349" src="/knowledge_center/sites/default/files/field/image/Step%201-3.png" width="543" />

<a name="filecontainer"> </a>
### Create a Cloud Files container (optional)

If you plan to use a Cloud Files container for the application, to back up files, or to assist with your application migration, create your container now.

1. At the top of the Cloud Control Panel window, click **Storage**.

2. In the popup menu, under **Object Storage and CDN**, select **Files**.

3. On the **Cloud Files/Containers** page, click **Create Container**.

4. Name the container, assign it to the same region as the server that you created, and select the container type.

5. Click **Create Container**.


<a name="createinstance"> </a>
### Create a Cloud Databases instance (optional)

If you will not be setting up your own database server, create a Cloud Databases instance.

1. At the top of the Cloud Control Panel window, click **Databases**.

2. In the popup menu, select **Database Instances**. 

3.On the Cloud Databases page, click **Create Instance**.
 
4. Name the instance and assign it to the same region as your server.

5. Select the type of database instance (datastore), and specify its size (in RAM and disk space).

6. (Optional) Add your first database by assigning it a name, user name, and password. 
    **Note:**You cannot name your user as root.

7. Click **Create Instance**.

<name="connectserver"> </a>
### Connect to the Cloud Server

1. On the Cloud Servers page in the Control Panel, click the name of your server. 

2. Under **Networks**, note the <strong>PublicNet (Internet) IPv4</strong> address.

3. Using SSH, connect to your cloud server by using the following command and the PublicNet address:

        ssh root@&lt;ip_address&gt;

    If you're connecting from a Windows computer, [use PuTTY](http://www.rackspace.com/knowledge_center/article/rackspace-cloud-essentials-3-going-from-windows-to-linux-using-putty") or a similar SSH command to connect to your server's IP address.

4. Enter your root password to log on.

<a name="migrate"> </a>
### Migrate your data

After your Rackspace Cloud services are provisioned, you can build your applications and transfer your data from AWS. The following articles provide detailed descriptions of migration scenarios:

- Applications built on a LAMP stack - [Migrating an Application Built on a LAMP Stack from Amazon Web Services](https://admin.rackspace.com/knowledge_center/article/migrating-an-application-built-on-a-lamp-stack-from-amazon-web-services)

- .NET applications - [Migrating a .NET application from Amazon Web Services](/knowledge_center/article/migrating-a-net-application-from-amazon-web-services)

- Java web applications [Migrating a Java Web Application from Amazon Web Services](/knowledge_center/article/migrating-a-java-web-application-from-amazon-web-services)

- Node.js applications - [Migrating an Application Based on Backbone.js, Node.js, and MongoDB from Amazon Web Services](/knowledge_center/article/migrating-an-application-based-on-backbonejs-nodejs-and-mongodb-from-amazon-web-services)

<p>&nbsp;</p>