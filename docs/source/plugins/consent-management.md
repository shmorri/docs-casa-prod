# Consent Management Plugin
## Overview 
The Consent Management plugin gives end-users the ability to view and revoke previously granted authorizations provided to applications accessed with their account in a Gluu Server. 

## Requirements

- The plugin jar file must match the version of your Casa (and Gluu Server) installation.

## Installation

1. Login to Casa using an administrator account

1. Visit `Administration console` > `Casa plugins`

    ![plugins page](../img/plugins/plugins314.png)

1. Click on `Add a plugin...` and select the plugin jar file

1. Click on `Add` 

## User guide

Once the plugin is activated, a new "Consent management" link will appear in the lefthand navigation menu for all users. 

New entries are added automatically whenever the user is prompted for, and authorizes the release of their personal data to an application accessed using their Gluu account.   

![image](https://user-images.githubusercontent.com/5271048/53795147-f5e7d900-3ef6-11e9-9907-ee4c2be2516f.png)

### Revoking consent
When a previously granted consent decision is revoked, the user will be re-prompted to authorize release of their data if/when they attempt to access the application again. 

