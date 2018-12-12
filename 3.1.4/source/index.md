# Gluu Casa 3.1.4 Documentation

## Overview

Gluu Casa ("Casa") is a user-facing application people can use to enroll, delete and manage their strong credentials in the [Gluu Server](https://gluu.org).

Out-of-the-box, Casa can be used to manage the following types of free or low-cost authentication mechanisms:    

- U2F security keys (like [Yubikeys](https://www.yubico.com/products/yubikey-hardware/))    
- Gluu's free and secure U2F mobile app, [Super Gluu](https://super.gluu.org)   
- OTP mobile apps (like Google Authenticator, FreeOTP, etc.)    
- Mobile phone numbers that can receive OTPs via SMS  
- Passwords (only if stored in the corresponding Gluu Server's local LDAP. Not supported if the passwords are stored in a backend LDAP like AD)      
  
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
Gluu Casa is licensed under the free open source [MIT License](https://github.com/GluuFederation/casa/blob/master/LICENSE). 

