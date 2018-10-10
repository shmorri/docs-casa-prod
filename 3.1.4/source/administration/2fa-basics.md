# About Two-Factor Authentication (2FA)

## Availability

By default, strong (two-factor) authentication will be available to users of Casa once they have added at least two credentials. By requiring users to register two strong credentials, the number of account lockouts that require admin intervention will be greatly reduced. If one credential is lost, there will be at least one fallback mechanism available. Avoiding user lockout is important because it prevents a serious burden for IT administrators.

You can increase or even reduce this value at your discretion via the [admin console](admin-console.md#2fa-settings).

To further reduce the likelihood of lockouts, Casa forces users to initially enroll one OTP credential before any other. OTP credentials are generally more accessible than their counterparts (like U2F) since they normally don't demand special conditions from the device used to access, like having a USB port.

There is no limit to the number of credentials a user can enroll, and credentials do not need to be of the same type: any combination is valid as long as one is OTP. If a user attempts to delete their only available OTP credential, a prompt will appear warning that doing so will disable 2FA, that is, resorting to password authentication.

## Supported types of 2FA

Users will only be able to add credentials with a type matching one of the already enabled authentication methods in the admin console. See the [Configuration page](./configuration.md) to learn more. Out of the box, all the following authentication methods are supported:

- U2F security keys
- Super Gluu
- HOTP/TOTP
- OTP sent by SMS with the Twilio service

## Resetting a user's preferred method

In the event a user loses access to his account, you can revert the preferred authentication method to "password only" by following the steps shown in the [troubleshooting guide](faq.md)
