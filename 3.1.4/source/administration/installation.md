# Installation

## Requirements
    
- A working Gluu Server 3.1.4 installation with at least the following components installed: Apache, LDAP, oxAuth, and oxTrust. Add at least  **1GB of additional RAM** to the pre-existing [Gluu system requirements](https://gluu.org/docs/ce/3.1.4/installation-guide/#system-requirements).  

- Ensure dynamic client registration is enabled. In oxTrust go to `Configuration` > `JSON Configuration` > `oxAuth configuration`, property `dynamicRegistrationEnabled` should be set to true.

!!! Note  
    You can turn dynamic enrollment off after Casa installation, as needed. 

- An active [oxd 3.1.4](https://gluu.org/docs/oxd/3.1.4) installation. The interactive setup script will prompt you to install oxd in case you don't already have an instance available. 

- Casa must be installed in the same host as your Gluu Server

!!! Note
    If your Gluu Server 3.1.4 was upgraded from 2.4.4, ensure the `uma_protection` scope is allowed for dynamic registration in oxTrust.
    
## Installation via Linux Packages 

Casa is distributed as part of the Gluu Server extensions bundle. Follow the instructions according to your underlying OS.

!!! Warning 
    If you have logged into the Gluu chroot in any console terminal, log out before proceeding.

### Ubuntu 14.04 (trusty)
    
| Command Description                   |               Trusty Commands         |
|---------------------------------------|---------------------------------------|
| Add Gluu Repository | `# echo "deb https://repo.gluu.org/ubuntu/ trusty main" > /etc/apt/sources.list.d/gluu-repo.list` |
| Add Gluu GPG Key                      | `# curl https://repo.gluu.org/ubuntu/gluu-apt.key | apt-key add -` |
| Update/Clean Repo                     | `# apt-get update`                    |
| Install Gluu Server extension pack    | `# apt-get install gluu-casa-3.1.4` |
 
### Ubuntu 16.04 (xenial)
      
|  Command Description    |               Xenial Commands         |
|-------------------------|---------------------------------------|
| Add Gluu Repository     | `# echo "deb https://repo.gluu.org/ubuntu/ xenial main" > /etc/apt/sources.list.d/gluu-repo.list` |
| Add Gluu GPG Key        | `# curl https://repo.gluu.org/ubuntu/gluu-apt.key | apt-key add -` |
| Update/Clean Repo       | `# apt-get update`                         |
| Install Gluu Server extension pack     | `# apt-get install gluu-casa-3.1.4`      |
 
### CentOS 6
      
| Command Description     |               CentOS 6.x              |
|-------------------------|---------------------------------------|
| Add Gluu Repository     | `# wget https://repo.gluu.org/centos/Gluu-centos6.repo -O /etc/yum.repos.d/Gluu.repo`|
| Add Gluu GPG Key        | `# wget https://repo.gluu.org/centos/RPM-GPG-KEY-GLUU -O /etc/pki/rpm-gpg/RPM-GPG-KEY-GLUU`|
| Import GPG Key          | `# rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-GLUU`|
| Update/Clean Repo       | `# yum clean all`                          |
| Install Gluu Server extension pack    | `# yum install gluu-casa-3.1.4`          |

### CentOS 7
     
| Command Description     |               CentOS 7.2              |
|-------------------------|---------------------------------------|
| Add Gluu Repository     | `# wget https://repo.gluu.org/centos/Gluu-centos7.repo -O /etc/yum.repos.d/Gluu.repo` |
| Add Gluu GPG Key        | `# wget https://repo.gluu.org/centos/RPM-GPG-KEY-GLUU -O /etc/pki/rpm-gpg/RPM-GPG-KEY-GLUU`|
| Import GPG Key          | `# rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-GLUU` |
| Update/Clean Repo       | `# yum clean all`                          |
| Install Gluu Server extension pack     | `# yum install gluu-casa-3.1.4`          |

### RHEL 6
     
| Command Description     |               RHEL 6.x              |
|-------------------------------|---------------------------------------|
| Add Gluu Repository     | `# wget https://repo.gluu.org/rhel/Gluu-rhel6.repo -O /etc/yum.repos.d/Gluu.repo` |
| Add Gluu GPG Key        | `# wget https://repo.gluu.org/centos/RPM-GPG-KEY-GLUU -O /etc/pki/rpm-gpg/RPM-GPG-KEY-GLUU`|
| Import GPG Key          | `# rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-GLUU` |
| Update/Clean Repo       | `# yum clean all`                          |
| Install Gluu Server extension pack     | `# yum install gluu-casa-3.1.4`          |

### RHEL 7
     
| Command Description     |               RHEL 7                  |
|-------------------------|---------------------------------------|
| Add Gluu Repository     | `# wget https://repo.gluu.org/rhel/Gluu-rhel7.repo -O /etc/yum.repos.d/Gluu.repo` |
| Add Gluu GPG Key        | `# wget https://repo.gluu.org/rhel/RPM-GPG-KEY-GLUU -O /etc/pki/rpm-gpg/RPM-GPG-KEY-GLUU`|
| Import GPG Key          | `# rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-GLUU` |
| Update/Clean Repo       | `# yum clean all`                          |
| Install Gluu Server extension pack     | `# yum install gluu-casa-3.1.4`          |

### Debian 8 (Jessie)

| Command Description     |               Jessie Commands         |
|-------------------------|---------------------------------------|
| Add Gluu Repository     | `# echo "deb https://repo.gluu.org/debian/ stable main" > /etc/apt/sources.list.d/gluu-repo.list`|
| Add Gluu GPG Key        | `# curl https://repo.gluu.org/debian/gluu-apt.key | apt-key add -` |
| Update/Clean Repo       | `# apt-get update`                         |
| Install Gluu Server extension pack     | `# apt-get install gluu-casa-3.1.4`      |

    
## Run the Setup Script

The Casa setup script, `setup_casa.py`, adds the application to Gluu Server, imports required data to LDAP, and applies a number of required configurations in Gluu Server chroot.

Log in to the Gluu Server chroot, as follows:

`$ service gluu-server-3.1.4 login`

Then `cd` to the setup scripts directory and run `setup_casa.py`: 

```
# cd /install/community-edition-setup
# ./setup_casa.py
```

Answer the setup questions as prompted. Hit Enter to accept the default value specified in square brackets, if appropriate. 

### Finish setup
After answering the setup script questions, the selections will be displayed with a prompt to finish installation. If everything looks good, hit Y to finish.

Upon successful installation, a confirmation message will appear that says: "Casa installation successful! Point your browser to `https://<host>/casa`".

Wait for one minute, then visit the URL and authenticate against Gluu to access Casa. 

!!! Note 
    To change the default URL path for Casa follow the steps listed [here](change-context-path.md). However, it is advisable to apply this customization **before** credentials are enrolled. 
   
