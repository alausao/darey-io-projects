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

## Step 1 — Installing Apache and Updating the Firewall [AWS SECURITY GROUP]

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

