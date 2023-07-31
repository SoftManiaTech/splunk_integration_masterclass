Login as root user using below command

```bash
sudo su
```
 

enable syslog 

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

Edit the syslog-ng.conf

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
network("15.152.197.52" transport("tcp") port(5514));
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
