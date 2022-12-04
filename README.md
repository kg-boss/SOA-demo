# SettingUp an SOA environment

## Requirements

+ Java JDK 17 or higher. *The latest JDK is recommanded (JDK 19 by the time this file was created)*
+ Jave JDK 8
+ GlassFish 5

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

## 2. SettingUp GlassFish

Now as Eclipse IDE is installed we can configure glassfish server

1. launch `Eclipse IDE`
2. open `Install New SOftware`
    1. go to `help`
    2. select `Install New SOftware`
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

