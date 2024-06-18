# telosys-spring-boot

Create a simple Spring Boot application derived from an existing database

## Installation

 * Download Telosys from https://www.telosys.org/download/telosys-cli/index.html
 * Install the downloaded file using the instructions at https://doc.telosys.org/telosys-cli/cli-installation-linux for Mac or Linux or https://doc.telosys.org/telosys-cli/cli-installation-windows for windows 

### Run the Command Line Interface

 * Create a new directory (home is a good choice) and
 * From the new directory run tt
 * Should get the telosys prompt
```
BASEDIR = .
 
    ______     __                     
   /_  __/__  / /___  _______  _______
    / / / _ \/ / __ \/ ___/ / / / ___/
   / / /  __/ / /_/ (__  ) /_/ (__  ) 
  /_/  \___/_/\____/____/\__, /____/  
                        /____/  4.1.1-001 (build: 240112.0917.664)
Enter ? for help
telosys>
```

### Initialize

 * Run __h .__ to initialize the home directory
 * The telosys prompt is updated with a "#"
```
telosys#>
```
 * Run __init__ to create the Telosys folders and files

### Create the model from the database

 * In any text editor, modify TelosysTools/databases.yaml
 * Update the url, user, and password in the section for the database you are using (for example PostgreSQL is in the section with an id of pg)
 * Add the driver file for the database to the lib folder (for example the PostgreSQL driver is available at https://mvnrepository.com/artifact/org.postgresql/postgresql)
 * Create a local telosys model from the database by running the new model command (for example for PostgreSQL run **nm mymodel pg**)
 * Should end with
```
Model 'mymodel' created. Current model is now 'mymodel'
telosys#(mymodel)>
```

### Install the template bundle

 * Switch to the github repository using __gh jshepard-chariot__
 * Install the bundle using __ib telosys-spring-boot__
 * Load the bundle using __b telosys-spring-boot__
 * Should end with an updated prompt
```
telosys#(mymodel)[telosys-spring-boot]>
```

### Configure the generation properties

 * In any text editor, modify TelosysTools/telosys-tools.cfg
 * Update **ROOT_PKG** to the root package for the generated code (for example com.changemecompanyname.changemeprojectname)
 * Update **ProjectVariable.MAVEN_ARTIFACT_ID** (for example changemeprojectname)
 * Update **ProjectVariable.MAVEN_GROUP_ID** (for example com.changemecompanyname)
 * Add **ProjectVariable.DATABASE_URL** to be the connection url for the database
 * Add **ProjectVariable.DATABASE_USER** for the database connection
 * Add **ProjectVariable.DATABASE_PASSWORD** for the database connection
 * SRC and RES near the top of the files are used as is. The remaining variables are not used in this template bundle

### Generate the code

 * Back in the Telosys command line run __gen * *__
 * At the **Do you want to launch the generation [y/n] ?** prompt select y
 * The successful result should end with something like
```
[INFO] ----- Generation without entity
[INFO] Gen : main-resources/application_properties.vm : (no entity)
[INFO] OK :  src/main/resources/application.properties
[INFO] Gen : main_java.vm : (no entity)
[INFO] OK :  src/main/java/com/mycompany/Main.java
[INFO] Gen : pom_xml.vm : (no entity)
[INFO] OK :  pom.xml
+-------------------
| (i) INFORMATION 
| END OF GENERATION
| 
|  0 resources(s) copied.
|  23 file(s) generated.
|  0 generation error(s).
+-------------------
```
 * Run **exit** to leave the Telosys CLI

### Build and Run the application

 * From the terminal run **mvn package** (assumens maven is installed)
 * Run **java -jar target/myproject-1.0.0.jar**
