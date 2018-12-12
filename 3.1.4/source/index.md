# Gluu Casa 3.1.4 Documentation

## Overview

Gluu Casa ("Casa") is a user-facing web application people can use to self-service specific personal data residing in the [Gluu Server](https://gluu.org/docs/ce) authentication and authorization system. 

For instance, you may want to give people the ability to do things like:

- Enroll, delete and manage their 2FA credentials, e.g. U2F keys, mobile apps, phone numbers and more;
- Turn 2FA on and off
- View and manage which apps have been authorized to access their personal data

Casa provides a web portal for people to perform these functions and more. 

## Plugin Oriented

Casa is a plugin-oriented, java web application. Existing functionality can be extended, and new functionality and APIs can be introduced through plugins. 

## Two-factor authentication

The core use case for Casa is self-service management of two-factor authentication credentials. If people need to call the IT helpdesk every time they get a new phone or security key, rolling out strong authentication becomes prohibitively expensive. 

Out-of-the-box, Casa can be used to manage the following types of free or low-cost authentication mechanisms:    

- U2F security keys (like [Yubikeys](https://www.yubico.com/products/yubikey-hardware/))    
- Gluu's free and secure U2F mobile app, [Super Gluu](https://super.gluu.org)   
- OTP mobile apps (like Google Authenticator, FreeOTP, etc.)    
- Mobile phone numbers that can receive OTPs via SMS  
- Passwords (only if stored in the corresponding Gluu Server's local LDAP. Not supported if the passwords are stored in a backend LDAP like AD)      


### Enrollment APIs

Casa offers APIs for enrolling phone numbers, OTP apps, and Super Gluu devices. The APIs can be handy for embedding strong credential enrollment into account registration processes, or elsewhere in an application ecosystem where it might be preferable to enroll strong credentials. 

## Other use cases

As a user-facing portal, Casa is an ideal place to offer self-service functionalities for other AA-specific action items. In addition to authentication, Casa is a good place to offer people the ability to perform:

- Account linking
- Request client IDs and secret for application development
- Request elevated scopes

These are just a few places where Casa can be useful. 

## Gluu Server Integration
Casa is tightly coupled with the [Gluu Server](https://gluu.org/docs/ce) authentication and authorization platform. A few important notes:

- **Same host**: By default, Casa must be installed on the same server (host) as a Gluu Server. 

- **Authentication scripts**: Gluu leverages "interception scripts" to implement user authentication. For each type of 2FA credential that should be manageable in Casa (e.g. U2F keys, OTP apps, etc.), the corresponding authentication script **must be** enabled in Gluu. Learn more about how authentication happens in the [Gluu documentation](https://gluu.org/docs/ce/authn-guide/intro/).  

- **oxd**: Casa leverages Gluu's OAuth 2.0 client software, [oxd](https://oxd.gluu.org), to integrate with the Gluu Server. Casa can leverage an existing oxd server, or a new instance of oxd can be deployed during [Gluu Casa installation](./administration/installation.md). 

## User Roles

There are two types of users in Gluu Casa:

- **Admin users**: Any user in the `Managers Group` in the Gluu Server. 

- **Regular users**: Any user in the Gluu Server. 

Admin users have access to the Casa [admin console](./administration/admin-console.md). All users can manage their 2FA credentials in Casa. 

## Get Started

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
Gluu Casa is licensed under the commercial [Gluu License Agreement for Gluu Casa](https://github.com/GluuFederation/casa/blob/master/LICENSE.md). 

