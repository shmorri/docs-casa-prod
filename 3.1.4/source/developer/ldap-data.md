# Manipulating LDAP data

Gluu LDAP directory is key in Gluu Casa [architecture](./architecture.md#backend). Plugins are very likely to require LDAP interaction so it's important to be aware of how this is materialized. Formerly in the [introductory page](./intro-plugin.md#ldap-sdk-for-java) we highlighted the importance of UnboundID LDAP SDK Persistence Framework as a vehicle to map LDAP entries into Java objects. We also mentioned about `casa-shared` module bringing an abstraction to easily perform CRUD. In this page we will get into the details and provide some useful examples.

## Requisites

Before proceding ensure you have:

- [Basic grasp of LDAP](./intro-plugin.md#ldap-notions)
- Downloaded the [UnboundID LDAP SDK](https://github.com/pingidentity/ldapsdk/releases] (version 4.0.0 is OK). 
- Skim through the persistence framework [doc page](https://docs.ldap.com/ldap-sdk/docs/persist/index.html) (also found in the SDK zip file). It will help you to start very quickly. Bookmarks in your browser pointing to that page and the API docs would be helpful.
- Means to connect to Gluu lightweight directory, as mentioned [here](./intro-plugin.md#a-running-gluu-casa-installation). Normally, you'll use the `o=gluu` base branch DN.

As an example, if your Gluu Server is backed by OpenLDAP, you can:

- Edit `/opt/symas/etc/openldap/symas-openldap.conf` and change `HOST_LIST` with `ldaps://127.0.0.1:1636/`
- Open port 1636 in your VM firewall
- Restart OpenLDAP (`service solserver restart`)

For a more general approach follow [these](https://gluu.org/docs/ce/user-management/local-user-management#manage-users-in-gluu-ldap) instructions.

## Know your LDAP

It is important to get some acquaintance with the structure of the directory. One you connect you will see two branches, `ou=applicances` and `o=...`. The former contains mostly configuration of the server itself, the latter holds more interesting stuff for developers such as:
- Users and groups data
- OpenID clients and scopes
- Custom scripts

Traverse the tree. Use your LDAP client to inspect schema, that way you can familiarize with the most relevant object classes (e.g. `gluuPerson`) and attributes types they can hold (e.g. `nickname`).

### Adding attributes to directory schema

While Gluu schema exhibits lots of attribute types, there are cases where you need to add your own attributes to cope with particular needs, for instance, storing user's age.
<!--
----------
`casa-shared` already provides some persistence-framework compatible POJOs that you can reuse or extend when writing plugins: []
(./intro-plugin.md#ldap-ped-pojos)

unboundid-ldapsdk-4.0.4\tools\generate-source-from-schema.bat --hostname <hostname> --port 1636 --bindDN "cn=directory manager,o=gluu" --bindPassword "<password>" --structuralClass <object-class> --rdnAttribute <rdn-attribute> --packageName <java-package> --className <java-class-name> --terse
-->