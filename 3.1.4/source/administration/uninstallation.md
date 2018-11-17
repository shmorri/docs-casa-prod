# Uninstallation and clean up

To remove Casa from your Gluu installation do the following:

1. Stop casa service, e.g: 

    ```
    service gluu-server-3.1.4 login
    service casa stop    
    ```

1. Run the clean up utility. It will remove configurations added to your Gluu Server when Casa was installed as well as data not needed anylonger. In chroot run:

    For deb based systems:
    
    ```
    # cd /install/community-edition-setup/
    # apt update && apt install python-pip
    # pip install ldap3
    # ./casa_cleanup.py
    ```
    
    For rpm based systems:
    
    ```
    # cd /install/community-edition-setup/
    # yum install epel-release && yum install python-pip
    # pip install ldap3
    # ./casa_cleanup.py
    ```

1. Logout from chroot and remove package:

    For deb based systems:
    
    ```
    apt remove gluu-casa-3.1.4
    ```

    For rpm based systems:

    ```
    yum remove gluu-casa-3.1.4
    ```
    