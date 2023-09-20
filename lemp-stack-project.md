# Web Stack Implementation (Lemp Stack)

## What is a LEMP Stack?

The Ubuntu LEMP stack serves as a substitute for the original [LAMP Stack](https://en.wikipedia.org/wiki/LAMP_%28software_bundle%29). Both stacks consist of the Linux operating system, a web server, a database, and a programming/scripting language. Both stacks allow users to host web applications and implement a fully-functional programming environment. Additionally, the main components of both the LAMP and LEMP stacks can be installed using the default Ubuntu software repository.

The original LAMP Stack includes Linux, [Apache](https://httpd.apache.org/docs/2.4/), [MySQL](https://dev.mysql.com/), and [PHP](https://www.php.net/). The Ubuntu LEMP stack alternative continues to use Linux and PHP, but it includes the [NGINX](https://docs.nginx.com/nginx/admin-guide/web-server/) web server instead of Apache. In most cases, a LEMP stack uses the [MariaDB](https://mariadb.org/) database, although MySQL can also be used.

## Before You Begin 🚀

1. In order to complete this tutorial, you will need to have an Ubuntu 22.04 server with a non-root sudo-enabled user account and a basic security group configuration. This can be configured using our [AWS account setup and Provisioning an Ubuntu Server](https://www.youtube.com/watch?v=xxKuB9kJoYM&list=PLtPuNR8I4TvkwU7Zu0l0G_uwtSUXLckvh&index=6) 

2. Follow our guide on how to access your EC2 Instance [Connecting to your EC2 Instance](https://www.youtube.com/watch?v=TxT6PNJts-s&list=PLtPuNR8I4TvkwU7Zu0l0G_uwtSUXLckvh&index=7)

3. You must have completed projects 1 - 3 Linux, Git, and LAMP.

This guide explains how to install and configure a LEMP stack on Ubuntu 22.04 LTS. It also provides some background about the LEMP stack and how it contrasts with a LAMP stack. Therefore, at the end of this exercise you have a thorough understanding of LAMP & LEMP Stacks and how they differ from each other.

### How to Install LEMP Stack on Ubuntu

This section explains how to install and configure the LEMP Stack on Ubuntu 22.04 LTS. The various LEMP stack components can be installed using the ``apt`` utility. To install the LEMP stack, follow these steps. In all cases, enter ``y`` to proceed with the installation when Ubuntu asks for confirmation.

1. Use ``apt`` to update the Ubuntu packages.

```
sudo apt update && sudo apt upgrade
```

2. Install the NGINX server.

```
sudo apt install nginx
```

3. Confirm NGINX is properly running using the ``systemctl`` utility.

```
sudo systemctl status nginx
```
---
**``output``**
---
```
nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
     Active: active (running) since Wed 2023-09-20 11:00:50 UTC; 14s ago
       Docs: man:nginx(8)
```

