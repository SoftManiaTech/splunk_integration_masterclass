### Install Syslog-ng on Linux (RHEL-9)
Login as root user
```bash
sudo su
```

```bash
subscription-manager repos --enable codeready-builder-for-rhel-9-noarch-rpms
dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm
```
Navigate to the below mentioned directory

```bash
cd /etc/yum.repos.d/
```

Install wget (Package installer)

```bash
yum install wget
```


```bash
wget https://copr.fedorainfracloud.org/coprs/czanik/syslog-ng336/repo/epel-8/czanik-syslog-ng41-epel-8.repo
```
```bash
yum install syslog-ng --nobest
```

Enable and start Syslog

```bash
systemctl enable syslog-ng
systemctl start syslog-ng
```
Check the status of the syslog using the below command

```bash
systemctl status syslog-ng
```


### Configure Syslog-ng to send data via 5514 port to Splunk

Login as root user using below command

```bash
sudo su
```
 

Enable syslog 

```bash
systemctl enable syslog-ng
```


Go to the directory mentioned below

```bash
cd /etc/syslog-ng
```

List the files to check if syslog-ng.conf is available

```bash
ls
```

Edit the syslog-ng.conf file

```bash
vi syslog-ng.conf
```

Add the below listed lines to forward the data.
Use your splunk instance IP address & Port number

```bash
source tcp_log {
file("/var/log/secure");
};

destination splunk_tcp {
network("35.179.4.112" transport("tcp") port(5514));
};

log {
source(tcp_log);
destination(splunk_tcp);
};
```
Restart syslog-ng service

```bash
systemctl restart syslog-ng
```

Troubleshooting:

```bash
egrep -i 'syslog-ng.*' /var/log/messages
```
```bash
semanage port -l | grep 5514
```

If the 5514 port enabled, then use below command to enable the port

```bash
semanage port -a -t http_port_t -p tcp 5514
```
