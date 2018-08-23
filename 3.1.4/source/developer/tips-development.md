# Tips for plugin development

This page points some techniques you can use to make your development tasks more agile when writing plugins.

## Bootstrap a plugin using an archetype

Instead of creating a maven project from scratch, you can generate one quickly by leveraging the archetype... TODO

## Skipping package and deployment phases

In ["Introduction to plugin development"](./intro-plugin.md#development-lifecycle) we describe the typical steps developers may follow when developing Casa plugins. However, if by chance you ever touched upon the [internals](./plugin-management-internals#resource-extraction-and-registration) page, it's likely that you have come up with some shorcut to be quicker. Here we describe how to get the most out of this.

Any change you need to apply on the plugin you have been working on not that doesn't require the java compiler to pitch in, like edition of javascript, css, images, or ZK pages can be tested without redeploying your plugin. Here is what you need:

1. Connect to the VM where Gluu Server and Casa are running via SSH
1. Login to chroot
1. Locate the jetty directory where Casa was exploded. This can be found at `/opt/jetty-9.4/temp` and has the form `jetty-localhost-8091-casa.war-_casa-any-7350344229673686162.dir`
1. `cd` to `webapp/pl/<plugin-id>`
1. Upload to your VM the files you have changed that need revision
1. Retest your plugin features

Being able to change files this way don't seem like a big advantange, however, experience shows that for instance, editing ZK pages on the fly can save a lot of time, specially when it comes to changes in visual layout (a task which demands lots of attempts until getting the desired result). Also not only can you replace files but create new ones, this enables for the informal experiments one does while developing. 

Actually, you can write some Java without requiring compilation. In ZK pages you can include snippets of Java in `<zscript>` tags. See "zscript" in [ZUML Reference](./intro-plugin.md#reference-docs) and "Scripts in ZUML" in [ZK Developers' Reference](./intro-plugin.md#reference-docs). zscript can be used as a fast prototyping vehicle, however, refrain from using it in production artifacts.


## Write a good manifest!

This won't make you more agile, but taking the time to write good license and description notes in your plugin manifest file will allow yout to communicate more effectively to others about the features you are delivering with your artifacts. You can also use the description note to describe requisites your plugin may have (e.g. interacting with an external system, etc...).
