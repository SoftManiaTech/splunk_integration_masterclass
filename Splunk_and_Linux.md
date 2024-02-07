## Splunk Forwarder Installation

### Connect to instance using backend SSH

### Login as Root User and update yum installer
```bash
sudo su
yum update -y
```
### Create user and group called splunk
```bash
useradd splunk
groupadd splunk
```
### Create splunkforwarder directory
```bash
mkdir /opt/splunkforwarder
ll /opt/
```
### Changing the ownership of that directory
```bash
chown -R splunk:splunk /opt/splunkforwarder/
ll /opt/
```
### Install wget package
```bash
yum install wget -y
```
### Switch to splunk user
```bash
sudo su - splunk
```
### Navigate to splunk user home directory
```bash
cd /home/splunk
```
### Download the Splunk UF
```bash
wget -O splunkforwarder-9.1.2-b6b9c8185839-Linux-x86_64.tgz "https://download.splunk.com/products/universalforwarder/releases/9.1.2/linux/splunkforwarder-9.1.2-b6b9c8185839-Linux-x86_64.tgz"
```
### Extract the tar package
```bash
tar -xvf splunkforwarder-9.1.2-b6b9c8185839-Linux-x86_64.tgz -C /opt/
```
### Accept the license & enter admin username and password:
```bash
/opt/splunkforwarder/bin/splunk start --accept-license
```

## Configure Splunk to run at boot time
### Exit from splunk user & sign in as root user
```bash
exit
sudo su
```
### Enable boot start
```bash
/opt/splunkforwarder/bin/splunk enable boot-start -user splunk
```

## Configuring Outputs.conf file:
### Switch to splunk user
```bash
sudo su - splunk
```
### Go to forwarder's local folder & configure the outputs.conf file:
```bash
cd /opt/splunkforwarder/etc/system/local
ls
```
### Create new file called outputs.conf
```bash
vi outputs.conf
```
### Paste the below content (Make sure to replace the ip_address with your indexer ip_address)
```bash
[tcpout]
defaultGroup=my_indexers

[tcpout:my_indexers]
server=35.179.4.112:9997

[tcpout-server://35.179.4.112:9997]
```
### Restarting the Splunk Universal Forwarder
```bash
cd /opt/splunkforwarder/bin
./splunk restart
```
## Download the splunk add on for unix and linux from splunkbase
## Install & Configuration of Splunk Add on:
### Copy the tar file to linux instance:
If you are using Windows OS for downloading Splunk, open your command prompt as a administrator and navigate to Downloads folder:

For example
```bash
cd C:\Users\Ramany\Downloads\
```

```bash
scp -i "london_ramany.pem" splunk-add-on-for-unix-and-linux_900.tgz ec2-user@ec2-18-171-221-122.eu-west-2.compute.amazonaws.com:/tmp
```
### Connect to instance using SSH client

### Login as Root User
```bash
sudo su
```
### Check for the file in tmp folder
```bash
cd /tmp
ls
```
### Change the ownership of the add-on package
```bash
chown -R splunk:splunk splunk-add-on-for-unix-and-linux_900.tgz
```
### Login as a Splunk user
```bash
sudo su - splunk
```
### Check for the file in tmp folder
```bash
cd /tmp
ls
```
### Extract the tar package within splunk universal forwarder apps folder
```bash
tar -xvf splunk-add-on-for-unix-and-linux_900.tgz -C /opt/splunkforwarder/etc/apps/
```
### Go to the apps folder and check if the add on folder is available 
```bash
cd /opt/splunkforwarder/etc/apps/
ls
```
### Go to add on's default folder and check for inputs.conf file
```bash
cd Splunk_TA_nix
cd default
ls
```
### Open inputs.conf file in read mode:
```bash
cat inputs.conf
```
### Copy the entire file content and paste in the notepad and make the below changes:
```bash
disabled=true to disabled=false
disabled=1 to disabled=0
```
### Move back to add-on folder
```bash
cd ..
```
### Create local folder within add-on folder 
```bash
mkdir local
cd local
```
### Create inputs.conf file in local folder and copy the contents of inputs.conf from default folder.
```bash
vi inputs.conf
```
### Now, Restart the splunk universal forwarder
```bash
cd /opt/splunkforwarder/bin
./splunk restart
```



