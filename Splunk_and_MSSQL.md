MSSQL Integration with splunk

1.Login as root user using below command

```bash
sudo su
```

2.Check the MSSQL status

```bash 
systemctl status mssql-server
```

3.Stop the MSSQL server

```bash 
systemctl stop mssql-server
```

4.To make sqlcmd and bcp accessible from the bash shell for login sessions, modify your PATH in the ~/.bash_profile file with the following command:

```bash 
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
```

```bash 
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
```

```bash 
source ~/.bashrc
```

5.Set the sa (system administrator) Password [Enter & Confirm sa password]

```bash 
/opt/mssql/bin/mssql-conf set-sa-password
```

6.Start MSSQL server

```bash 
systemctl start mssql-server
```

7.Check MSSQL status

```bash 
systemctl status mssql-server
```

8.Use sqlcmd to locally connect to your new SQL Server instance.

```bash
exit
sqlcmd -S localhost -U sa -P YOUR_PASSWORD -C
```
