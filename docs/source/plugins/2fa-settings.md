# Strong Authentication Settings Plugin

This plugin allows administrators to configure how and when 2FA is applied. Admins can:

- Specify the minimum number of credentials users must enroll before they are able to turn on 2FA

- Choose from a set of predefined policies for when 2FA should be prompted:
 
    - Always (at every login attempt)
    - When user's location is unrecognized
    - When user's device is unrecognized
    - Users can define their own policy (based on the above)
  
- Set how long a location or device can be deemed as recognized
    
Additionally, when administrators allow users to set their own strong authentication policy, users can:

- View the list of physical devices they have used to login (e.g. PC, tablet, phone)
- View the time and location (city) associated to the last login event
- Remove a device from the list (eg. when it should not be considered trustworthy anymore)

A device/location is considered trustworthy when the user has presented a strong credential in order to login to Casa with it. Subsequent login attempts from trustworthy (recognized) device/locations will not require them to present a second factor.

## Requirements

- Plugin jar file must match the version of your Casa (and Gluu Server) installation.

    
## Installation

1. Login to Casa using an administrator account

1. Visit `Administration console` > `Casa plugins`

1. Click on `Add a plugin...` and select the plugin jar file

1. Click on `Add` 

## How to use

For administrators, a new link labeled "2FA settings" appears in the dashboard menu to access the functionalities.

For regular users, proper details appear in the widget where preferred authentication mechanism is set. These will be visible only if an option other than "password only" has been selected.
