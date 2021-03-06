---
version: 2
category: user
layout: page
title: Installation on Fedora
---
# How to install Seccubus on Fedora?

[Click here for other operating systems](../11-installation)

## From the package cloud repo

For the repo that is synced with current releases run

```bash
curl -s https://packagecloud.io/install/repositories/seccubus/releases/script.rpm.sh | sudo bash
```

For the repo that is synced with the latest code pushes to master run

```bash
curl -s https://packagecloud.io/install/repositories/seccubus/latest/script.rpm.sh | sudo bash
```

Once the repo is set up you can install Seccubus via the regular dnf command

```bash
dnf install seccubus
```

If you get an error about the package not being trusted, then please run `apt-get install gpg` before you run the script from packagecloud.io

## Dowloaded from Github

Install the rpm

```bash
wget https://github.com/schubergphilis/Seccubus/releases/download/2.32/Seccubus-2.x.x-x.noarch.rpm
sudo dnf install Seccubus-2.x.x-x.noarch.rpm
```

Update the configuration file in /etc/seccubus/config.xml 

Now create the database and populate the database with the following
commands:

```bash
sudo systemctl start mariadb # If mariadb isn't running
mysql << EOF
create database seccubus;
grant all privileges on seccubus.* to seccubus@localhost identified by 'seccubus';
flush privileges;
EOF

mysql -u seccubus -pseccubus seccubus < /opt/seccubus/var/structure_vX.mysql 
                # Use version and path indicated on the screen
mysql -u seccubus -pseccubus seccubus < /opt/seccubus/var/data_vX.mysql 
                # Use version and path indicated on the screen
```

Replace X with the database version that you need. 

## Restart the service

```bash
sysctl restart seccubus.service
```
