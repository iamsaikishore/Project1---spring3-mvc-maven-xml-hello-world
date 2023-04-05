Maven - Spring 3 MVC Hello World
===============================
Template for Spring 3 MVC + JSP view + XML configuration, using Maven build tool.

###1. Technologies used
* Maven 3
* Spring 3.2.13.RELEASE
* JSTL 1.2
* Logback 1.1.3
* Boostrap 3

###2. To Run this project locally
```shell
$ git clone https://github.com/mkyong/spring3-mvc-maven-xml-hello-world (for original project) or $ git clone https://github.com/iamsaikishore/Project1-spring3-mvc-maven-xml-hello-world.git
$ mvn jetty:run
```
Access ```http://localhost:8080/spring3```

###3. To import this project into Eclipse IDE
1. ```$ mvn eclipse:eclipse```
2. Import into Eclipse via **existing projects into workspace** option.
3. Done.

###4. Project Demo
Please refer to this article [Maven - Spring 3 MVC Hello World ](http://www.mkyong.com/spring3/spring-3-mvc-hello-world-example/)
maven file.



Project1 - spring3-mvc-maven-xml-hello-world
======================================
**Prerequisites:**  Git, Maven, Jenkins, Tomcat

First launch a Linux server, for this project am using AWS EC2 instance and make sure to open port 8080 (for Jenkins) and port 8282 (for tomcat, by default tomcat runs on port 8080 but we are using it for Jenkins) in security group.

**Configuring Tomcat:**
```shell
$ sudo -i
Create a directory
$ mkdir /opt/tomcat
Download apache tomcat 
$ wget https://dlcdn.apache.org/tomcat/tomcat-8/v8.5.87/bin/apache-tomcat-8.5.87.tar.gz
$ tar xvzf apache-tomcat-8.5.87.tar.gz
$ cd apache-tomcat-8.5.87
```
The typical directory hierarchy of a Tomcat installation consists of the following:

*	**bin** - startup, shutdown and other scripts and executables
*	**Common** - common classes that Catalina and web applications can use
*	**conf** - XML files and related DTDs to configure Tomcat(server.xml, tomcat-users.xml)
*	**logs** - Catalina and application logs
*	**server** - classes used only by Catalina
*	**shared** - classes shared by all web applications
*	**webapps** - directory containing the web applications
*	**work** - temporary storage for files and directories
Open server.xml file and change the tomcat port from 8080 to 8282
```shell
$ vim /opt/tomcat/apache-tomcat-8.5.87/conf/server.xml
<Connector port="8282" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />
```
To access the tomcat GUI, we have to create user with gui roles
```shell
$ vim /opt/tomcat/apache-tomcat-8.5.87/conf/tomcat-users.xml
  <role rolename="admin-gui"/>
  <role rolename="admin-script"/>
  <role rolename="manager-gui"/>
  <role rolename="manager-script"/>
  <user username="tomcat" password="tomcat" roles="admin-gui,admin-script,manager-gui,manager-script"/>
```
Now to start the Tomcat server go to /opt/tomcat/apache-tomcat-8.5.87/bin and run the startup.sh script.
```shell
$ cd /opt/tomcat/apache-tomcat-8.5.87/bin
$ ./startup.sh
```
Now in the browser, search with ip address of the instance and port number ```(ex: 10.0.0.1:8282)```
![tomcat1](https://user-images.githubusercontent.com/129657174/229402560-939dd0f6-2aac-4636-a09b-22f0ed6c90ee.png)
 
Click on Manager App and give the credentials we have configured in tomcat-users.xml (username=tomcat password=tomcat)
![tomcat2](https://user-images.githubusercontent.com/129657174/229402573-ff0ce1c6-8bb0-4e06-b844-066275495c48.png)
 
You have configured Tomcat successfully.

Configuring Jenkins:
```shell
$ wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo
$ rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
$ yum upgrade -y
# Add required dependencies for the jenkins package
$ yum install java-11-openjdk -y
$ yum install Jenkins -y
$ systemctl start Jenkins.service
```


Now in the browser, search with ip address of the instance and port number ```(ex: 10.0.0.1:8080)```
```shell
$ cat /var/lib/jenkins/secrets/initialAdminPassword
```
Copy the password in Jenkins, install the plugins and create a user.

Required plugins for this project: Maven integration, Deploy to container.

Go to Manage Jenkins --> Manage Plugins click on Available and search for the plugins and install them.

Now Configure Maven for that go to Manage Jenkins --> Global Tool Configuration and edit as below
![maven1](https://user-images.githubusercontent.com/129657174/229402586-7af64b24-063e-4b7e-b80f-51e262344f55.png)
 
Now create a freestyle job and configure as below
![jenkins1](https://user-images.githubusercontent.com/129657174/229402590-62648b56-a53c-42b5-8cf0-cf7c97e69e14.png)
![jenkins2](https://user-images.githubusercontent.com/129657174/229402595-1521999d-7483-4d25-8034-33380d7269e9.png)
![jenkins3](https://user-images.githubusercontent.com/129657174/229402596-4b1bf7c9-79e8-49ad-a119-900613d83777.png)
   
Add the Tomcat credentials(username and password) and click on Save.

Now click Build Now to build the project.

Now go to tomcat server and you should see /kishq
![app1](https://user-images.githubusercontent.com/129657174/229402598-92933ab3-6165-46c9-affd-eec0a827fe24.png)
 
Now click on /kishq
![app2](https://user-images.githubusercontent.com/129657174/229402604-18f1ca80-91ed-4a6e-b401-d40362f69907.png)
 
Yeah! Our application was deploy successfully to Tomcat server.

### Hope you all are enjoyed.

For the original Project Details click the below links.

[GitHub Repo](https://github.com/jmstechhome8/spring3-mvc-maven-xml-hello-world)

[Youtube](https://www.youtube.com/watch?v=4TRfvlU7W90&list=PLVnWcdGotHcapVIbp1dCUkT4fifxUz5kN&index=4&t=2468s)

Please refer to this article [Maven - Spring 3 MVC Hello World ](http://www.mkyong.com/spring3/spring-3-mvc-hello-world-example/)


