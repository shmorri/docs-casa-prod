# Gluu Casa 3.1.6 Documentation

## Overview

Gluu Casa ("Casa") is a self-service web portal for end-users to manage authentication and authorization data for their account in a [Gluu Server](https://gluu.org/docs/ce). 

For example, as people interact with an organization's digital services, they may need to:

- Enroll, delete and manage two-factor authentication (2FA) credentials for their account (e.g. FIDO security keys, mobile apps, phone numbers, etc.)
- Turn 2FA on and off
- View and manage which external apps have been authorized to access what personal data
- View trusted devices   

Casa provides a platform for people to perform these account security functions and more. 

## Two-factor authentication

The core use case for Casa is self-service 2FA. If people need to call the helpdesk every time they get a new phone or security key, supporting strong authentication becomes prohibitively expensive. 

Out-of-the-box, Casa can be used to enroll and manage the following authenticators:    

- U2F security keys like [Yubikeys](https://www.yubico.com/products/yubikey-hardware/)       
- Gluu's U2F push-notification mobile app, [Super Gluu](https://super.gluu.org)    
- OTP hardware cards like [these](https://www.ftsafe.com/products/OTP/Display_Card) or dongles like [these](https://www.ftsafe.com/Products/OTP/Single_Button_OTP)      
- OTP mobile apps like Google Authenticator, FreeOTP, etc.       
- Mobile phone numbers able to receive OTPs via SMS   
- Passwords (if stored in the corresponding Gluu Server's local LDAP, i.e. not a backend LDAP like AD)      

Additional authenticators and use cases can be supported via [custom plugins](#plugin-oriented). 

## 2FA enrollment APIs

To facilitate 2FA device enrollment during account registration, or elsewhere in an application ecosystem, Casa exposes APIs for enrolling the following types of authenticators:   

- Phone numbers for SMS OTP   
- OTP apps, cards or dongles        
- Super Gluu Android and iOS devices        

Learn more in the [developer guide](./developer/index.md#apis-for-credential-enrollment).  

## Plugin oriented

Casa is a plugin-oriented, Java web application. Existing functionality can be extended and new functionality and APIs can be introduced through plugins. 

Learn more in the [developer guide](./developer/index.md).

## Existing plugins
Gluu has written a number of plugins to extend Casa, including plugins for:

- [Consent management](./plugins/consent-management.md) 
- [Custom branding](./plugins/custom-branding.md)  
- [2FA settings](./plugins/2fa-settings.md)  
- Account linking (*coming soon!*)   
- Developer portal (*coming soon!*)     

For more information visit the [Casa website](https://casa.gluu.org/plugins). 

## Gluu Server integration

Casa is tightly bundled with the [Gluu Server](https://gluu.org/docs/ce) identity and access management (IAM) platform. A few important notes:

- **Same host**: Casa must be installed on the same server (host) as its corresponding Gluu Server. For example, if the Gluu Server is deployed on `https://accounts.mydomain.com` , Casa should reside on the same host, for instance at `https://accounts.mydomain.com/signinoptions` 

- **Authentication scripts**: The Gluu Server relies on "interception scripts" to implement user authentication. Casa itself has an interecption script which defines authentication logic and routes authentications to specific 2FA mechanisms which also have their own scripts. All scripts must be enabled in the Gluu Server.        

- **oxd**: Casa uses the [oxd OAuth 2.0 client software](https://oxd.gluu.org) to leverage the Gluu Server for authentication. oxd can be deployed during Casa installation.  

More detailed information is available in the Admin Guide, linked [below](#admin-guide).

## User roles

There are two types of users in Gluu Casa:

- **Admin users**: Any user in the `Managers Group` in the Gluu Server   

- **Regular users**: Any user in the Gluu Server  

Admin users have access to the Casa [admin console](./administration/admin-console.md). All users can manage their 2FA credentials, as outlined in the [user guide](./user-guide.md).  

## Get started

Use the following links to get started with Casa:  

### Admin Guide

  - [Installation](./administration/installation.md)
  - [Admin console](./administration/admin-console.md)
  - [Credentials storage](./administration/credentials-stored.md)        
  - [Custom branding](./administration/custom-branding.md)        
  - [FAQs](./administration/faq.md)            

### User Guide

- [Home](./user-guide.md)

### Developer Guide

- [Home](./developer/index.md)

## License
Gluu Casa is made available under the [Gluu License Agreement for Gluu Casa](https://github.com/GluuFederation/casa/blob/master/LICENSE.md). 

