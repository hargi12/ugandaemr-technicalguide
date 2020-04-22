# Setting up a Development Enviornment

## Developer Prerequisites

### Minium Computer Hardware and Software Requirements

The minimum requirements for a developer machine are:

* OS: Windows 7, Ubuntu Linux 14 or Fedora 18, MacOSX 10.8 
* 2.5GHz Dual Core Intel Processor 
* 4GB RAM \(any less will slow down the development process\) 

### Technology Stack

UgandaEMR currently runs on OpenMRS Reference Application 2.7 which requires the following:

* MySQL 5.5+ \(5.6 recommended\) 
* Java 8 \(Java 6 and 7 will not run\) 
* Apache Tomcat 7+ \(no testing has been done on Tomcat 8\)

### Code Repository

The repositories are hosted under the METS Program organization on GitHub - [https://github.com/METS-Programme/](https://github.com/METS-Programme/)

* \[Aijar module\] \([https://github.com/METS-Programme/openmrs-module-aijar](https://github.com/METS-Programme/openmrs-module-aijar)\) - provides configuration and metadata for the UgandaEMR distribution
* \[UgandaEMR Reports\] \([https://github.com/METS-Programme/openmrs-module-ugandaemr-reports](https://github.com/METS-Programme/openmrs-module-ugandaemr-reports)\) - provides reporting functionality as well as pre-built reports

### Toolset

The development environment leverages the [OpenMRS SDK](https://wiki.openmrs.org/display/docs/OpenMRS+SDK) to run the software which requires the following:

* Maven 3.3.9
* Git 2.3.9
* GitHub account
* OpenMRS SDK - [https://wiki.openmrs.org/display/docs/OpenMRS+SDK](https://wiki.openmrs.org/display/docs/OpenMRS+SDK)
* IDE - any that you are comfortable is supported, a recommendation is the free  [Intellij IDEA Community Edition](https://www.jetbrains.com/idea/download/#)

### Setting up a Server using the SDK

**Prerequisites:**

* MySQL server running 
* MySQL user with privileges to create a database and a password recommended is openmrs with password openmrs. The root user with a blank password will create issues with the SDK setup
* JDK and Maven setup and available on the PATH so that commands can be run from anywhere on the file system 
* Internet connection to be able to download the required openmrs platform and module libraries 

**Installation Steps**

1. Set up the environment via the following command, chosing the serverId then follow the interactive instructions that follow. For many of them the defaults are adequate. Note that the environment will be set up the directory openmrs in the user's home directory

   `mvn openmrs-sdk:setup -Ddistro=org.openmrs.module:aijar:LATEST-SNAPSHOT`

   To set up a server with the ugandaemrpoc distro, one can use the command below

   `mvn openmrs-sdk:setup -Ddistro=org.openmrs.module:ugandaemrpoc:LATEST-SNAPSHOT`

2. Then startup the server `mvn openmrs-sdk:run -DserverId=[serverId]` which can be accessed at [http://localhost:8080/openmrs/](http://localhost:8081/openmrs/) \*NOTE\* the port may change depending on what was selected during the step \#1 above
3. Once you can see the login page, run the following script to bring the concept dictionary up-to-the latest version currently 1.0.13 - [https:\sourceforge.net\projects\ugandaemr\files\1.0.13\concept\_dictonary\_ref\_1.0.13.sql\download](https://sourceforge.net/projects/ugandaemr/files/1.0.13/concept_dictonary_ref_1.0.13.sql/download)
4. Clone the fork of your module to your computer
5. In the directory of the cloned module, there is need to setup the server created in step \#1 above so that user interface changes in the module are automatically updated to the server by running

   `mvn openmrs-sdk:watch -DserverId=[serverId]`

6. From now going forward when the server is started the latest changes in the module will be compiled and copied to the server

**NOTE:**

* Replace any placeholders like \[serverId\] with your own details without the brackets 
* The distro parameter version can be changed to the latest at the time 
* The port can also be changed which provides the ability to run multiple SDK versions at the same time on different ports 

### Upgrading the module versions on a Server

Once you have installed the distribution, you should be able to update it with the following command from the base directory of the ugandaemr project:

`mvn openmrs-sdk:deploy -DserverId=[serverId] -Ddistro=org.openmrs.module:aijar:NEW_VERSION`

The possible values of NEW\_VERSION:

* LATEST-SNAPSHOT: deploys the latest development version 
* 2.0.0 - last stable official release 

