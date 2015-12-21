---
node_id: 4229
title: 'Vyatta vRouter: Allow an IP address to access the vRouter via SSH'
permalink: article/vyatta-vrouter-allowing-ip-to-access-the-vrouter-via-ssh
type: article
created_date: '2014-09-09 20:34:04'
created_by: sameer.satyam
last_modified_date: '2015-02-18 20:3452'
last_modified_by: rose.contreras
products: Cloud Servers
categories: Security Tools
body_format: markdown_w_tinymce
---

This article demonstrates how to configure an IP address to connect to a Brocade Vyatta vRouter through SSH, for administration purposes.

## Connect to the vRouter

Access the vRouter remotely or through the console. For instructions, see [Managing access to the Vyatta vRouter](https://www.rackspace.com/knowledge_center/article/managing-access-to-the-vyetta-router).

**Note:** After you've accessed the vRouter, you should add a local user. Follow the procedure described in [Vyatta vRouter: Adding a local administrative user](https://www.rackspace.com/knowledge_center/article/vyatta-vrouter-adding-a-local-administrative-user). If you are not logged in via SSH as the user *Vyatta* or as an administrative user, then access the vRouter remotely or through the console, then add a local user. Follow the procedure at [Vyatta vRouter: Add a local administrative user}()


## Add the IP address to the SSH group

After you are logged in to the vRouter, add the IP address to the <code>VYATTA-SSH-ALLOW</code> group, as follows:

    set firewall group network-group VYATTA-SSH-ALLOW network 1.1.1.1/32

The <code>VYATTA-SSH-ALLOW</code> group contains the IP addresses that Rackspace uses to connect to this device. This group is also applied to a firewall that protects traffic destined for the vRouter itself. Do not remove this group.

Verify that the group is applied to the vRouter's local firewall of the public interface, as follows:

    vyatta@vya-1:~$ show configuration commands | grep local
	set interfaces ethernet eth0 firewall local name 'PUBLIC-LOCAL-IN'

    vyatta@vya-1:~$ show configuration commands | grep PUBLIC-LOCAL-IN
	set firewall name PUBLIC-LOCAL-IN rule 6 action 'accept'
	set firewall name PUBLIC-LOCAL-IN rule 6 destination port '22'
	set firewall name PUBLIC-LOCAL-IN rule 6 protocol 'tcp'
	set firewall name PUBLIC-LOCAL-IN rule 6 source group network-group 'VYATTA-SSH-ALLOW'

## More information about SSH

[Connecting to a server using SSH on Linux or Mac OS](http://www.rackspace.com/knowledge_center/article/connecting-to-a-server-using-ssh-on-linux-or-mac-os)

[Rackspace Cloud Essentials - Checking a server’s SSH host fingerprint with the web console](http://www.rackspace.com/knowledge_center/article/rackspace-cloud-essentials-checking-a-server’s-ssh-host-fingerprint-with-the-web-console)

[Generating RSA Keys With SSH - PuTTYgen](http://www.rackspace.com/knowledge_center/article/generating-rsa-keys-with-ssh-puttygen)

<p>&nbsp;</p>