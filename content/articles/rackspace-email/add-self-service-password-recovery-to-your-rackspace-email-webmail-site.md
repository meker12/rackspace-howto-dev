---
node_id: 4446
title: Add self-service password recovery to your Rackspace Email Webmail site
permalink: article/add-self-service-password-recovery-to-your-rackspace-email-webmail-site
type: article
created_date: '2014-11-26 14:27:54'
created_by: brian.hazzard
last_modified_date: '2015-09-14 21:2711'
last_modified_by: kelly.holcomb
products: Rackspace Email
body_format: full_html
---

You can enable Rackspace Email users to change their passwords without
contacting an administrator. To do this, you must first [enable mobile
phone collection for your private label Webmail
site](/knowledge_center/node/4385). Then, you follow the steps in this
article to link to the self-service password recovery from your
Rackspace Email Webmail site login page.

For direct customers
--------------------

To link to the self-service password recovery, add a line of HTML code
to your private label login page, as follows:

1.  Log in to
    [https://cp.rackspace.com](https://cp.rackspace.com "https://cp.rackspace.com").
2.  Click **Rackspace Email**.
3.  Click **Webmail Sites**.
4.  Click **Login/Logout Pages**.
5.  Add the following html code between the \<body\> and \</body\> tags.

        <a href="/forgot-password" id="forgot_password">Forgot Password?</a>

6.  Click **Save**.

For resellers
-------------

To link to the self-service password recovery, add a line of HTML code
to your private label login page, as follows:

1.  Log in to
    [https://cp.rackspace.com](https://cp.rackspace.com "https://cp.rackspace.com").
2.  Click **Reseller Tools**.
3.  Click **Webmail Sites**.
4.  Choose a Webmail site and click **Customize**.
5.  Click **Login/Logout Pages**.
6.  Add the following html code above between the \<body\> and \</body\>
    tags.

        <a href="/forgot-password" id="forgot_password">Forgot Password?</a>

7.  Click **Save**.

