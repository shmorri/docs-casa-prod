# Working with menus

!!! Note
    It is highly recommended you follow the [Writing your first plugin](writing-first.md) guide before reading this contents.
    
## Overview

In introductory pages we mentioned developers can customize three types of menus: user, admin, and drop down. This can be achieved by implementing extension point `org.gluu.credmanager.extension.navigation.NavigationMenu`.

Every extension point you implement specifies which type of menu item it is intended by supplying a return value for method `menuType`. Valid return values are `MenuType.USER`, `MenuType.ADMIN_CONSOLE`, or `MenuType.AUXILIARY`.

Method `getContentsUrl` references a path to a page that can contain markup of any kind. This markup will be evaluated and added to the corresponding menu. The path is relative to the `assets` directory of your plugin.

Recall all menu items are added after Casa defaults. For example, if you are targetting user menus, the 2FA menu and password reset will be shown first, those dynamically added come afterwards.

Since plugins can have several extensions, and even several plugins can be added to a Casa installation, there must be some way to organize the order of appearance of menu items contributed by plugins. For this, `getPriority` method is used: every `NavigationMenu` extension should return a number between 0 and 1 for it. The higher the value, the upper position this menu contents will occupy in the overall menu.

This strategy allows developers to place their menu items in a specific position if there is prior knowldege about the priority of already existing menu items. For this reason, it is **highly** recommended to include somewhere in your markup the priority of the items you are adding. To avoid putting hardcoded values, you can use the `priority` parameter which is passed to your zul files when they contain menu-ish markup. 

As an example, in the menu item added in the [HelloWorld](writing-first.md#menuzul) plugin, you can use something like:

```
<a class="..." href="..." data-priority="${priority}">
	...
</a>
```

so that others know which the priority of your markup is upon code inspection. This allows other developers to choose suitable priority values for use in `getPriority`.

## Markup that should be used

While you can point in your menu extension to a zul page containing basically anything, you should be careful with code supplied. The following are some tips:

- To preserve a consistent look and feel, you should use similar markup as in default Casa menu items. If possible, inspect the zul code used to generate such markup, not the one appearing in the browser because it can be more verbose than needed. The following is a list of files you may like peeking at (these are from [Casa repo](writing-first.md#download-project) itself):

   - `app/src/main/webapp/menubuttons.zul` for regular users menu
   - `app/src/main/webapp/admin/menu.zul` for admin dashboard menu
   - `app/src/main/webapp/header.zul` for dropdown (top-right) menu
   
- Try using simple static markup for menu items. Avoid using long expressions or complex logic to generate markup. Since every page loaded incurs evaluating your zul code, it is desirable to keep it lightweight.

- Ensure your zul content won't end up in runtime evaluation error under any circumstance. This may render the app unusable since no page could be loaded. This applies for both user and drop-down menu.
