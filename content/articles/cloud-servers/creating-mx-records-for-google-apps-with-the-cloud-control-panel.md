---
node_id: 2176
title: Creating MX Records for Google Apps through the Cloud Control Panel
type: article
created_date: '2012-09-19 20:59:16'
created_by: lee.jelley
last_modified_date: '2016-01-05 16:5322'
last_modified_by: rose.contreras
product: Cloud Servers
body_format: tinymce
---

In this article we discuss adding [Google
Apps](http://www.google.com/enterprise/apps/business/pricing.html) MX
records to a domain managed via the Cloud Control Panel.

### DNS

If you haven't already, be sure you verify your domain with Google Apps
through their administrative interface.

Once Google has successfully verified the domain the next step will be
to add Googl&rsquo;s MX records to the domain's information in the DNS
section of the [Cloud Control Panel](https://mycloud.rackspace.com/).

### MX

Google Apps provides five MX records to be added to the domain DNS
settings.  You can find the latest MX record values on [the Google Apps
web
site](http://support.google.com/a/bin/answer.py?hl=en&answer=174125).

Once you have the MX records in-hand you'll want to add the records in
the Cloud Control Panel.

If you need help finding the screen to add a record to a domain we have
an article with more details for our [Cloud Control
Panel](/knowledge_center/article/creating-a-dns-records-for-cloud-servers-next-generation-control-panel).

Once we're on the&ldquo;Add DNS Recor&rdquo; screen we should be able to fill in
the necessary information for each record.  Let's have a look at the
interface in the control panel:

![](http://www.rackspace.com/knowledge_center/sites/default/files/field/image/addrecord.png)

As in the example above, you'll need to select "MX Record" as the record
type to create a Mail Exchanger record for inbound email. Start with the
first record on Google's list, which at the time of this writing is
ASPX.L.GOOGLE.COM, and assign the priority Google recommends for that
record (the number listed before the domain name on Google's table of MX
entries).

Don't include a period at the end of the mailserver domain when you
enter it.  The system will add that for you behind the scenes if it's
required.

Once you're done entering the first MX record repeat the process for the
other four MX records.

### Check and Test

Now that the MX records have been stored within the DNS settings for
your domain, the changes should propagate after the time specified in
the TTL has passed.  You can test your changes with a DNS checker.

Now that we can see the MX records have propagated correctly we can run
an email test.

Send an email through the Google Apps webmail interface to an email
address you can access on a different domain, then reply to it.  If the
email to your domain gets back to Google Apps you'll know the DNS
changes worked.

### Summary

Google Apps allows for email service using your own domain for free,
which can be useful when deciding whether to host email with an email
hosting provider or run your own email environment.

This process is relatively simple to follow and can take up to around 10
minutes to complete, making it an easy way to get email up and running
when yo&rsquo;re in a hurry.
