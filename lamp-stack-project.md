# Lamp Stack Implemetation

## Introduction

A “LAMP” stack is a group of open source software that is typically installed together in order to enable a server to host dynamic websites and web apps written in PHP. This term is an acronym which represents the **L**inux operating system with the **A**pache web server. The site data is stored in a **M**ySQL database, and dynamic content is processed by **P**HP.

**In this guide, you’ll set up a LAMP stack on an Ubuntu 22.04 server on AWS.**

### 🎓 **Pre-requisites:**

- In order to complete this tutorial, you will need to have an Ubuntu 22.04 server with a non-root sudo-enabled user account and a basic firewall. This can be configured using our [AWS account setup and Provisioning an Ubuntu Server](https://www.youtube.com/watch?v=xxKuB9kJoYM&list=PLtPuNR8I4TvkwU7Zu0l0G_uwtSUXLckvh&index=6) and [Connecting to your EC2 Instance](https://www.youtube.com/watch?v=TxT6PNJts-s&list=PLtPuNR8I4TvkwU7Zu0l0G_uwtSUXLckvh&index=7)

- Basic knowledge of Linux OS

## 🎯 Project Objective 

- At the end of this project you should have an improved understanding of the Linux Terminal

- Understand how to allow ports on AWS Security Group

- Have confidence setting up a LAMP Stack

### Let Us Begin 🚀

## 📋 Step 1 — Installing Apache and Updating AWS SECURITY GROUP

The Apache web server is among the most popular web servers in the world. It’s well documented, has an active community of users, and has been in wide use for much of the history of the web, which makes it a great choice for hosting a website.

Start by updating the package manager cache on your ubuntu server using ``apt``:

```shell
sudo apt update
```

Then install Apache with:

```shell
sudo apt install -y apache2
```
Once the installation is finished, you’ll need to adjust your security group settings to allow HTTP traffic on port 80

1. **Access the EC2 Dashboard:**
   Once logged in, navigate to the EC2 Dashboard. You can do this by either searching for "EC2" in the AWS services search bar or by finding "EC2" under "Compute" in the AWS services list.

2. **Select the Appropriate Security Group:**
   In the EC2 Dashboard, select the instance for which you want to open port 80. Under the "Description" tab, find the "Security groups" section, and click on the security group associated with your instance. This will take you to the Security Group page.

3. **Edit the Security Group Inbound Rules:**
   On the Security Group page, navigate to the "Inbound rules" tab. This is where you can configure the rules to allow incoming traffic.

4. **Add a Rule for Port 80 (HTTP):**
   To open port 80 for HTTP traffic, click the "Edit inbound rules" button. Then, click the "Add rule" button to add a new rule. Configure the rule as follows:
   - **Type:** HTTP (80)
   - **Source:** You can specify the source IP range or leave it as 0.0.0.0/0 to allow traffic from any IP address.

6. **Review and Save the Rule:**
   Double-check your rule settings to ensure they are correct. Once you are satisfied, click the "Save rules" or "Save" button to apply the changes.

7. **Confirm the Rule:**
   After saving, the rule will be added to your security group. Make sure that it's properly configured and that the inbound rule for port 80 (HTTP) is present.

***With these steps completed, you have opened port 80 for HTTP traffic in your AWS Security Group, allowing incoming web traffic to reach your Apache EC2 Instance.***

You can do a spot check right away to verify that everything went as planned by visiting your server’s public IP address in your web browser.

```shell
http://your_server_ip
```
The default Ubuntu 22.04 Apache web page is there for informational and testing purposes. Below is an example of the Apache default web page:

![Apache2](./images/lamp-project-1.png)

If you can view this page, your web server is correctly installed and accessible through your firewall.

## 📝 Step 2 —  Installing MySQL

Now that you have a web server up and running, you need to install the database system to be able to store and manage data for your site. MySQL is a popular database management system used within PHP environments.

Again, use ``apt`` to acquire and install this software:

```shell
sudo apt install mysql-server -y
```
When the installation is finished, it’s recommended that you run a security script that comes pre-installed with MySQL. This script will remove some insecure default settings and lock down access to your database system. Hey! There's a warning!

<span style="color:orange">⚠️</span> **Warning!**  As of ``July 2022``, an error will occur when you run the ``mysql_secure_installation`` script without some further configuration. The reason is that this script will attempt to set a password for the installation’s **root** MySQL account but, by default on Ubuntu installations, this account is not configured to connect using a password.

Prior to July 2022, this script would silently fail after attempting to set the **root** account password and continue on with the rest of the prompts. However, as of this writing the script will return the following error after you enter and confirm a password:

**``output``**

```
... Failed! Error: SET PASSWORD has no significance for user 'root'@'localhost' as the authentication method used doesn't store authentication data in the MySQL server. Please consider using ALTER USER instead if you want to change authentication parameters.

New password:
```

This will lead the script into a recursive loop which you can only get out of by closing your terminal window.

To avoid entering this recursive loop, though, you’ll need to first adjust how your root MySQL user authenticates.

First, open up the MySQL prompt:

```shell
sudo mysql
```

Then run the following ``ALTER USER`` command to change the **root** user’s authentication method to one that uses a password. The following example changes the authentication method to ``mysql_native_password``:

```shell
mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

After making this change, exit the MySQL prompt:

```shell
mysql> exit
```
Then, you can run the ``mysql_secure_installation`` script without issue.

```bash
sudo mysql_secure_installation
```
This will ask if you want to configure the ``VALIDATE PASSWORD PLUGIN``.

- Note: Enabling this feature is something of a judgment call. If enabled, passwords which don’t match the specified criteria will be rejected by MySQL with an error. It is safe to leave validation disabled, but you should always use strong, unique passwords for database credentials.

Answer ``Y`` for yes, or anything else to continue without enabling.

```
VALIDATE PASSWORD PLUGIN can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD plugin?

Press y|Y for Yes, any other key for No:
```

If you answer “yes”, you’ll be asked to select a level of password validation. Keep in mind that if you enter ``2`` for the strongest level, you will receive errors when attempting to set any password which does not contain numbers, upper and lowercase letters, and special characters:

```
There are three levels of password validation policy:

LOW    Length >= 8
MEDIUM Length >= 8, numeric, mixed case, and special characters
STRONG Length >= 8, numeric, mixed case, special characters and dictionary              file

Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG: 1
```

Regardless of whether you chose to set up the ``VALIDATE PASSWORD PLUGIN``, your server will next ask you to select and confirm a password for the MySQL root user. This is not to be confused with the **system root**. The **database root** user is an administrative user with full privileges over the database system. Even though the default authentication method for the MySQL root user doesn’t involve using a password, **even when one is set**, you should define a strong password here as an additional safety measure.

If you enabled password validation, you’ll be shown the password strength for the root password you just entered and your server will ask if you want to continue with that password. If you are happy with your current password, enter ``Y`` for “yes” at the prompt:

```
Estimated strength of the password: 100
Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No)
```

For the rest of the questions, press ``Y`` and hit the ``ENTER`` key at each prompt. This will remove some anonymous users and the test database, disable remote root logins, and load these new rules so that MySQL immediately respects the changes you have made.

When you’re finished, test whether you’re able to log in to the MySQL console by typing:

```
sudo mysql
```
This will connect to the MySQL server as the administrative database user **root**, which is inferred by the use of ``sudo`` when running this command. Below is an example output:

```
Output
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 10
Server version: 8.0.28-0ubuntu4 (Ubuntu)

Copyright (c) 2000, 2023, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> 
```
To exit the MySQL console, type:

```
mysql> exit
```

Notice that you didn’t need to provide a password to connect as the **root** user, even though you have defined one when running the ``mysql_secure_installation`` script. That is because the default authentication method for the administrative MySQL user is ``unix_socket`` instead of ``password``. Even though this might seem like a security concern, it makes the database server more secure because the only users allowed to log in as the **root** MySQL user are the system users with sudo privileges connecting from the console or through an application running with the same privileges.

Your MySQL server is now installed and secured. Next, you’ll install PHP, the final component in the LAMP stack. Let's dive right in 🚀

## 📝 Step 3 —  Installing PHP

You have Apache installed to serve your content and MySQL installed to store and manage your data. PHP is the component of our setup that will process code to display dynamic content to the final user. In addition to the ``php`` package, you’ll need ``php-mysql``, a PHP module that allows PHP to communicate with MySQL-based databases. You’ll also need ``libapache2-mod-php`` to enable Apache to handle PHP files. Core PHP packages will automatically be installed as dependencies.

run the following command to install these packages:

```shell
sudo apt install php libapache2-mod-php php-mysql -y
```

You can verify the installation using:

```
php -v
```

```
Output
PHP 8.1.2 (cli) (built: Jun  4 2023 18:13:46) (NTS)
Copyright (c) The PHP Group
Zend Engine v4.1.2, Copyright (c) Zend Technologies
    with Zend OPcache v8.1.2, Copyright (c), by Zend Technologies
```

At this point, your LAMP stack is fully operational, but before testing your setup with a PHP script, it’s best to set up a proper [Apache Virtual Host](https://httpd.apache.org/docs/current/vhosts/) to hold your website’s files and folders.

## Step 4 — Creating a Virtual Host for your Website

When using the Apache web server, you can create virtual hosts (similar to server blocks in Nginx) to encapsulate configuration details and host more than one domain from a single server. In this guide, we’ll set up a domain called **your_domain**, but you should **replace this with your own domain name**.

Apache on Ubuntu 22.04 has one virtual host enabled by default that is configured to serve documents from the ``/var/www/html directory``. While this works well for a single site, it can become unwieldy if you are hosting multiple sites. Instead of modifying ``/var/www/html``, we’ll create a directory structure within ``/var/www`` for the **your_domain** site, leaving ``/var/www/html`` in place as the default directory to be served if a client request doesn’t match any other sites.

Create the directory for **your_domain** as follows:

```
sudo mkdir /var/www/your_domain
```

Next, assign ownership of the directory with the ``$USER`` environment variable, which will reference your current system user:

```
sudo chown -R $USER:$USER /var/www/your_domain
```

Then, open a new configuration file in Apache’s ``sites-available`` directory using your preferred command-line editor. Here, we’ll use ``nano``:

```
sudo nano /etc/apache2/sites-available/your_domain.conf
```

This will create a new blank file. Add in the following bare-bones configuration with your own domain name:

***/etc/apache2/sites-available/your_domain.conf***
---

```
<VirtualHost *:80>
    ServerName your_domain
    ServerAlias www.your_domain 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/your_domain
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

Save and close the file when you’re done. If you’re using ``nano``, do that by pressing ``CTRL+X``, then ``Y`` and ``ENTER``.

With this ``VirtualHost`` configuration, we’re telling Apache to serve ``your_domain`` using ``/var/www/your_domain`` as the web root directory. If you’d like to test Apache without a domain name, you can remove or comment out the options ``ServerName`` and ``ServerAlias`` by adding a pound sign (``#``) the beginning of each option’s lines.

Now, use ``a2ensite`` to enable the new virtual host:

```
sudo a2ensite your_domain
```

You might want to disable the default website that comes installed with Apache. This is required if you’re not using a custom domain name, because in this case Apache’s default configuration would override your virtual host. To disable Apache’s default website, type:

```
sudo a2dissite 000-default
```

To make sure your configuration file doesn’t contain syntax errors, run the following command:

```
sudo apache2ctl configtest
```

Finally, reload Apache so these changes take effect:

```
sudo systemctl reload apache2
```

Your new website is now active, but the web root ``/var/www/your_domain`` is still empty. Create an ``index.html`` file in that location to test that the virtual host works as expected:

```
nano /var/www/your_domain/index.html
```

***/var/www/your_domain/index.html***
---

```
<html>
  <head>
    <title>your_domain website</title>
  </head>
  <body>
    <h1>Hello World!</h1>

    <p>This is the landing page of <strong>your_domain</strong>.</p>
  </body>
</html>
```