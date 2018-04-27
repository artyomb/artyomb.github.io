---
layout: post
title:  "Create SSL certificate simple way"
date:   2018-04-26 11:53:23 +0300
categories: linux ssl
comments: true
---

It is possible to create SSL certificates for client, server and root ca with openssl only in a single line.

## Openssl
I often had to quickly create client/server SSL certificates to setup HTTP server, Jabber, OpenVPN etc.
I was looking for the way to complete it without **easy-rsa** or similar tools.  

I spent some time to find the right params for **openssl** and I'd like to share my scripts. 
The is a trade off between simplicity and flexibility but I hope these scripts will help you make the job done.

There are three script:  
- **make_ca.sh**
  To create new CA certificate (self-signed)
- **make_server.sh** 
  To create server certificate, and sign it with CA
- **make_client.sh**
  To create client certificate, and sign it with CA
  
Each script contains the debug section. It is used to print out information about just created certificates. 
You may definitely cat it out.

Please feel free to comment and fix me if you want!
**GitHub.Gists** <https://gist.github.com/artyomb/05b2282b566214967545d7569050a746>

<script src="https://gist.github.com/artyomb/05b2282b566214967545d7569050a746.js"></script>