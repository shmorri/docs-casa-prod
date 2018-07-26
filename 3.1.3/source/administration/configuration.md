# Configuration

## Overview

After installation you may like to proceed with the following administrative tasks:

* Add specific types of second factor authentication
* Change oxd configuration

## Enabling specific types of 2FA

In order to implement a specific type of 2FA, applicable custom scripts need to be configured and enabled. In the oxTrust UI, navigate to  `Configuration` > `Manage custom scripts`. 

Enable the authentication script for each type of 2FA credential that should be manageable in Credential Manager. Supported options include: U2F, Super Gluu, OTP, and Twilio SMS.  

A recommended practice is to enable one script in the Gluu Server, then add (enable) the associated method in cred-manager. Test and confirm enrollment and authentication is working as expected, then continue adding other desired 2FA methods. Employ a user other than `admin` to test enrollments as a relogin is needed every time a new method is added. This will also prevent locked outs of your `admin` account.

!!! Note
    Learn more about how the Gluu Server handles authentication in the [user authentication intro](https://www.gluu.org/docs/ce/authn-guide/intro). In addition, to learn more about how custom interception scripts work, review the [custom script tutorial](https://www.gluu.org/docs/ce/admin-guide/custom-script). 

### Confirming script functionality

In order to ensure the authentication scripts are properly configured in the Gluu Server, it is advisable to:

* Check the contents of the `oxauth_script.log` file (found at `/opt/gluu/jetty/oxauth/logs`). You should not see errors; only successful initialization messages. Every time a new script is enabled, give the server a minute to pick up the changes.

* The scripts included in the default Gluu Server distribution should provide basic working functionality. To see a script in action, enable a script in `Configuration` > `Manage custom scripts`, then set it as the default oxTrust acr in `Manage authentication` > `Default authentication method` > `oxTrust acr`. Open an incognito browser and login to your oxTrust dashboard. By default, your 2FA credential will be enrolled during the first authentication attempt. 

## Change oxd configuration

### Providing license details

If upon installation you did not provide oxd license details, you can do so by editing the `oxd-config.json` file of oxd-server.

Navigate to the directory where oxd-server is installed (if oxd was installed by the setup script, it is located in **???** of Gluu chroot).

Open the file `conf/oxd-conf.json` and fill the following fields accordingly:

* license_id
* public_key
* public_password
* license_password

After saving the file, restart oxd (by issuing for instance `service oxd-server restart`). If you check the log file of oxd located at `/var/log/oxd-server.log` you will see a message like 

```
TRACE [...] License is validated successfully.
TRACE [...] License data: LicenseMetadata{creationDate=..., expirationDate=...}
INFO  [...] Server socket is bound to port: 8099, with timeout: 0 seconds. Start listening for notifications.
```

that indicates your license is valid and oxd is operating correctly.

To proceed, just [restart cred-manager](faq.md#How-to-restart-the-application).

### Point to a different server

If you want cred-manager to use a different oxd server, you can specify these details via the app's admin UI. There is no need to do application restarts for this case but if for any reason you cannot login to cred manager due to oxd misconfigurations, do the following:

* Navigate to `/etc/gluu/conf`
* Edit the config file of the application `cred-manager.json`. Provide the oxd details in under the "oxd_config" section.
* Save your file and restart the application
* [Check the logs](#check-the-logs), you will see a successful message regarding to oxd registration in it.
* Login to the application


