---
node_id: 542
title: Does the Cloud Sites FTP service support restarts/continuations?
permalink: article/does-the-cloud-sites-ftp-service-support-restartscontinuations
type: article
created_date: '2011-03-16 21:57:40'
created_by: RackKCAdmin
last_modified_date: '2011-09-07 15:2916'
last_modified_by: matt.wheeler
products: Cloud Sites
body_format: tinymce
---

The Cloud Sites FTP service does support resumable uploading. This means
that if there is a connection failure during an upload, it does not have
to be started from the beginning. The ftp client may need to be
configured appropriately to permit this.
