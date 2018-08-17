# Architectural details

## Application

Gluu Casa ("Casa") is a web application (more specifically, a Java EE 7 web module).

### UI aspects

To generate HTML content this application uses the [ZK Community Edition](https://www.zkoss.org) framework. Pages built with ZK are lightweight, still preserving a Java backend binding typical of JSF applications. The lifecycle of ZK pages and components is simpler than that of JSF, but at the same time shares many aspects such as interfaces defined in terms of XML tags and usage of EL expressions. 

ZK helps developers write highly interactive interfaces in a fast paced manner still using similar dialects of other Java-based UI frameworks. Additionally, despite it does a lot of Ajax in the browser, no knowledge about Javascript is required.

There is a handful of approaches for ZK development, particularly in Casa the MVVM pattern is used. This pattern has 3 roles: View, Model, and ViewModel which allow to achieve a separation of data and logic from presentation. For more information see [ZK MVVM Reference](http://books.zkoss.org/zk-mvvm-book/8.0/).

Plugin developers are encouraged to use MVVM development style of ZK, however any other approach is pluggable and should supported.

### Backend

From the server-side perspective, the following summarizes the most relevant aspects:

- Contexts and Dependency Injection (CDI)

Casa uses Weld 3.0 (JSR-365 aka CDI 2.0) for managed beans. The most important aspects of business logic are implemented through a set of beans found in Java package `org.gluu.credmanager.core`.

Managed beans are injected in UI controller classes (ZK ViewModels) by means of custom ZK annotations. ZK pages can access bean properties via EL expressions when they are annotated `javax.inject.Named`.

- Logging

Casa uses "Simple Logging Facade for Java" (SLF4J) with the Log4j2 binding. Log files are located in `/opt/gluu/jetty/casa/logs` of Gluu Server chroot container. To get more information on loggers and appenders, check the `log4j2.xml` file found in `/WEB-INF/classes` of the application war. Alternatively, you can check the file online in [github](https://github.com/GluuFederation/casa/blob/version_3.1.3/app/src/main/resources/log4j2.xml) (point to the branch that corresponds to your Casa version).

- Async timers

Casa currently employs two asynchronous jobs to periodically clean users trusted devices list if any, and to detect changes in relevant custom interception scripts and notify plugin handlers of this event. For this task, the Quartz 2 library is used.

- Plugin framework

The "Plugin Framework for Java" ([PF4J](http://www.pf4j.org)) is the mechanism Casa supports for plugin management. Plugins are artifacts intended to extend and under certain circumstances, override application functionalities.

Plugins are added at runtime, which, requires no restart of Casa. Additionally, plugins can be temporarily stopped or permanently removed.
To add a plugin, a jar file must be uploaded via the admin dashboard. 

- LDAP persistence

As expected, access to LDAP is key in Casa. To cover this need, the "UnboundID Persistence Framework" was employed. This is a small framework (part of the more general "UnboundID LDAP SDK") which allows to easily establish a mapping between Java objects (POJOs) and LDAP entries facilitating CRUD operations a lot. Plugins leverage some of the persistence framework tools as well as some functionalities exposed directly by the application which makes access to LDAP fairly easy to understand and highly productive at the same time. 

- Rest services

Plugins can add RESTful web services dynamically. For this purposes the well-known JBoss RestEasy 3.0 libraries were included in this project. Additionally, in future releases Gluu Casa will expose some API endpoints that leverage these libraries. 

## External dependencies

Gluu casa has some few key external dependencies to work properly

### Authorization server

The oxAuth component of your Gluu Server installation is the most relevant. Despite Casa leverages (oxd)[#oxd-server] to simplify the authorization process, some endpoints of oxAuth are being consumed directly to support credential enrollment functionalities or gathering certain configuration parameters. 

More importantly, the workflow exhibited by the authorization server when an authentication attempt is made by the application depends on a set of interception scripts and custom pages which were built specifically for this application. 

### oxd server

oxd server (and the oxd-https-extension if used) acts as a mediator to simplify the authorization process (which follows the OpenID connect code flow). This is a required component whose location is supplied during Casa installation (in case administrators don't have an oxd server available, they can make use of the option to install and configure on instance).

### Geolocation service

Casa uses the "ip-api" geolocation service for two purposes: gathering basic location information in the moment of the login itself and when enrollments take place for super gluu devices. The latter being available only if the administrator has added supergluu as one of its [enabled methods](../administration/#enabled-methods) previously.

Casa supports free and pro service of ip-api.

## Data storage

### LDAP

Casa uses the same lightweight directory (LDAP) of your Gluu Server to store users data such as [enrolled credentials](../administration/credentials-stored.md), preferred authentication method, users' trusted devices information, and so on. 

It is recommended that developers writing plugins leverage the existing directory to save their data. Nonetheless, any other alternative mechanism can be embraced (e.g. a database); it is up to administrators and developers to agree on how to incorporate this to the current stack.

### Config file

For convenience, all configuration parameters are stored in a JSON-formatted file located at `/etc/gluu/conf/casa.json` of the Gluu Server chroot container. This file contains all aspects that allow to customize/parameterize the application behaviour, in other words, it stores all the settings accessible through the application's [admin dashboard](../administration/admin-console.md).

Manipulating a plain-text file is a highly accessible alternative when, by means of some misconfiguration, administrators cannot login to access the dashboard. A more common use case is that of cloning an environment with subtle differences in configuration.

To force the application pick changes manually applied to this file, a [restart](../administration/faq.md#how-do-i-restart-the-application) is required.

### Plugins directory

Jar files of all [plugins](#plugin-framework) (started/stopped) reside in filesystem at `/opt/gluu/casa/plugins`.

## Runtime environment

These are key facts for potential Casa developers:

* Underlying operating system: The linux distro where your Gluu Server is running. For plugin development, there is no restriction on operating system.

* Java SE version: Gluu Server comes with JDK 1.8 installed in chroot container, that is, the war file of Casa uses a JVM in such version.  For plugin development, JDK 1.8 is recommended as well.

* Application container: Casa runs in a Jetty 9.4 instance (which is setup upon installation of Casa). Plugin writers don't need to use an application container since they only produce jar files.

* Build tool: To write plugins the usage of Maven 3 is recommended, however any build system which allows to create fat (Uber) jars will suffice.
