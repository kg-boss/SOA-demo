# Setting-Up an SOA environment

## Requirements

+ Java JDK 17 or higher. *The latest JDK is recommanded (JDK 19 by the time this file was created)*
+ Java JDK 8
+ GlassFish 5
+ SoapUI

> If the requirements are not installed please download them before continuing.

## 1. Installing Eclipse
You can download the `latest` version of ***Eclipse IDE*** by following the [link](https://www.eclipse.org/downloads/) below
```URL
https://www.eclipse.org/downloads/
```
1. find `Get Eclipse IDE 2022‑09`. *The latest version is recommanded (Eclipse IDE 2022‑09 by the time this file was created)*
2. click on `Download x86_64`
3. after redirecting click on `Download`

*After waiting for executable to download*

4. run the downloaded `.exe` file

*Eclipse Installer will ask for IDE type*

5. Select `Eclipse IDE for Java and Web Developers` option

![Screenshot demo](Screenshots/Demo/Eclipse%20IDE%20type%20selection.png "Eclipse IDE type selection - Screenshot demo")

6. Select your Java and installation folder paths
7. Accept Licence and wait for installation to finish

## 2. Setting-Up GlassFish

Now as Eclipse IDE is installed we can configure glassfish server

1. launch `Eclipse IDE`
2. open `Install New Software`
    1. go to `help`
    2. select `Install New Software`
3. In the `Work with` field place the following link
```
http://download.oracle.com/otn_software/oepe/12.2.1.8/oxygen/repository/dependencies/
```
4. find and select `Eclipse GlassFish Tools` plugin

![Screenshot demo](Screenshots/Demo/Eclipse%20Marketplace%20-%20glassfish.png "Install GlassFish Tools plugin - Screenshot demo")

5. click `next`, follow the process and wait for download to finish
6. Restart Eclipse IDE

*If the Servers view is not opened, try to open it first. Click `Windows -> Show Views -> Servers` from Eclipse main menu*

7. In the Servers view, right click on the blank area, select `New -> Server` in the context menu. It starts a New Server wizard to set up a server instance.
8. Select `GlassFish` and click `next`.

![Screenshot demo](Screenshots/Demo/Starting%20glassfish%20server.png "Start GlassFish Server - Screenshot demo")

9. Fill in `GlassFish 5` and `Java JDK 8` paths and click `next`.
10. Follow the rest of the process keeping default values.

## 3. Setting-Up a New Project

Now as everything is ready let's create a new Project

1. Create a new `Maven Project`. Click `File -> New -> Maven Project` from Eclipse main menu*
2. Select your Workspace or just keep the default params for first window
3. When selecting `archtype`, wait for options to download it may take some time. Select the ***webapp*** archtype: GroupID `org.apache.maven.archtypes` ArtifactID `maven-archtype-webapp` VERSION `1.4`

![Screenshot demo](Screenshots/Demo/Maven%20Archtype%20Selection.png "Select Maven Archtype - Screenshot demo")

4. Last step is to provide the GroupID, ArtifactID and Version of your project. We've chosen: GroupID `com.lifeleft` ArtifactID `lifeleft` VERSION `1.0-SNAPSHOT`

![Screenshot demo](Screenshots/Demo/Project%20Setup.png "Finish Project Configuration - Screenshot demo")

> ***IMPORTANT*** In the console it may ask you to confirm your configuartion
> If you find a line containing:  `Y : : ` just hit `Enter` 

Once The project is created

5. In the Project hierarchy tree find the folder `src/main`, Right-Click it then go `New -> Folder` to create a new folder named `java`

![Screenshot demo](Screenshots/Demo/Create%20Java%20folder.png "Create java folder - Screenshot demo")

> By default, the folder will be configured as a source folder

6. Create a new package called like your GroupID `com.lifeleft`
    1. Right-Click on `java` folder, then go `New -> Other` or `Ctrl + N`

    ![Screenshot demo](Screenshots/Demo/Create%20new%20package%20(1).png "Create new java package (step 1) - Screenshot demo")

    2. Search for `Java/package`

    ![Screenshot demo](Screenshots/Demo/Create%20new%20package%20(2).png "Create new java package (step 2) - Screenshot demo")

    3. Name it like your GroupID `com.lifeleft` and click finish

    ![Screenshot demo](Screenshots/Demo/Create%20new%20package%20(3).png "Create new java package (step 3) - Screenshot demo")

7. (Optional) The file `src/main/webapp/WEB-INF/web.xml` is useless so you can delete it (the file `web.xml` only)

![Screenshot demo](Screenshots/Demo/Delete%20file%20web-xml.png "Delete file web.xml - Screenshot demo")


## 4. Creating a new Bottom-Up Service

### Service Description

Your web service must therefore receive the following parameters:

+ a name of type **String**
+ a gender of type **String** (male/female)
+ an year of birth of type **Integer**

The service returns a response of type **String** corresponding to name and number of years left to live.

To calculate, we base ourselves on the life expectancy in France, which is:

+ Men: 79 years
+ Women: 85 years


### Service Implementation

1. In the package `com.lifeleft`, Create a new class called `LifeLeftService`

![Screenshot demo](Screenshots/Demo/Create%20new%20class%20(1).png "Create new java class (step 1) - Screenshot demo")
![Screenshot demo](Screenshots/Demo/Create%20new%20class%20(2).png "Create new java class (step 2) - Screenshot demo")

The necessary code is provided below



```Java
package com.lifeleft;

import java.util.Calendar;

public class LifeLeftService {

    private static final int MALE_LIFE_EXPECTANCY = 79;
    private static final int FEMALE_LIFE_EXPECTANCY = 85;

    private static final String GENDER_MALE   = "male";
    private static final String GENDER_FEMALE = "female";

    int evDeReference = 0;

    public String  yearsLeftToLive (String name, String gender, int yearOfBirth) {

        int lifeExpectancy = 0;

        if     (gender.equals(GENDER_MALE  )) lifeExpectancy = MALE_LIFE_EXPECTANCY;
        else if(gender.equals(GENDER_FEMALE)) lifeExpectancy = FEMALE_LIFE_EXPECTANCY;

        int yearsLeft = yearOfBirth + lifeExpectancy - Calendar.getInstance().get(Calendar.YEAR);

        return "Hello " + name + ", you have " + yearsLeft + " years left to live, make each day count !";
    }

}

```
2. Make sure your `pom.xml` file is well-configured. if not, copy the following code, save it and update your ***Maven Project*** by Clicking `Project -> Update Maven Project` from Eclipse main menu
```XML
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.lifeleft</groupId>
  <artifactId>lifeleft</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>war</packaging>

  <name>lifeleft: how much you have left to live? </name>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
  </properties>

  <build>
    <finalName>lifeleft</finalName>
    <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
      <plugins>
        <plugin>
          <artifactId>maven-clean-plugin</artifactId>
          <version>3.1.0</version>
        </plugin>
        <!-- see http://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_war_packaging -->
        <plugin>
          <artifactId>maven-resources-plugin</artifactId>
          <version>3.0.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.8.0</version>
        </plugin>
        <plugin>
          <artifactId>maven-surefire-plugin</artifactId>
          <version>2.22.1</version>
        </plugin>
        <plugin>
          <artifactId>maven-war-plugin</artifactId>
          <version>3.2.2</version>
		  <configuration>
		    <failOnMissingWebXml>false</failOnMissingWebXml>
		  </configuration>
        </plugin>
        <plugin>
          <artifactId>maven-install-plugin</artifactId>
          <version>2.5.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-deploy-plugin</artifactId>
          <version>2.8.2</version>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
</project>

```

3. add the ***WebService Annotations***

```Java
package com.lifeleft;

import java.util.Calendar;

import javax.jws.WebMethod;
import javax.jws.WebService;

@WebService(serviceName = "LifeLeft")
public class LifeLeftService {

    private static final int MALE_LIFE_EXPECTANCY = 79;
    private static final int FEMALE_LIFE_EXPECTANCY = 85;

    private static final String GENDER_MALE	  = "male";
    private static final String GENDER_FEMALE = "female";

    int evDeReference = 0;

    @WebMethod
    public String  yearsLeftToLive (String name, String gender, int yearOfBirth) {

        int lifeExpectancy = 0;

        if     (gender.equals(GENDER_MALE  )) lifeExpectancy = MALE_LIFE_EXPECTANCY;
        else if(gender.equals(GENDER_FEMALE)) lifeExpectancy = FEMALE_LIFE_EXPECTANCY;

        int yearsLeft = yearOfBirth + lifeExpectancy - Calendar.getInstance().get(Calendar.YEAR);

        return "Hello " + name + ", you have " + yearsLeft + " years left to live, make each day count !";
    }

}
```

### Running the Service 

*If the Servers view is not opened, try to open it first. Click `Windows -> Show Views -> Servers` from Eclipse main menu*

1. In the Servers view, make sure you have a `GlassFish 5` server. if not Jump back up to `Setting-Up GlassFish` section
2. If the server is not running (NOT displaying `[Started, Synchronized]`), right click on it, select `Start`.
3. Deploy your project.
    1. Right click ***Project Folder***, select `Run As -> Run on Server`.

![Screenshot demo](Screenshots/Demo/Run%20project%20(1).png "Deploy the project (step 1) - Screenshot demo")

    2. Select `GlassFish 5` server and click finish

![Screenshot demo](Screenshots/Demo/Run%20project%20(2).png "Deploy the project (step 2) - Screenshot demo")

Your ***WebService*** should be running on the following URL:

```URL
http://localhost:8080/lifeleft/LifeLeft
```
![Screenshot demo](Screenshots/Demo/Run%20project%20(3).png "Deployement Preview")


### Testing the Service 

Now as the service is Up and Running we can test it with SoapUI

1. First let's create a ***new Project***, select `File -> new SOAP Project` from SoapUI main menu.
2. Fill in a Project name `LifeLeft`, copy & make sure your ***WSDL*** URL is correct, leave the rest as default

![Screenshot demo](Screenshots/Demo/SoapUI%20(1).png "Create new SoapUI Project - Screenshot demo")

3. Create a new ***Test Case Suite***. Right-click project folder and select `new TestSuite`. You may leave the default name `TestSuite 1` 

![Screenshot demo](Screenshots/Demo/SoapUI%20(2).png "Create new TestSuite - Screenshot demo")

4. Create a new ***Test Case*** for our **Webservice**. Expand the **WebService** to make the **Request** visible. Right-click Request select `Add to TestCase`. 

![Screenshot demo](Screenshots/Demo/SoapUI%20(3).png "Create new TestCase (Step 1) - Screenshot demo")

5. In the **Popup** select `Create a new TestCase` (should be default). You may leave the default name `TestCase 1` 

![Screenshot demo](Screenshots/Demo/SoapUI%20(4).png "Create new TestCase (Step 2) - Screenshot demo")

6. Add the ***Request*** to the ***TestCase***. In the **Popup** leave the default params and click `OK`

![Screenshot demo](Screenshots/Demo/SoapUI%20(5).png "Add Request to TestCase - Screenshot demo")

> At this point a window to test the **WebService** should appear. Enjoy testing


7. Fill in some informations in the test XML file (arg0: name, arg1: gender, arg2: year of birth) and push the ***Green Triangle*** to run the test

![Screenshot demo](Screenshots/Demo/SoapUI%20(6).png "Testing Preview")

Here is the output

![Screenshot demo](Screenshots/Demo/SoapUI%20(7).png "Testing Preview")

