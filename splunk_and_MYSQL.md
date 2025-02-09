mysql integration with splunk


Login as root user using the below command

```bash
sudo su
```
Open pluginconf.d folder

```bash
cd /etc/yum/pluginconf.d/
```
Edit subscription-manager.conf file

```bash
vi subscription-manager.conf
```
Inside the “subscription-manager.conf” file, change enabled to 0 and save the file

```bash
[main]
enabled=0
```
Remove all cached files from all enabled repositories at once

```bash
yum clean all
```

Install MYSQL server packages

```bash
dnf install mysql-server
```
Allow the packages

```bash
y
```
Start mysqld service

```bash
systemctl start mysqld.service
```

Enable the mysqld service to start at boot

```bash 
systemctl enable mysqld.service
```
To improve security when installing MySQL, run the following command

```bash
mysql_secure_installation
```
It will ask request to set up a new password >>Enter “y”

```bash
y
```
Set the new password with given requirements (you select Medium Length 1)

```bash
1
```
Continue with the password provider

```bash
y
```
Accept all requirements
1.Remove anonymous users?

```bash
y
```
2.Disallow root login remotely?

```bash
y 
```
3.Remove test databas and access to it?

```bash
y 
```
4.Reload privileges tables now?

```bash
y
```

































































































