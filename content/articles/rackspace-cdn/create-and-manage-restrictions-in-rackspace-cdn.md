---
node_id: 4662
title: Create and manage restrictions in Rackspace CDN
permalink: article/create-and-manage-restrictions-in-rackspace-cdn
type: article
created_date: '2015-05-11 15:24:28'
created_by: Rackspace Support
last_modified_date: '2016-01-08 21:1835'
last_modified_by: catherine.richardson
products: Rackspace CDN
body_format: tinymce
---

Restriction rules limit who can see your content. Restriction rules
define the traffic to *allow* or to *block*. (For example, a
**Referrer** value of **website.com** with **Allow** chosen, *allows*
traffic being requested from **website.com**. If **Block** is chosen,
traffic is denied.)

When you create multiple rules, you must order rules from least specific
to most specific.

For more information about rules, see the following sections and
[Rackspace CDN edge
rules](https://www.rackspace.com/knowledge_center/article/rackspace-cdn-edge-rules).

After you create your service, you enter restriction rules in the
**Restrictions** section of the CDN service page.

![](/knowledge_center/sites/default/files/field/image/Screen%20Shot%202015-10-02%20at%2011.52.24%20AM.png)

 

### To create a restriction

After you have created your service, follow these steps to create a
restriction:

1. Click **Add Rule**. A popup dialog box displays.

![](/knowledge_center/sites/default/files/field/image/Screen%20Shot%202015-10-02%20at%2011.54.43%20AM.png)

2. Enter the following information to define the rule:

-   **Name**: A name for the rule.
-   **Type**: **Referrer**, **Geography**, and **Client IP** address are
    the restriction types currently supported. Choose one from the drop
    down menu.
-   **Access**: **Access** enables you to **Allow** or **Block** access
    to your content.
-   **Referrer**: The domain that is allowed to access your edge node
    content. You can enter a URL with or without **http://**.
-   **Path**: Path for the rule. Path defines which content enforces
    your restriction. To apply the restriction to your entire site, use
    the path "/\*"

**Note**: You can add multiple **Referrer** domains that use the same
**Path** by separating the list of domains with a space, as shown in the
following example.

![](/knowledge_center/sites/default/files/field/image/Screen%20Shot%202015-10-02%20at%2012.07.19%20PM.png)

3. Click **Save Rule**. The **Service Status** is **Pending** until the
new restriction is deployed. After the restriction is deployed, it
displays in the **Restrictions**list.

![](/knowledge_center/sites/default/files/field/image/Screen%20Shot%202015-10-02%20at%2012.02.38%20PM.png)

 

### To edit a restriction

To edit a restriction, follow these steps:

1. Click the gear icon beside the rule that you want to edit, and
select **Edit Rule**.

2. Edit the **Name**, **Type**, **Access**, **Referrer**, or the
**Path** for the rule.

![](/knowledge_center/sites/default/files/field/image/Screen%20Shot%202015-10-02%20at%2012.09.39%20PM.png)

3. Click **Save Rule**. The **Service Status** is **Pending** until the
edited restriction is deployed. After the edited restriction is
deployed, it displays in the **Restrictions**list.

 

### To delete a restriction

To delete a restriction, follow these steps:

1. Click the gear icon beside the rule that you want to delete, and
select **Delete Rule**.

2. In the popup dialog box, click **Delete Rule**.

![](/knowledge_center/sites/default/files/field/image/DeleteOriginRule_1.png)

The **Service Status** is **Pending** until the restriction is deleted.
After the restriction is deleted, it is removed from the
**Restrictions** list.

 

#### [\< Create and manage caching rules in Rackspace CDN](https://www.rackspace.com/knowledge_center/article/create-and-manage-caching-rules-in-rackspace-cdn)    -     [Enable or disable logging in Rackspace CDN \>](https://www.rackspace.com/knowledge_center/article/enable-or-disable-logging-in-rackspace-cdn)

 

 

 
