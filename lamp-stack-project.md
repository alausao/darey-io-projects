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

⚠️ As of ``July 2022``, an error will occur when you run the ``mysql_secure_installation`` script without some further configuration. The reason is that this script will attempt to set a password for the installation’s **root** MySQL account but, by default on Ubuntu installations, this account is not configured to connect using a password.

Prior to July 2022, this script would silently fail after attempting to set the **root** account password and continue on with the rest of the prompts. However, as of this writing the script will return the following error after you enter and confirm a password:

**``output``**

```
<b>output</b>
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

Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG: <b>1</b>
```

Regardless of whether you chose to set up the ``VALIDATE PASSWORD PLUGIN``, your server will next ask you to select and confirm a password for the MySQL root user. This is not to be confused with the **system root**. The **database root** user is an administrative user with full privileges over the database system. Even though the default authentication method for the MySQL root user doesn’t involve using a password, **even when one is set**, you should define a strong password here as an additional safety measure.

If you enabled password validation, you’ll be shown the password strength for the root password you just entered and your server will ask if you want to continue with that password. If you are happy with your current password, enter ``Y`` for “yes” at the prompt:

```
Estimated strength of the password: <b>100</b>
Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No)
```

Estimated strength of the <b>password</b>: 100
Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No)


