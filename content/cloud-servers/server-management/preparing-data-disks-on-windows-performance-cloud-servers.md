---
node_id: 3750
title: Preparing data disks on Windows Cloud Servers
permalink: article/preparing-data-disks-on-windows-performance-cloud-servers
type: article
created_date: '2013-10-31 16:23:23'
created_by: jered.heeschen
last_modified_date: '2015-10-01 15:3609'
last_modified_by: kyle.laffoon
products: Cloud Servers
categories: Server Management
body_format: markdown_w_tinymce
---

The data disks attached to some Cloud Servers flavors, specifically I/O flavors, are unformatted when created.  Before you can use them to hold data on Windows, they have to be prepared by formatting them and assigning each a drive letter.

1. Open the Server Management interface.

    - On Windows Server 2008, right-click the computer's icon and select Manage.

    - On Windows Server 2012, click the Server Manager button on the taskbar.

2. Navigate to the list of the system's attached storage volumes.
 
    - On Windows Server 2008, select Storage in the left panel, then select Disk Management.

    - On Windows Server 2012, select File and Storage Services in the left panel, then select Disks.

3. For each unassigned disk in the list, delete any existing partitions.

    - On Windows Server 2008, the disk will be displayed in the lower pane with any existing partitions.  Right-click an existing partition (if any) and select Delete to remove it.

    - On Windows Server 2012, right-click the drive and select Bring Online.  When the disk is online, right-click the disk and select Reset Disk to ensure all disk space is available for your use.

3. For each unassigned disk in the list, run the New Volume Wizard to format it as NTFS and assign it a drive letter.

    - On Windows Server 2008, right-click the disk's unallocated space in the lower pane and select "New Simple Volume".

    - On Windows Server 2012, right-click the disk and select New Volume.

4. Open the Computer window to view your server's active disks and confirm the new volume or volumes are available.

When all drives are formatted and assigned a drive letter you can install any required software to the appropriate drives.