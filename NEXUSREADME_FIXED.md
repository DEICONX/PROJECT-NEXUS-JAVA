# AWS BUILD SERVER CREATION

### LAUNCH EC2

create a instance by giving instance name

![](./NEXUSBUILDSERVER/01.png)

----

select ubuntu image and make sure it is latest version i.e 24.04 LTS (HVM)

![](./NEXUSBUILDSERVER/02.png)

------

click on edit network settings and change security group name(optional) and launch instance

![](./NEXUSBUILDSERVER/03.png)

-----

connect to the instance

![](./NEXUSBUILDSERVER/04.png)

-----

copy the SSH key and open terminal

![](./NEXUSBUILDSERVER/05.png)

------

In terminal change directory to downloads(your PEM file is present in downloads) use the below command: `cd downloads` and press enter paste the SSH key and press enter now it will ask permission yes/no type yes

![](./NEXUSBUILDSERVER/06.png)

-----

Now you are connected to BUILD server image(ubuntu)

![](./NEXUSBUILDSERVER/07.png)

------

# JAVA BUILD-MAVEN VERSION 0.0.1

> we have full java code which is cloned from github using `git clone <URL>` now iam changing it to version 0.0.1 that has only addition feature 
>
> `cd src/main/webapp/`
>
> `sudo vi index.jsp`

![](./NEXUSBUILDV1/Screenshot%202025-10-15%20151336.png)

------

> remove that highlighted part shown in below image

![](./NEXUSBUILDV1/Screenshot%202025-10-15%20151356.png)

------

> after removing save the file and now this code becomes suitable to perform only addition function

![](./NEXUSBUILDV1/Screenshot%202025-10-15%20151450.png)

------

> Now modify the pom.xml file i.e by changing the highlighted part version and artifact id name

![](./NEXUSBUILDV1/Screenshot%202025-10-15%20151549.png)

-----

> Now the version is changed to 0.0.1 and also artifact id to webapp-add
>
> save it

![](./NEXUSBUILDV1/Screenshot%202025-10-15%20151623.png)

----

> Now set up your environment to perform build
>
> update and install java first and also install maven `sudo apt install maven`
>
> validate using `mvn validate` and build using `mvn package`

![](./NEXUSBUILDV1/Screenshot%202025-10-15%20151705.png)

-------

> after build you will now get a .war file of first version

![](./NEXUSBUILDV1/Screenshot%202025-10-15%20151733.png)

----

# AWS DEPLOY SERVER CREATION AND CONFIGURATION

#### LAUNCH EC2

create an instance by giving instance name

![](./NEXUSDEPLOYSERVER/01.png)

------

select image ubuntu latest version same as BUILD server and launch the server

![](./NEXUSDEPLOYSERVER/02.png)

------

configure inbound rules go to security and u will find inbound and outbound rules

![](./NEXUSDEPLOYSERVER/03.png)

-----

select edit inbound rules to add port number of TOMCAT WEB Server

![](./NEXUSDEPLOYSERVER/04.png)

----

Add port number 8080

Type: custom TCP ; Port range: 8080 ; Source: Anywhere IPV4

![](./NEXUSDEPLOYSERVER/05.png)

------

After adding inbound rule click save rules and it will show successfully modified

![](./NEXUSDEPLOYSERVER/06.png)

-----

copy the SSH key and open Terminal

![](./NEXUSDEPLOYSERVER/07.png)

-----

Use `cd downloads` to get into PEM file location which is saved in downloads

Now paste the SSH key and enter yes you will be connected to DEPLOY server

![](./NEXUSDEPLOYSERVER/08.png)

-----

# NEXUS TOOL SETUP

> similar to our DEPLOY server launch instance but add port number 8081 as nexus runs on port number 8081
>
> Download java (nexus needs java)

![](./NEXUSSETUP/Screenshot%202025-10-15%20172820.png)

----

> download nexus from browser by copying link address

![](./NEXUSSETUP/Screenshot%202025-10-15%20173017.png)

----

> copy the link address of linux as we are now using ubuntu

![](./NEXUSSETUP/Screenshot%202025-10-15%20173037.png)

----

> Download using `wget <link address>` 
>
> `ls` you can see the tar file

![](./NEXUSSETUP/Screenshot%202025-10-15%20173111.png)

------

> extract the file using `tar -xvf <zip file name>`

![](./NEXUSSETUP/Screenshot%202025-10-15%20173140.png)

------

> after extracting cd `nexus-3.85.0-03` and `ls`
>
> you will see a executable nexus file
>
> run that executable file

![](./NEXUSSETUP/Screenshot%202025-10-15%20173400.png)

-----

> it will execute and show usage 
>
> now start nexus using `./nexus start`

![](./NEXUSSETUP/Screenshot%202025-10-15%20173528.png)

----

> you can see the status of nexus whether it started or not by using `netstat -ntpl` (highlighted part in image shows port number of nexus)

![](./NEXUSSETUP/Screenshot%202025-10-15%20173625.png)

-----

> now copy the public ip of nexus server 

![](./NEXUSSETUP/Screenshot%202025-10-15%20173703.png)

------

> New tab and paste the public ip along with port number of nexus i.e `54.92.192.98:8081`

![](./NEXUSSETUP/Screenshot%202025-10-15%20173736.png)

------

> now the nexus tool is successfully installed and its running 

![](./NEXUSSETUP/Screenshot%202025-10-15%20173822.png)

-----

> login and default username is admin
>
> configure password (copy the path )
>
> While installing and starting nexus it creates a default password and also it gives the path where the password is stored

![](./NEXUSSETUP/Screenshot%202025-10-15%20173850.png)

-----

> now to read the password 
>
> `sudo cat <path>`

![](./NEXUSSETUP/Screenshot%202025-10-15%20173937.png)

-----

> it will ask you to set up a password give any and click next

![](./NEXUSSETUP/Screenshot%202025-10-15%20174016.png)

-----

> disable anonymous access

![](./NEXUSSETUP/Screenshot%202025-10-15%20174054.png)

----

> You can see all the default repos created by nexus in browse

![](./NEXUSSETUP/Screenshot%202025-10-15%20174113.png)

----

> create your own repo 
>
> go to system status 

![](./NEXUSSETUP/Screenshot%202025-10-15%20174127.png)

-----

> click on repositories and you will see create a repository 

![](./NEXUSSETUP/Screenshot%202025-10-15%20174143.png)

----

> by using that create a repository it will ask you to select the recipe type select maven(hosted)

![](./NEXUSSETUP/Screenshot%202025-10-15%20174201.png)

-----

> Give a name to your repo and click on create

![](./NEXUSSETUP/Screenshot%202025-10-15%20174219.png)

-----

> after creating you can see you repo in browse

![](./NEXUSSETUP/Screenshot%202025-10-15%20174238.png)

-------

# DEPLOYMENT-TOMCAT WEB SERVER SETUP

Update the server using `sudo apt -y update`

Install JAVA latest version by using `sudo apt install openjdk-17-jre-headless -y`

![](./NEXUSDEPLOY/Screenshot%202025-10-07%20125258.png)

-----

Browse apache tomcat install and open the website

copy the address(URL Link) of tar.gz(pgp,sha512) file

![](./NEXUSDEPLOY/Screenshot%202025-10-07%20125403.png)

-----

Use `wget <tar.gz link address>` to download the folder

By using `ls` u can find downloaded folder

![](./NEXUSDEPLOY/Screenshot%202025-10-07%20125433.png)

------

to extract the folder use `tar -xvf apache-tomcat-9.0.110.tar.gz`

![](./NEXUSDEPLOY/Screenshot%202025-10-07%20125500.png)

------

Now change directory to bin folder `cd bin`

Start TOMCAT server using `./startup.sh` 

![](./NEXUSDEPLOY/Screenshot%202025-10-07%20125927.png)

------

First add a user for WEB server to do that

`ls` lists all the files/folders

change directory to `cd conf/` and `ls` to see all the files/folders present inside it

open file using `vi <file name>` here in the below image it is `vi tomcat-users.xml`

Add User at bottom above

```
<role rolename="manager-gui"/>
<role rolename="manager-script"/>
<user username="admin" password="admin123" roles="manager-gui,manager-script"/>
```

username and password can be anything depending upon user and save it using `:wq`

![](./NEXUSDEPLOY/Screenshot%202025-10-07%20135146.png)

----

configure the webapps

change directory to `cd webapps/manager/META-INF` and `ls` to list the file to be configured

open editor `vi <file name>` here in below image it is `vi context.xml`

here remove the valve file

![](./NEXUSDEPLOY/Screenshot%202025-10-07%20135427.png)

open the browser by cpoying pubic ip of deploy server and paste it followed by port number i.e :8080 it will ask username and password

Enter the valid username and password while u have given in adding users

signin

![](./NEXUSDEPLOY/Screenshot%202025-10-07%20135529.png)

-----

Now after configuration you can access manager in web server

here you will see all the files present in webapps

![](./NEXUSDEPLOY/05.png)

-----

# COPYING .WAR TO NEXUS REPO

> CONFIGURE pom.xml `vi pom.xml`

![](./NEXUSBUILDMODIFY/Screenshot%202025-10-15%20174455.png)

----

> The highlighted part in image describes about nexus tool 
>
> <id> is your nexus repo name 
>
> URL is the nexus repo URL

![](./NEXUSBUILDMODIFY/Screenshot%202025-10-15%20174518.png)

------

> change it with your repo URL and name

![](./NEXUSBUILDMODIFY/Screenshot%202025-10-15%20174604.png)

-----

> configure maven 
>
> `cd /etc/maven` and `sudo vi settings.xml`

![](./NEXUSBUILDMODIFY/Screenshot%202025-10-15%20174905.png)

------

> Now uncomment it and giive your username and password

![](./NEXUSBUILDMODIFY/Screenshot%202025-10-15%20174947.png)

-----

> After uncommenting it and giving username password you can see in below image

![](./NEXUSBUILDMODIFY/Screenshot%202025-10-15%20175055.png)

-----

> now clean `mvn clean` build `mvn build` and deploy to nexus tool repo using `mvn deploy`

![](./NEXUSBUILDMODIFY/Screenshot%202025-10-15%20175423.png)

-----

> now in your nexus tab you can see the version 0.0.1 .war

![](./NEXUSBUILDMODIFY/Screenshot%202025-10-15%20180519.png)

----

> Copy the URL to move .war file to /webapps in deploy server 

![](./NEXUSBUILDMODIFY/Screenshot%202025-10-15%20180535.png)

------

> For this `cd /webapps` and `wget <URL>` in that URL you need to give username:password@ of nexus after http://
>
> now your version 0.0.1 .war is copied into webapps folder 

![](./NEXUSBUILDMODIFY/Screenshot%202025-10-15%20180656.png)

-----

> you can view our version 0.0.1 in deploy server i.e Tomcat website

![](./NEXUSDEPLOY/06.png)

------

> test the output 

![](./NEXUSDEPLOY/07.png)

---

> Similarly follow the above steps when version 0.0.2 comes deploy it to nexus rebuild again`mvn deploy` 

![](./NEXUSBUILDMODIFY/Screenshot%202025-10-15%20181426.png)

----

> copy the path URL
>
> For this `cd /webapps` and `wget <URL>` in that URL you need to give username:password@ of nexus after http://
>
> now your version 0.0.2 .war is copied into webapps folder 

![](./NEXUSBUILDMODIFY/Screenshot%202025-10-15%20181716.png)

-----

> version 0.0.2 is deployed

![](./NEXUSBUILDMODIFY/Screenshot%202025-10-15%20181732.png)

----

> test the output

![](./NEXUSBUILDMODIFY/Screenshot%202025-10-15%20181740.png)

-----

> Follow the above steps and do the same when version 0.0.3 comes

> copy the path URL

> For this `cd /webapps` and `wget <URL>` in that URL you need to give username:password@ of nexus after http://

> now your version 0.0.2 .war is copied into webapps folder

![](./NEXUSBUILDMODIFY/Screenshot%202025-10-15%20181716.png)

----

> version 0.0.3 is deployed

![](./NEXUSBUILDMODIFY/Screenshot%202025-10-15%20182214.png)

----

> test the output

![](./NEXUSBUILDMODIFY/Screenshot%202025-10-15%20182222.png)

