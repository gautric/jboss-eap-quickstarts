ejb-in-ear: Deployment of an EAR Containing a JSF WAR and an EJB JAR
====================================================================
Author: Paul Robinson  
Level: Intermediate  
Technologies: EJB, EAR  
Summary: Packages an EJB JAR and WAR in an EAR  
Target Product: EAP  
Product Versions: EAP 6.1, EAP 6.2, EAP 6.3, EAP 6.4  
Source: <https://github.com/jboss-developer/jboss-eap-quickstarts/>  

What is it?
-----------

This example demonstrates the deployment of an EAR artifact. The EAR contains: *JSF 2.0* WAR and an *EJB 3.1* JAR.

The example is composed of three maven projects, each with a shared parent. The projects are as follows:

1. `ejb`: This project contains the EJB code and can be built independently to produce the JAR archive.

2. `web`: This project contains the JSF pages and the managed bean.

3. `ear`: This project builds the EAR artifact and pulls in the ejb and web artifacts.

The root `pom.xml` builds each of the subprojects in the above order and deploys the EAR archive to the server.


The example follows the common "Hello World" pattern. These are the steps that occur:

1. A JSF page asks the user for their name.
2. On clicking _Greet_, the name is sent to a managed bean named `Greeter`.
3. On setting the name, the `Greeter` invokes the `GreeterEJB`, which was injected to the managed bean. Notice the field annotated with `@EJB`.
4. The response from invoking the `GreeterEJB` is stored in a field (message) of the managed bean.
5. The managed bean is annotated as `@SessionScoped`, so the same managed bean instance is used for the entire session. This ensures that the message is available when the page reloads and is displayed to the user.

System requirements
-------------------

The application this project produces is designed to be run on Red Hat JBoss Enterprise Application Platform 6.1 or later. 

All you need to build this project is Java 6.0 (Java SDK 1.6) or later, Maven 3.0 or later.


Configure Maven 
-------------

If you have not yet done so, you must [Configure Maven](https://github.com/jboss-developer/jboss-developer-shared-resources/blob/master/guides/CONFIGURE_MAVEN.md#configure-maven-to-build-and-deploy-the-quickstarts) before testing the quickstarts.


Start the JBoss EAP Server
-------------------------

1. Open a command prompt and navigate to the root of the JBoss EAP directory.
2. The following shows the command line to start the server:

        For Linux:   EAP_HOME/bin/standalone.sh
        For Windows: EAP_HOME\bin\standalone.bat


Build and Deploy the Quickstart
-------------------------

_NOTE: The following build command assumes you have configured your Maven user settings. If you have not, you must include Maven setting arguments on the command line. See [Build and Deploy the Quickstarts](../README.md#build-and-deploy-the-quickstarts) for complete instructions and additional options._

1. Make sure you have started the JBoss EAP server as described above.
2. Open a command prompt and navigate to the root directory of this quickstart.
3. Type this command to build and deploy the archive:

        mvn clean install jboss-as:deploy

4. This will deploy `target/jboss-ejb-in-ear.ear` to the running instance of the server.

 

Access the application 
---------------------

The application will be running at the following URL <http://localhost:8080/jboss-ejb-in-ear>.

Enter a name in the input field and click the _Greet_ button to see the response.


Undeploy the Archive
--------------------

1. Make sure you have started the JBoss EAP server as described above.
2. Open a command prompt and navigate to the root directory of this quickstart.
3. When you are finished testing, type this command to undeploy the archive:

        mvn jboss-as:undeploy


Run the Quickstart in JBoss Developer Studio or Eclipse
-------------------------------------
You can also start the server and deploy the quickstarts or run the Arquillian tests from Eclipse using JBoss tools. For more information, see [Use JBoss Developer Studio or Eclipse to Run the Quickstarts](https://github.com/jboss-developer/jboss-developer-shared-resources/blob/master/guides/USE_JDBS.md#use-jboss-developer-studio-or-eclipse-to-run-the-quickstarts) 


Debug the Application
---------------------

If you want to debug the source code or look at the Javadocs of any library in the project, run either of the following commands to pull them into your local repository. The IDE should then detect them.

        mvn dependency:sources
        mvn dependency:resolve -Dclassifier=javadoc
