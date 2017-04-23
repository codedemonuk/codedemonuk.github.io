---
title: "Setting up a Chef Server on Ubuntu"
date: 2017-04-22 19:00
categories:
- Infrastructure as Code
- Chef
- Desired State Configuration
---

This tutorial will assume that you already have an LTS instance of Ubuntu Server running as a pysical machine or virtual machine.
Full [instructions for installing Ubuntu Server][1] are available on the [Ubuntu website][2].

## Download and Install Chef Server

From the [Chef Server Downloads][3] page, download the latest stable version of Chef for your operating system.
You can use either [Wget][4] or [Curl][5] for this.

```bash
wget https://packages.chef.io/files/stable/chef-server/12.14.0/ubuntu/16.04/chef-server-core_12.14.0-1_amd64.deb
```

Then use DPKG to install the package file into Ubuntu.

```bash
sudo dpkg -i chef-server-core_12.14.0-1_amd64.deb
```

Once Chef has been installed, you can verify it by running the command `chef-server-ctl`.

## Reconfiguring Chef

So far you have installed the basic commands for Chef, but you will not have a working Chef server yet.
To get that you will need to reconfigure chef with the following command:

```bash
sudo chef-server-ctl reconfigure
```

This will take a number of minutes and set up Chef on your server, and will use Chef to install the various dependencies such as PostgreSql, RabbitMQ, etc.

At this point you can browse to the Chef server on port 80, but will see a page informating you that until you install the management console, there will not be much for you to see.

![Empty Chef site](/assets/img/looking-for-chef-server.png)

## Set up your admin users and organisations

You will now need to create a an administrative user with the Chef `user-create` command.
You will need to provide your username, forename, surname, email address, password and a location for it to store the generated certificate.

```bash
sudo chef-server-ctl user-create pervezchoudhury Pervez Choudhury junk-mail@thinkbinary.co.uk p@ssw0rd --filename /home/pervezchoudhury/chef-certs/pervezchoudhury.pem
```

Next you will need to create an application and add your user to this new application.

```bash
sudo chef-server-ctl org-create chefdemo "Chef Demo" --association_user pervezchoudhury --filename /home/pervezchoudhury/chef-certs/chefdemo.pem
```

## Install the management console

```bash
sudo chef-server-ctl install chef-manage
sudo chef-server-ctl reconfigure
sudo chef-manage-ctl reconfigure
```

You will now be able to log into the Chef manageent console using your username and password you created earlier.

## Install the reporting add-on

Finally you will need to install the reporting add on to give you more information about your Chef infrastucture.

```bash
sudo chef-server-ctl install opscode-reporting
sudo chef-manage-ctl reconfigure
sudo opscode-reporting-ctl reconfigure
```

[1]: https://www.ubuntu.com/download/server/install-ubuntu-server
[2]: https://www.ubuntu.com/
[3]: https://downloads.chef.io/chef-server/
[4]: https://www.gnu.org/software/wget/
[5]: https://curl.haxx.se/