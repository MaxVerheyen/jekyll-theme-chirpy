---
title: Why Docker > MAMP
author: Max Verheyen
date: 2020-07-08 22:33:00 +0800
categories: [Blogging, Demo]
tags: [localhost, WordPress]
---

If you want to set up a local development environment for a CMS like WordPress for example, MAMP might seem like an easy option compared to setting up a virtual machine platform with containers like Docker.

First i will show you how to setup WordPress with MAMP, then i will explain how to do it with Docker and why it offers many advantages compared to MAMP.

## 1. Setting up a local WordPress with MAMP

### 1.1 Download and install MAMP

Download and install the latest version of [MAMP](https://www.mamp.info/en/).

After successful installation you can launch your local servers. Start MAMP and click on the Start Servers button. In the status display in the upper right corner, the launch status of the servers is displayed. If necessary, you will be asked for your administrator password.

The web server (Apache) starts by default on port 8888, the database server (MySQL) on port 8889. When calling your web page in a web browser, you must enter the Apache port at the end of the URL, e.g.: http://localhost:8888

![upload-image]({{ "/assets/img/sample/MAMP.png" | relative_url }})

- **Cloud**
Open up the MAMP Cloud Functions. See the Cloud section for more details.

- **Open WebStart page**
Open the start page of your local web server.

- **Start Servers / Stop Servers**
Start or stop the Apache/Nginx and MySQL services of MAMP.

### 1.2 Download WordPress and setup document root

**Mac**

Download [WordPress](https://wordPress.org/download/). After downloading, the resulting zip file should be in your `~/Downloads` folder. Unzip this WordPress.zip file. You should now see a `~/Downloads/WordPress` folder. Give this folder your repository name and move it to `/Applications/MAMP/htdocs`.

**Windows**

Download [WordPress](https://wordPress.org/download/). After downloading, the resulting zip file should be in your `C:\Downloads` folder. Unzip this WordPress.zip file. You should now see a `C:\Downloads\WordPress` folder. Give this folder your repository name and move it to `C:\MAMP\htdocs`.

### 1.3 Create a Database in phpMyAdmin

Click on Open Start Page, then on the phpMyAdmin link. Create a database in phpMyAdmin and call it “wordpress”.

![upload-image]({{ "/assets/img/sample/phpMyAdminAddWordPress.png" | relative_url }})

### 1.4 Install WordPress

Go to http://localhost:8888/repository 

You should now see the WordPress installation process begin.

The following fields are the default for the MAMP MySQL installation, user name: “root”, password: “root”, database host: “localhost:8889” (Use only “localhost” if your MySQL port is 3306)

![upload-image]({{ "/assets/img/sample/WordPressWizard.png" | relative_url }})

Finish the WordPress installation process. The “admin” is your WordPress administrator. You can use a different user name for the administrator.

## 2. Setting up a local WordPress with Docker

### 1.1 Download and install Docker

**Mac**

Download [Docker](https://hub.docker.com/editions/community/docker-ce-desktop-mac/). After succesful double-click Docker.app in the Applications folder to start Docker.

The Docker menu in the top status bar indicates that Docker Desktop is running, and accessible from a terminal.

![upload-image]({{ "/assets/img/sample/whale-in-menu-bar.png" | relative_url }})

**Windows**

Download [Docker](https://hub.docker.com/editions/community/docker-ce-desktop-windows/) After succesful installation, search for Docker, and select Docker Desktop in the search results to start it.

When the whale icon in the status bar stays steady, Docker Desktop is up-and-running, and is accessible from any terminal window.

![upload-image]({{ "/assets/img/sample/whale-icon-systray.png" | relative_url }})

After you’ve successfully installed Docker Desktop, open a terminal and run `docker --version` to check the version of Docker installed on your machine.

```terminal
$ docker --version
Docker version 19.03.5, build 633a0ea
```

### 1.2 Setup document root

You will need to create a repository that contains a [docker-compose.yaml](https://gist.github.com/bradtraversy/faa8de544c62eef3f31de406982f1d42) file in it's root. Edit the credentials in the file if desired.

The docker-compose file needs to contain a MySQL, phpMyAdmin and WordPress image to be able to run WordPress.

```sh
repository/
└── docker-compose.yaml
```

- You can browse and create your own images at [hub.docker.com](https://hub.docker.com/search?q=&type=image)

- More [documentation](https://docs.docker.com/compose/) about docker-compose.yaml

### 1.3 Start up containers with docker-compose

Open a terminal and run `docker-compose up -d` from your repository.

If you used the docker-compose.yaml that was provided, you should now be able to access your WordPress site by visiting [http://localhost:8000](http://localhost:8000) and your phpMyAdmin panel by visiting [http://localhost:8080](http://localhost:8080) as specified in the docker-compose.yaml file.

Finish the WordPress installation process.

## Speed up your workflow with Docker

As you have followed this tutorial you will notice that Docker did a couple of things for us.

- Automatically download and unzip the latest version of WordPress

- Automatically create and connect a database