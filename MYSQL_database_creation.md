Create a MySQL Database (Let’s create a movies database)

1. Create a database using the CREATE statement:

```bash
CREATE DATABASE movies;
```

2. Next, verify that the database was created by showing a list of all databases. Use the SHOW statement:

```bash
SHOW DATABASES;
```

3. Select the database to make changes to it by using the USE statement:

```bash
USE movies;
```


4. Create a table using the CREATE command. Using the information from our movies example, the command is:

```bash
CREATE TABLE movies(title VARCHAR(50) NOT NULL,genre VARCHAR(30) NOT NULL,director VARCHAR(60) NOT NULL,release_year INT NOT NULL,PRIMARY KEY(title));
```

5. Verify that the table is created using the DESCRIBE command:

```bash
DESCRIBE movies;
```

6. Insert movie information in column order – title, genre, director, and release year. Use the INSERT command:

```bash
INSERT INTO movies VALUE ("Joker", "psychological thriller", "Todd Phillips", 2019);
```

7. Repeat the previous step with the second movie. Use the SELECT command to display the table:

```bash
SELECT * FROM movies;
```
