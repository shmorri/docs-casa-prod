# Credential Manager 3.1.3 Documentation

## Overview

Credential Manager is a simple, user-facing application people can use to enroll, delete and manage their strong credentials in the [Gluu Server](https://gluu.org).

Out-of-the-box Credential Manager supports the following free or low-cost authentication mechanisms:    

- U2F security keys (like [Yubikeys](https://www.yubico.com/products/yubikey-hardware/))    
- Gluu's free and secure U2F mobile app, [Super Gluu](https://super.gluu.org)   
- OTP mobile apps (like Google Authenticator, FreeOTP, etc.)    
- Mobile phone numbers that can receive OTPs via SMS  
- Passwords (only if stored in the corresponding Gluu Server's local LDAP. Not supported if the passwords are stored in a backend LDAP like AD)      
  
## Gluu Server Integration
Credential Manager is tightly coupled with the [Gluu Server](https://gluu.org/docs/ce) authentication and authorization platform. A few important notes:

- **Same host**: By default, Credential Manager must be installed on the same server (host) as a Gluu Server. 

- **Authentication scripts**: Gluu leverages "interception scripts" to implement user authentication. For each type of 2FA credential that should be manageable in Cred Manager (e.g. U2F keys, OTP apps, etc.), the corresponding authentication script **must be** enabled in Gluu. Learn more about how authentication happens in the [Gluu documentation](https://gluu.org/docs/ce/authn-guide/intro/).  

- **oxd**: Cred Manager leverages Gluu's OAuth 2.0 client software, [oxd](https://oxd.gluu.org), to integrate with the Gluu Server. Credential Manager can leverage an existing oxd server, or a new instance of oxd can be deployed during [Credential Manager installation](./administration/installation.md). 

## User Roles

There are two types of users in Credential Manager:

- **Admin users**: Any user in the `Managers Group` in the Gluu Server. 

- **Regular users**: Any user in the Gluu Server. 

Admin users have access to the Cred Manager [admin console](./administration/admin-console.md). All users can manage their 2FA credentials in Credential Manager. 

## Get Started

Use the following links to get started with credential manager:  

### Admin Guide

  - [Installation](./administration/installation.md)
  - [Admin console](./administration/admin-console.md)
  - [Credentials storage](./administration/credentials-stored.md)        
  - [Custom branding](./administration/custom-branding.md)        
  - [FAQs](./administration/faq.md)            

### User Guide

- [Home](./user-guide.md)

### Developer Guide

- [Home](./developer-guide.md)


## License
Credential Manager is licensed under the free open source [MIT License](https://github.com/GluuFederation/cred-manager/blob/master/LICENSE). 

