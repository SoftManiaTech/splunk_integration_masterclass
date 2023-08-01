MSSQL DATABASE CREATION


1.From the sqlcmd command prompt, paste the following Transact-SQL command to create a test database

```bash 
CREATE DATABASE TestDB;
```

2.On the next line, write a query to return the name of all of the databases on your server

```bash 
SELECT Name from sys.databases;
```

```bash 
GO
```

3.From the sqlcmd command prompt, switch context to the new TestDB database

```bash 
USE TestDB;
```

```bash 
GO
```


4.Create new table named dbo.Inventory

```bash 
CREATE TABLE dbo.Inventory (id INT, name NVARCHAR(50), quantity INT, PRIMARY KEY (id));
```

```bash 
GO
```

5.Insert data into the new table

```bash 
INSERT INTO dbo.Inventory VALUES (1, 'banana', 150);
INSERT INTO dbo.Inventory VALUES (2, 'orange', 154);
INSERT INTO dbo.Inventory VALUES (3, 'Mango', 155);
INSERT INTO dbo.Inventory VALUES (4, 'guava', 156);
INSERT INTO dbo.Inventory VALUES (5, 'Mango', 152);
```

```bash 
GO
```

6.From the sqlcmd command prompt, enter a query that returns rows from the dbo.Inventory table where the quantity is greater than 152

```bash 
SELECT * FROM dbo.Inventory WHERE quantity > 152;
```

```bash 
GO
```

=====================================================================================================================================================================
MSSQL USER & PASSWORD CREATION


1.Change the configuration option 'contained database authentication' from 0 to 1

```bash 
sp_configure 'contained database authentication', 1;
```

```bash 
GO
```

2.Run the reconfigure statement to install

```bash 
RECONFIGURE;
```

```bash 
GO
```

3.Create user & password

```bash 
ALTER DATABASE TestDB SET CONTAINMENT = PARTIAL;
```

```bash 
GO
```

```bash 
USE TestDB
```

```bash 
GO
```

```bash 
CREATE USER Test123 WITH PASSWORD = 'Rahuman123!';
```

```bash 
GO
```

```bash 
GRANT SELECT ON OBJECT::dbo.Inventory TO Test123;
```

```bash   
GO
```

```bash 
EXIT
```


4.Login as root user using below command

```bash 
sudo su
```

```bash 
/opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2,1.1,1.0
```


5.Restart mssql server

```bash 
systemctl restart mssql-server.service
```



