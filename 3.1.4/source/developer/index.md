# Developer Guide

## Plugins

### What are plugins?

A plugin is an artifact packaged in a Java ARchive (<i>jar</i> file) that augments the functionalities available in your default Gluu Casa installation. Under certain circumstances, plugins can override existing application functionalities.

Plugins are mostly written in the Java programming language, but Kotlin can also be used.

#### What can you do with plugins?

Plugins are very versatile, the following is by no means an extensive list of things you can do via plugins:

- Add menu items in user's menu, top-right dropdown menu, or admin's dashboard menu
- Add UI pages with arbitrary content (and backend-functionality!), this also applies for the admin dashboard
- Add static files (e.g. Javascript, images, stylesheets, etc.)
- Add RESTEasy services
- Add or override authentication mechanisms to be supported by the application

In addition to the above:

- Any plugin can have easy access to the underlying LDAP of the Gluu Server where casa was installed
- Plugins can onboard their own libraries (jar files) and classes

#### What can't you do?

- Remove, deactivate or alter existing menu items found in your default installation or added by other plugins
- Alter the way in which certain features look or work such as: password reset, default admin dashboard functionalities, logout, etc.
- Plug custom logic to intercept calls or listen events when they occur (e.g. trigger a notification when a user has enrolled a specific type of credential)
- Alter the authentication flow. While this is not feasible via plugins, you can customize the flow by editing the Casa [interception script](https://gluu.org/docs/ce/admin-guide/custom-script) and its associated custom pages bundled with your Gluu Server installation 3.1.4 or higher.
- Use Dependency Injection

### Plugin basics

- [Architectural details](./architecture.md)
- [Introduction to plugin development](./intro-plugin.md)
- [Writing your first plugin](./writing-first.md)

### Common tasks

- [Working with menus](./menus.md)
- [Adding UI pages](./ui-pages.md)
- [Manipulating LDAP data](./ldap-data.md)
- Adding REST services
- Adding/overriding authentication mechanisms

### Other topics

- [Tips for plugin development](./tips-development.md)
- [Internals of plugin management in Casa](./plugin-management-internals.md)
