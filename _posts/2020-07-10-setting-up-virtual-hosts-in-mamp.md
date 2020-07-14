---
title: Setting up Virtual Hosts in MAMP
author: Max Verheyen
date: 2020-07-10 23:25:00 +0200
categories: [Localhost, 2. Custom Domain]
tags: [Localhost, MAMP, Apache]
---

By following these steps you will be able to set up custom domains and remove the :8888 from you localhost domain. When you are developing locally it's a good idea to run your site on a similar domain compared to your live environment.

## Configure your ports

Open your MAMP preferences and make sure you are running Apache.

![upload-image]({{ "/assets/img/sample/server.png" | relative_url }})

Make sure your Apache Port is set to 80. The default port for MySQL is 3306.

![upload-image]({{ "/assets/img/sample/ports.png" | relative_url }})

## Listen to port 80

Go to `/Applications/MAMP/conf/apache/httpd.conf` and open the file with a text editor.
Find these lines in the file (they won't be next to each other):

```
Listen 8888
ServerName localhost:8888
```

Change to:

```
Listen 80
ServerName localhost:80
```

## Allow Virtual Hosts

Find these lines in that same `httpd.conf` file (they will be next to each other):

```
# Virtual hosts
#Include /Applications/MAMP/conf/apache/extra/httpd-vhosts.conf
```

Uncomment the code by removing the hash symbol.

```
# Virtual hosts
Include /Applications/MAMP/conf/apache/extra/httpd-vhosts.conf
```

## Allow SymLink override

Find the `FollowSymLinks` directory in that same `httpd.conf` file.

```
<Directory />
    Options Indexes FollowSymLinks
    AllowOverride None
</Directory>
```

Change None to All.

```
<Directory />
    Options Indexes FollowSymLinks
    AllowOverride All
</Directory>
```
## Add Virtual Host paths

Go to `/Applications/MAMP/conf/apache/extra/httpd-vhosts.conf` and open the file in an editor.

```
<VirtualHost *:80>
 ServerName localhost
 DocumentRoot /Applications/MAMP/htdocs
</VirtualHost>
```

Add custom domains:

```
<VirtualHost *:80>
  ServerName website1.dev
  DocumentRoot "/Applications/MAMP/htdocs/website1"
</VirtualHost>

<VirtualHost *:80>
  ServerName website2.dev
  DocumentRoot "/Applications/MAMP/htdocs/website2"
</VirtualHost>
```
> For any of the changes made to MAMP config files to take effect, you will have to restart your MAMP servers.

## Allow your computer to recognize your local domain

A Hosts file is a file that almost all computers and operating systems can use to map a connection between an IP address and domain names.

You have to open the file with administrator rights to be able to edit it (include `sudo` and enter your admin password when asked).

Open up a terminal and edit the `/etc/hosts` file with an editor you feel comfortable using. 

`sudo nano /etc/hosts` Opens the file with Nano inside the terminal.

`sudo pico /etc/hosts` Opens the file with Pico inside the terminal.

`sudo code /etc/hosts` Opens the file with Visual Studio Code (requires Shell Command : Install 'code' in PATH).

Make sure the file contains:

```
127.0.0.1 localhost
```

Add your custom domains:

```
127.0.0.1 website1.dev
127.0.0.1 website2.dev
```

> On Windows the Hosts file can be easily located under `C:\Windows\System32\Drivers\etc\hosts`.