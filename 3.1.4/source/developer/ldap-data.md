# Manipulating LDAP data

Gluu LDAP directory is key in Gluu Casa [architecture](./architecture.md#backend). Plugins are very likely to require LDAP interaction so it's important to be aware of how this is materialized. Formerly in the [introductory page](./intro-plugin.md#ldap-sdk-for-java) we highlighted the importance of UnboundID LDAP SDK Persistence Framework as a vehicle to map LDAP entries into Java objects. We also mentioned about `casa-shared` module bringing an abstraction to easily perform CRUD. In this page we will get into the details and provide some useful examples.

## Requisites

Before proceding ensure you have:

- [a basic grasp of LDAP](./intro-plugin.md#ldap-notions)
- downloaded the [UnboundID LDAP SDK](https://github.com/pingidentity/ldapsdk/releases] (version 4.0.0 is OK). 
- skimmed through the persistence framework [doc page](https://docs.ldap.com/ldap-sdk/docs/persist/index.html) (also found in the SDK zip file). It will help you to start very quickly. Bookmarks in your browser pointing to that page and the API docs would be helpful.
- the means to connect to Gluu lightweight directory, as mentioned [here](./intro-plugin.md#a-running-gluu-casa-installation). Normally, you'll use the `o=gluu` base branch DN.

As an example, if your Gluu Server is backed by OpenLDAP, you can:

- Edit `/opt/symas/etc/openldap/symas-openldap.conf` and change `HOST_LIST` with `ldaps://127.0.0.1:1636/`
- Open port 1636 in your VM firewall
- Restart OpenLDAP (`service solserver restart`)

For a more general approach follow [these](https://gluu.org/docs/ce/user-management/local-user-management#manage-users-in-gluu-ldap) instructions.

## Know your LDAP

It is important to get some acquaintance with the structure of the directory. One you connect you will see two branches, `ou=appliances` and `o=...`. The former contains mostly configuration of the server itself, the latter holds more interesting stuff for developers such as:
- Users and groups data
- OpenID clients and scopes
- Custom scripts

Traverse the tree. Use your LDAP client to inspect schema, that way you can familiarize with the most relevant object classes (e.g. `gluuPerson`) and attributes types they can hold (e.g. `nickname`).

### Adding attributes to directory schema

While Gluu schema exhibits lots of attribute types, there are cases where you need to add your own attributes to cope with particular needs, for instance, storing user's age.

This [page](https://gluu.org/docs/ce/admin-guide/attribute#custom-attributes) is a reference doc demonstrating how an attribute can be added to directory schema. In this case an attribute is added to `gluuCustomPerson` object class, but you can use any other or even create your own. Basically you need to:

1. Choose a name and a description for the attribute.
1. Assign a syntax (e.g. string, boolean, etc.). For more information check RFC 4517 or search "LDAP syntax definitions" in the web.
1. Assign the attribute to one or more object classes.
1. Save the editions in the (plain text) schema file of your LDAP server.
1. Restart the LDAP service. Normally this service will not start if the supplied changes don't have the correct format expected by the LDAP implementation bundled in your Gluu Server.

For plugin development there is no need to register the attribute in oxTrust unless you know you'll need to inspect the attribute, for instance, in a user profile via oxTrust.

### Branches DNs

Instances of `org.gluu.casa.service.ILdapService` interface provide some `get*` methods to easily obtain distinguished names for the most relevant branches in the directory. Accessing DNs allow plugin developers to specify proper locations for searches or updates.

### POJOs for reuse

`casa-shared` provides a few [persistence-framework compatible POJOs](./intro-plugin.md#ldap-ped-pojos) you can reuse or extend when developing. Plugin requirements are varied so we decided not to provide ready-to-use classes for the majority of existing LDAP object classes. This would result in classes with several dozens of fields (plus associated getters and setters) that are not as meaningful as having small tailored classes focused on modeling the problem at hand. Additionally, writing your own classes will allow you to understand how modeling works and do troubleshooting if problems arise.

## Working with a persistence-aware class

If you have ever used the Java Persistence API (JPA), the term "object/relational mapping" may result familiar to you. It consists of a series of rules and annotations to facilitate managing relational data in Java applications. The LDAP persistence framework is aimed at solving a similar problem in LDAP domain, however, this is not a standard itself but a facility available in Ping Identity LDAP SDK for Java. 

The framework allows to express (via annotations) the logical rules to store a Java object into LDAP, and the conversion (retrieval) of an entry into a Java object.

!!! Note: 
    We highly encourage to visit the persistence framework [docs](https://docs.ldap.com/ldap-sdk/docs/persist/index.html) now. The framework is very small so it's a short reading. Emphasize on the example(s) shown.
    
Now that you have the grasp of the framework, let's proceed with an example. Here, we will generate a POJO with the tool for this purpose, minimize it to fit a particular need, and put it to work on real data.

<!--
Suppose your boss ask you to write 
que ejemplo poner basado en la lista de plugins por hacer: social, dev portal, gdpr, consent
----------

unboundid-ldapsdk-4.0.4\tools\generate-source-from-schema.bat --hostname <hostname> --port 1636 --bindDN "cn=directory manager,o=gluu" --bindPassword "<password>" --structuralClass <object-class> --rdnAttribute <rdn-attribute> --packageName <java-package> --className <java-class-name> --terse
-->
