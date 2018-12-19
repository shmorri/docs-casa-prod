# Gluu Casa 3.1.4 Documentation

## Overview

Gluu Casa ("Casa") is a self-service web portal for people to manage their authentication and authorization data in an organization's [Gluu Server](https://gluu.org/docs/ce). 

For example, people may need to:

- Enroll, delete and manage their two-factor authentication (2FA) credentials (e.g. U2F keys, mobile apps, phone numbers)
- Turn 2FA on and off
- View and manage which apps are authorized to access what personal data
- View trusted devices   

Casa provides a web portal for people to perform these functions and more. 

## Two-factor authentication

The core use case for Casa is self-service 2FA. If people need to call the helpdesk every time they get a new phone or security key, supporting strong authentication becomes prohibitively expensive. 

Out-of-the-box, Casa can be used to enroll and manage the following types of authenticators:    

- U2F security keys like [Yubikeys](https://www.yubico.com/products/yubikey-hardware/)       
- Gluu's U2F push-notification mobile app, [Super Gluu](https://super.gluu.org)    
- OTP hardware cards like [these](https://www.ftsafe.com/products/OTP/Display_Card)    
- OTP mobile apps like Google Authenticator, FreeOTP, etc.       
- Mobile phone numbers able to receive OTPs via SMS   
- Passwords (if stored in the corresponding Gluu Server's local LDAP, i.e. not a backend LDAP like AD)      

Additional authenticators and use cases can be supported via [custom plugins](#plugin-oriented). 

### Enrollment APIs

Casa offers APIs for enrolling the following authenticators: 

- Phone numbers   
- OTP apps
- OTP cards       
- Super Gluu devices     

APIs can be leveraged to build strong credential enrollment into an account registration process or elsewhere in an application ecosystem. Learn more in the [developer guide](./developer/index.md#apis-for-credential-enrollment).  

## Plugin oriented

Casa is a plugin-oriented, Java web application. Existing functionality can be extended and new functionality and APIs can be introduced through plugins. Learn more in the [developer guide](./developer/index.md).

### Existing plugins
Gluu has written a number of plugins to extend Casa, including plugins for:

- Consent management 
- Custom branding  
- 2FA settings  
- Account linking (*coming soon!*)   
- Developer portal (*coming soon!*)     

For a more information about the existing plugins, visit the [Casa website](https://casa.gluu.org/plugins). 

## Gluu Server integration

Casa is tightly coupled with the [Gluu Server](https://gluu.org/docs/ce). A few important notes:

- **Same host**: Casa must be installed on the same server (host) as its corresponding Gluu Server. For example, if the Gluu Server is deployed on `https://accounts.mydomain.com` , Casa should reside on the same host, for instance at `https://accounts.mydomain.com/signinoptions` 

- **Authentication scripts**: The Gluu Server leverages "interception scripts" to implement the user authentication process. For each type of authenticator that is manageable in Casa (e.g. U2F keys, OTP apps, etc.), its corresponding authentication script **must be** enabled in Gluu  

- **oxd**: Casa uses the [oxd](https://oxd.gluu.org) OAuth 2.0 client software to leverage the Gluu Server for authentication. Casa can use an existing oxd server, or a new instance of oxd can be deployed during [Gluu Casa installation](./administration/installation.md)  

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
Gluu Casa is made available under the commercial [Gluu License Agreement for Gluu Casa](https://github.com/GluuFederation/casa/blob/master/LICENSE.md). 

