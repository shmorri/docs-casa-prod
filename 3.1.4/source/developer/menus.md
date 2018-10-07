# Working with menus

!!! Note
    It is highly recommended you follow the [Writing your first plugin](writing-first.md) guide before reading this page contents.
    
In introductory pages we mentioned developers can customize three types of menus: user, admin, and drop down. This can be achieved by implementing extension point `org.gluu.credmanager.extension.navigation.NavigationMenu`.

Every extension point you implement specifies which type of menu item it is intended by supplying a return value for method `menuType`. Valid return values are `MenuType.USER`, `MenuType.ADMIN_CONSOLE`, or `MenuType.AUXILIARY`.

<!--Method `getContentsUrl` references a path to a page that can contain markup of any kind -->

<!-- show the priority of menu item-->
