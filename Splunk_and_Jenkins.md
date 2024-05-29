Download & install Jenkins


1.Ensure that your software packages are up to date on your instance by using the following command to perform a quick software update

```bash 
sudo yum update

sudo yum install wget -y
``` 

2.Add the jenkins repo

```bash 
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
```
	
3.Import a key file from Jenkins-CI to enable installation from the package

```bash 
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
```

```bash 
sudo yum upgrade
```

4.Install Java

```bash 
sudo yum install fontconfig java-17-openjdk -y
```

5.Install Jenkins

```bash 
sudo yum install jenkins -y
```

6.Enable the Jenkins service to start at boot

```bash 
sudo systemctl enable jenkins
```

7.Start Jenkins as a service

```bash 
sudo systemctl start jenkins
```

8.You can check the status of the Jenkins service using the command
```bash
sudo systemctl status jenkins
```
As prompted, enter the password found in /var/lib/jenkins/secrets/initialAdminPassword.

Use the following command to display this password

```bash 
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
