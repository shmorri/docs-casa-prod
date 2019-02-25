# About localization
 
Casa has multilingual support by means of resource bundles. Administrators supply bundles in the form of plain text files ending with `.properties` file extension.
 
By default, Casa contains 3 bundles, each in a separate file as shown [here](https://github.com/GluuFederation/casa/tree/version_3.1.6/app/src/main/resources/labels). These bundles contain the internationalization labels in English language, as displayed in a default Casa installation. If you want to add for instance support for French, you would have to create the following files:
 
- `user_fr.properties`
- `admin_fr.properties`
- `general_fr.properties`
 
The first one contains labels mostly found in regular users pages, while the second is focused on administrator-only pages. The third (general) contains a small set of terms to be potentially reused everywhere in the app or in developed plugins.
 
## Adding internationalization labels

To supply labels in a particular language (or even if you want to override the English translation provided), do the following:

1. Login to chroot
1. Extract Casa default labels: `/opt/jre/bin/jar -xf /opt/gluu/jetty/casa/webapps/casa.war WEB-INF/classes/labels`
1. Run `mv WEB-INF/classes/labels/*.properties .` and delete WEB-INF dir: `rm -R WEB-INF/`
1. Add the appropriate suffix to the properties files found in the current directory, ie. `_de` for German, `_es` for Spanish, `_ja` for Japanese, etc.
1. Edit the contents of files accordingly. Use UTF-8 encoding for opening and saving.
1. `cd` to `/opt/gluu/jetty/casa/static`
1. Create directory `i18n` if it does not exist: `mkdir i18n`
1. Transfer the properties files to the `i18n` folder
1. Ensure `jetty` user has permission for reading the files
1. Restart casa: `service casa restart`

Login to the application and review your work. Apply any editions needed and repeat the process.

## How are labels picked?

In Casa, the rule for displaying contents is leveraged from the [underlying framework](https://www.zkoss.org/wiki/ZK%20Developer's%20Reference/Internationalization). In short, the locale to use per session is picked based on the end-user browser settings.

As an example, if your browser was configured to use English of United States, the locale will be `en_US`. This means that files ending in  `_en_US.properties` will be considered first. In case of no match, the country code is removed and thus `_en.properties` is tried. The last attempt removes the locale entirely, thus matching the default label files bundled with Casa.

## Localization in plugins

Plugins also support localization through the "labels" bundle. Check [here](../developer/intro-plugin.md#anatomy-of-a-plugin) for more information. This is useful for plugins developed by your organization, if you have installed plugins developed by Gluu, they will only contain a single default English file.

To add your own translation of plugin texts, proceed as below:

1. `cd` to the folder where you stored the jar file of the plugin of interest. This file was delivered to you by Gluu staff directly.
1. Extract plugin's default labels (requires Java bin on your path): `jar -xf JAR_FILE labels/zk-label.properties`
1. `cd` to `labels` folder
1. Add the appropriate suffix to the properties file, ie. `_de` for German, `_es` for Spanish, `_ja` for Japanese, etc.
1. Edit the contents accordingly. Use UTF-8 encoding for opening and saving.
1. Connect to your Gluu Casa Server/VM and login to chroot
1. `cd` to `/opt/gluu/jetty/casa/static`
1. Create directory `i18n` if it does not exist: `mkdir i18n`
1. Transfer the properties file to the `i18n` folder
1. Ensure `jetty` user has permission for reading
1. Restart casa: `service casa restart`

**Note**: Since most Gluu Inc. plugins have a `zk-label.properties` you can accumulate all plugins texts into a single file, or you can use a different filename for each plugin.

## The syntax of properties files

Administrators acquainted with the format used for properties files in Java will find Casa resource bundle files familiar. The format used in Casa differs slightly but it is more powerful. To learn more about this topic, visit this [page](https://www.zkoss.org/wiki/ZK%20Developer's%20Reference/Internationalization/Labels/The%20Format%20of%20Properties%20Files).

## Tips

- Not all entries present in default label files have to be translated in your own localized versions. If you are comfortable with the current text for a particular entry, you can simply remove it so the one found in default files will be used.

- There is no need to supply specific translations for countries. While supported, most of time it suffices to create files suffixed with, for instance `_es`, and not necessarily several like `_es_CO`, `_es_AR`, `_es_EC`, `_es_ES`, etc. 

- Actual filenames for properties files are not relevant. Upon start, Casa will parse all properties files present in `i18n` folder.
