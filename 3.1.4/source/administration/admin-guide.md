# Admin Guide - Credential Manager

## About two-factor authentication (2FA)

Strong (two-factor) authentication will be only available to users once they have added at least one credential in credential manager. By requiring users to register at least two strong credentials, the number of account lockouts that require admin intervention will be greatly reduced. If one credential is lost, there will be at least one fallback mechanism available. Avoiding user lockout is important because it prevents a serious burden for IT administrators.

The two required credentials do not need to be of the same type (two security keys or two supergluu devices, for instance): they can be of distinct type. Also, there is no limit in the number of credentials a user can enroll.

## Supported types of 2FA
Users will only be able to add credentials whose type match any of the enabled authentication methods set in the configuration file of the application (see the [Configuration page](configuration.md)). If not set, all already enabled methods in the Gluu server installation will be supported as long as they are part of the following restricted set:

* U2F security keys
* Super Gluu
* HOTP/TOTP
* OTP sent by SMS with the Twilio service

## Resetting a user's preferred method

In the event a user loses access to his account, you can revert the preferred authentication method to "password only" by following the steps shown in the [troubleshooting guide](troubleshooting.md)

## Administration console

The webapp puts at admins disposal the following functionalities via the graphical admin console:

* Switch password reset on/off
* Change logging level
* Custom branding
* OXD settings
* LDAP settings
* 2FA settings
* Choose authentication methods offered to users
* Reset users preferred method of authentication

These features map basically one-to-one with respect to the properties set in the configuration file `cred-manager.json`.

Once you login to the app with your admin credentials, you will land to admin console's page. To change or enroll your own credentials as regular users do, just click on the option "My credentials".

Most changes done via the admin console are applied instantly (so no additional action is required). When you change a setting that requires an application restart, you will be presented a proper descriptive message.
