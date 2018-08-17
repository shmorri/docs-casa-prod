# Writing your first plugin

In this page we will disect the "Hello world" plugin project, apply editions on its code, do the packaging, deploy, and testing on a Gluu Casa installation.

## Requirements

Requirements for this task are the same as those listed in the [introductory page](intro-plugin.md#requirements-and-tools) except for LDAP-related stuff which is not needed. Additionally, maven will be used as build tool. If you don't want to use maven you'll need to investigate how to perform the tasks in the tool of your preference. 

If you skipped ["Introduction to plugin development"](intro-plugin.md) we strongly encourage you to glance at it now.

## Hello?

Hello world is minimalistic plugin that showcases very basic aspects of plugin development. This plugin will simply add a menu item to Casa users menu that takes to a separate page showing a salutation. In this page you can enter some text, execute server-side logic and update the UI back accordingly.

### Download project

Let's start by downloading the code. Hello World plugin is found inside the Gluu Casa project itself. This way you can easily check the underlying APIs and real world UI pages, particularly, the [`casa-shared` module](intro-plugin.md#casa-shared-module) being of great interest.

If you have `git` installed in your machine, issue the following command. Replace the content in the angle brackets with your Gluu Casa version (e.g. "version_3.1.3"):

```
$ git clone https://github.com/GluuFederation/casa.git
$ git checkout <branch>
```

Alternatively you can download a zipped version of the project from github. Visit this [page](https://github.com/GluuFederation/casa), then ...


### Anatomy