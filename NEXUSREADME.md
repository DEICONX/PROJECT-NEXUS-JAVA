# AWS BUILD SERVER CREATION

### LAUNCH EC2

create a instance by giving instance name

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDSERVER\01.png)

----

select ubuntu image and make sure it is latest version i.e 24.04 LTS (HVM)

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDSERVER\02.png)

------

click on edit network settings and change security group name(optional) and launch instance

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDSERVER\03.png)

-----

connect to the instance

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDSERVER\04.png)

-----

copy the SSH key and open terminal

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDSERVER\05.png)

------

In terminal change directory to downloads(your PEM file is present in downloads) use the below command: `cd downloads` and press enter paste the SSH key and press enter now it will ask permission yes/no type yes

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDSERVER\06.png)

-----

Now you are connected to BUILD server image(ubuntu)

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDSERVER\07.png)

------

# JAVA BUILD-MAVEN VERSION 0.0.1

> we have full java code which is cloned from github using `git clone <URL>` now iam changing it to version 0.0.1 that has only addition feature 
>
> `cd src/main/webapp/`
>
> `sudo vi index.jsp`

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDV1\Screenshot 2025-10-15 151336.png)

------

> remove that highlighted part shown in below image

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDV1\Screenshot 2025-10-15 151356.png)

------

> after removing save the file and now this code becomes suitable to perform only addition function

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDV1\Screenshot 2025-10-15 151450.png)

------

> Now modify the pom.xml file i.e by changing the highlighted part version and artifact id name

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDV1\Screenshot 2025-10-15 151549.png)

-----

> Now the version is changed to 0.0.1 and also artifact id to webapp-add
>
> save it

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDV1\Screenshot 2025-10-15 151623.png)

----

> Now set up your environment to perform build
>
> update and install java first and also install maven `sudo apt install maven`
>
> validate using `mvn validate` and build using `mvn package`

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDV1\Screenshot 2025-10-15 151705.png)

-------

> after build you will now get a .war file of first version

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDV1\Screenshot 2025-10-15 151733.png)

----

# AWS DEPLOY SERVER CREATION AND CONFIGURATION

#### LAUNCH EC2

create an instance by giving instance name

![](C:\Users\jagan\Downloads\NEXUS\NEXUSDEPLOYSERVER\01.png)

------

select image ubuntu latest version same as BUILD server and launch the server

![](C:\Users\jagan\Downloads\NEXUS\NEXUSDEPLOYSERVER\02.png)

------

configure inbound rules go to security and u will find inbound and outbound rules

![](C:\Users\jagan\Downloads\NEXUS\NEXUSDEPLOYSERVER\03.png)

-----

select edit inbound rules to add port number of TOMCAT WEB Server

![](C:\Users\jagan\Downloads\NEXUS\NEXUSDEPLOYSERVER\04.png)

----

Add port number 8080

Type: custom TCP ; Port range: 8080 ; Source: Anywhere IPV4

![](C:\Users\jagan\Downloads\NEXUS\NEXUSDEPLOYSERVER\05.png)

------

After adding inbound rule click save rules and it will show successfully modified

![](C:\Users\jagan\Downloads\NEXUS\NEXUSDEPLOYSERVER\06.png)

-----

copy the SSH key and open Terminal

![](C:\Users\jagan\Downloads\NEXUS\NEXUSDEPLOYSERVER\07.png)

-----

Use `cd downloads` to get into PEM file location which is saved in downloads

Now paste the SSH key and enter yes you will be connected to DEPLOY server

![](C:\Users\jagan\Downloads\NEXUS\NEXUSDEPLOYSERVER\08.png)

-----

# NEXUS TOOL SETUP

> similar to our DEPLOY server launch instance but add port number 8081 as nexus runs on port number 8081
>
> Download java (nexus needs java)

![](C:\Users\jagan\Downloads\NEXUS\NEXUSSETUP\Screenshot 2025-10-15 172820.png)

----

> download nexus from browser by copying link address

![](C:\Users\jagan\Downloads\NEXUS\NEXUSSETUP\Screenshot 2025-10-15 173017.png)

----

> copy the link address of linux as we are now using ubuntu

![](C:\Users\jagan\Downloads\NEXUS\NEXUSSETUP\Screenshot 2025-10-15 173037.png)

----

> Download using `wget <link address>` 
>
> `ls` you can see the tar file

![](C:\Users\jagan\Downloads\NEXUS\NEXUSSETUP\Screenshot 2025-10-15 173111.png)

------

> extract the file using `tar -xvf <zip file name>`

![](C:\Users\jagan\Downloads\NEXUS\NEXUSSETUP\Screenshot 2025-10-15 173140.png)

------

> after extracting cd `nexus-3.85.0-03` and `ls`
>
> you will see a executable nexus file
>
> run that executable file

![](C:\Users\jagan\Downloads\NEXUS\NEXUSSETUP\Screenshot 2025-10-15 173400.png)

-----

> it will execute and show usage 
>
> now start nexus using `./nexus start`

![](C:\Users\jagan\Downloads\NEXUS\NEXUSSETUP\Screenshot 2025-10-15 173528.png)

----

> you can see the status of nexus whether it started or not by using `netstat -ntpl` (highlighted part in image shows port number of nexus)

![](C:\Users\jagan\Downloads\NEXUS\NEXUSSETUP\Screenshot 2025-10-15 173625.png)

-----

> now copy the public ip of nexus server 

![](C:\Users\jagan\Downloads\NEXUS\NEXUSSETUP\Screenshot 2025-10-15 173703.png)

------

> New tab and paste the public ip along with port number of nexus i.e `54.92.192.98:8081`

![](C:\Users\jagan\Downloads\NEXUS\NEXUSSETUP\Screenshot 2025-10-15 173736.png)

------

> now the nexus tool is successfully installed and its running 

![](C:\Users\jagan\Downloads\NEXUS\NEXUSSETUP\Screenshot 2025-10-15 173822.png)

-----

> login and default username is admin
>
> configure password (copy the path )
>
> While installing and starting nexus it creates a default password and also it gives the path where the password is stored

![](C:\Users\jagan\Downloads\NEXUS\NEXUSSETUP\Screenshot 2025-10-15 173850.png)

-----

> now to read the password 
>
> `sudo cat <path>`

![](C:\Users\jagan\Downloads\NEXUS\NEXUSSETUP\Screenshot 2025-10-15 173937.png)

-----

> it will ask you to set up a password give any and click next

![](C:\Users\jagan\Downloads\NEXUS\NEXUSSETUP\Screenshot 2025-10-15 174016.png)

-----

> disable anonymous access

![](C:\Users\jagan\Downloads\NEXUS\NEXUSSETUP\Screenshot 2025-10-15 174054.png)

----

> You can see all the default repos created by nexus in browse

![](C:\Users\jagan\Downloads\NEXUS\NEXUSSETUP\Screenshot 2025-10-15 174113.png)

----

> create your own repo 
>
> go to system status 

![](C:\Users\jagan\Downloads\NEXUS\NEXUSSETUP\Screenshot 2025-10-15 174127.png)

-----

> click on repositories and you will see create a repository 

![](C:\Users\jagan\Downloads\NEXUS\NEXUSSETUP\Screenshot 2025-10-15 174143.png)

----

> by using that create a repository it will ask you to select the recipe type select maven(hosted)

![](C:\Users\jagan\Downloads\NEXUS\NEXUSSETUP\Screenshot 2025-10-15 174201.png)

-----

> Give a name to your repo and click on create

![](C:\Users\jagan\Downloads\NEXUS\NEXUSSETUP\Screenshot 2025-10-15 174219.png)

-----

> after creating you can see you repo in browse

![](C:\Users\jagan\Downloads\NEXUS\NEXUSSETUP\Screenshot 2025-10-15 174238.png)

-------

# DEPLOYMENT-TOMCAT WEB SERVER SETUP

Update the server using `sudo apt -y update`

Install JAVA latest version by using `sudo apt install openjdk-17-jre-headless -y`

![](C:\Users\jagan\Downloads\NEXUS\NEXUSDEPLOY\Screenshot 2025-10-07 125258.png)

-----

Browse apache tomcat install and open the website

copy the address(URL Link) of tar.gz(pgp,sha512) file

![](C:\Users\jagan\Downloads\NEXUS\NEXUSDEPLOY\Screenshot 2025-10-07 125403.png)

-----

Use `wget <tar.gz link address>` to download the folder

By using `ls` u can find downloaded folder

![](C:\Users\jagan\Downloads\NEXUS\NEXUSDEPLOY\Screenshot 2025-10-07 125433.png)

------

to extract the folder use `tar -xvf apache-tomcat-9.0.110.tar.gz`

![](C:\Users\jagan\Downloads\NEXUS\NEXUSDEPLOY\Screenshot 2025-10-07 125500.png)

------

Now change directory to bin folder `cd bin`

Start TOMCAT server using `./startup.sh` 

![](C:\Users\jagan\Downloads\NEXUS\NEXUSDEPLOY\Screenshot 2025-10-07 125927.png)

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

![](C:\Users\jagan\Downloads\NEXUS\NEXUSDEPLOY\Screenshot 2025-10-07 135146.png)

----

configure the webapps

change directory to `cd webapps/manager/META-INF` and `ls` to list the file to be configured

open editor `vi <file name>` here in below image it is `vi context.xml`

here remove the valve file

![](C:\Users\jagan\Downloads\NEXUS\NEXUSDEPLOY\Screenshot 2025-10-07 135427.png)

open the browser by cpoying pubic ip of deploy server and paste it followed by port number i.e :8080 it will ask username and password

Enter the valid username and password while u have given in adding users

signin

![](C:\Users\jagan\Downloads\NEXUS\NEXUSDEPLOY\Screenshot 2025-10-07 135529.png)

-----

Now after configuration you can access manager in web server

here you will see all the files present in webapps

![](C:\Users\jagan\Downloads\NEXUS\NEXUSDEPLOY\05.png)

-----

# COPYING .WAR TO NEXUS REPO

> CONFIGURE pom.xml `vi pom.xml`

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDMODIFY\Screenshot 2025-10-15 174455.png)

----

> The highlighted part in image describes about nexus tool 
>
> <id> is your nexus repo name 
>
> URL is the nexus repo URL

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDMODIFY\Screenshot 2025-10-15 174518.png)

------

> change it with your repo URL and name

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDMODIFY\Screenshot 2025-10-15 174604.png)

-----

> configure maven 
>
> `cd /etc/maven` and `sudo vi settings.xml`

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDMODIFY\Screenshot 2025-10-15 174905.png)

------

> Now uncomment it and giive your username and password

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDMODIFY\Screenshot 2025-10-15 174947.png)

-----

> After uncommenting it and giving username password you can see in below image

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDMODIFY\Screenshot 2025-10-15 175055.png)

-----

> now clean `mvn clean` build `mvn build` and deploy to nexus tool repo using `mvn deploy`

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDMODIFY\Screenshot 2025-10-15 175423.png)

-----

> now in your nexus tab you can see the version 0.0.1 .war

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDMODIFY\Screenshot 2025-10-15 180519.png)

----

> Copy the URL to move .war file to /webapps in deploy server 

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDMODIFY\Screenshot 2025-10-15 180535.png)

------

> For this `cd /webapps` and `wget <URL>` in that URL you need to give username:password@ of nexus after http://
>
> now your version 0.0.1 .war is copied into webapps folder 

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDMODIFY\Screenshot 2025-10-15 180656.png)

-----

> you can view our version 0.0.1 in deploy server i.e Tomcat website

![](C:\Users\jagan\Downloads\NEXUS\NEXUSDEPLOY\06.png)

------

> test the output 

![](C:\Users\jagan\Downloads\NEXUS\NEXUSDEPLOY\07.png)

---

> Similarly follow the above steps when version 0.0.2 comes deploy it to nexus rebuild again`mvn deploy` 

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDMODIFY\Screenshot 2025-10-15 181426.png)

----

> copy the path URL
>
> For this `cd /webapps` and `wget <URL>` in that URL you need to give username:password@ of nexus after http://
>
> now your version 0.0.2 .war is copied into webapps folder 

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDMODIFY\Screenshot 2025-10-15 181716.png)

-----

> version 0.0.2 is deployed

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDMODIFY\Screenshot 2025-10-15 181732.png)

----

> test the output

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDMODIFY\Screenshot 2025-10-15 181740.png)

-----

> Follow the above steps and do the same when version 0.0.3 comes

> copy the path URL

> For this `cd /webapps` and `wget <URL>` in that URL you need to give username:password@ of nexus after http://

> now your version 0.0.2 .war is copied into webapps folder

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDMODIFY\Screenshot 2025-10-15 181716.png)

----

> version 0.0.3 is deployed

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDMODIFY\Screenshot 2025-10-15 182214.png)

----

> test the output

![](C:\Users\jagan\Downloads\NEXUS\NEXUSBUILDMODIFY\Screenshot 2025-10-15 182222.png)

