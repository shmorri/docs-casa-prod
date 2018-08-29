# Installation

## Requirements
    
1. A working Gluu Server installation (version 3.1.4), with at least the following components installed: Apache, LDAP, oxAuth, and oxTrust. [Install Gluu](https://gluu.org/docs/ce/installation-guide/).  

1. An active [oxd](https://gluu.org/docs/oxd) installation, version 3.1.2 or higher. If you don't already have an oxd server available, the interactive setup script will prompt you to install oxd inside your Gluu Server container. 

1. Credential Manager must be installed in the same host as your Gluu Server

!!! Note
    If your Gluu Server 3.1.4 was upgraded from 2.4.4, ensure the `uma_protection` scope is allowed for dynamic registration in oxTrust.
    
## Installation via Linux Packages 

Credential Manager is distributed as part of the Gluu Server extensions bundle. Follow the instructions according to your underlying OS.

!!! Warning 
    If you have logged into the Gluu chroot in any console terminal, log out before proceeding.

### Ubuntu 14.04 (trusty)
    
| Command Description                   |               Trusty Commands         |
|---------------------------------------|---------------------------------------|
| Add Gluu Repository | `# echo "deb https://repo.gluu.org/ubuntu/ trusty main" > /etc/apt/sources.list.d/gluu-repo.list` |
| Add Gluu GPG Key                      | `# curl https://repo.gluu.org/ubuntu/gluu-apt.key | apt-key add -` |
| Update/Clean Repo                     | `# apt-get update`                    |
| Install Gluu Server extension pack    | `# apt-get install gluu-server-ext-3.1.4` |
 
### Ubuntu 16.04 (xenial)
      
|  Command Description    |               Xenial Commands         |
|-------------------------|---------------------------------------|
| Add Gluu Repository     | `# echo "deb https://repo.gluu.org/ubuntu/ xenial main" > /etc/apt/sources.list.d/gluu-repo.list` |
| Add Gluu GPG Key        | `# curl https://repo.gluu.org/ubuntu/gluu-apt.key | apt-key add -` |
| Update/Clean Repo       | `# apt-get update`                         |
| Install Gluu Server extension pack     | `# apt-get install gluu-server-ext-3.1.4`      |
 
### CentOS 6
      
| Command Description     |               CentOS 6.x              |
|-------------------------|---------------------------------------|
| Add Gluu Repository     | `# wget https://repo.gluu.org/centos/Gluu-centos6.repo -O /etc/yum.repos.d/Gluu.repo`|
| Add Gluu GPG Key        | `# wget https://repo.gluu.org/centos/RPM-GPG-KEY-GLUU -O /etc/pki/rpm-gpg/RPM-GPG-KEY-GLUU`|
| Import GPG Key          | `# rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-GLUU`|
| Update/Clean Repo       | `# yum clean all`                          |
| Install Gluu Server extension pack    | `# yum install gluu-server-ext-3.1.4`          |

### CentOS 7
     
| Command Description     |               CentOS 7.2              |
|-------------------------|---------------------------------------|
| Add Gluu Repository     | `# wget https://repo.gluu.org/centos/Gluu-centos7.repo -O /etc/yum.repos.d/Gluu.repo` |
| Add Gluu GPG Key        | `# wget https://repo.gluu.org/centos/RPM-GPG-KEY-GLUU -O /etc/pki/rpm-gpg/RPM-GPG-KEY-GLUU`|
| Import GPG Key          | `# rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-GLUU` |
| Update/Clean Repo       | `# yum clean all`                          |
| Install Gluu Server extension pack     | `# yum install gluu-server-ext-3.1.4`          |

### RHEL 6
     
| Command Description     |               RHEL 6.x              |
|-------------------------------|---------------------------------------|
| Add Gluu Repository     | `# wget https://repo.gluu.org/rhel/Gluu-rhel6.repo -O /etc/yum.repos.d/Gluu.repo` |
| Add Gluu GPG Key        | `# wget https://repo.gluu.org/centos/RPM-GPG-KEY-GLUU -O /etc/pki/rpm-gpg/RPM-GPG-KEY-GLUU`|
| Import GPG Key          | `# rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-GLUU` |
| Update/Clean Repo       | `# yum clean all`                          |
| Install Gluu Server extension pack     | `# yum install gluu-server-ext-3.1.4`          |

### RHEL 7
     
| Command Description     |               RHEL 7                  |
|-------------------------|---------------------------------------|
| Add Gluu Repository     | `# wget https://repo.gluu.org/rhel/Gluu-rhel7.repo -O /etc/yum.repos.d/Gluu.repo` |
| Add Gluu GPG Key        | `# wget https://repo.gluu.org/rhel/RPM-GPG-KEY-GLUU -O /etc/pki/rpm-gpg/RPM-GPG-KEY-GLUU`|
| Import GPG Key          | `# rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-GLUU` |
| Update/Clean Repo       | `# yum clean all`                          |
| Install Gluu Server extension pack     | `# yum install gluu-server-ext-3.1.4`          |

### Debian 8 (Jessie)

| Command Description     |               Jessie Commands         |
|-------------------------|---------------------------------------|
| Add Gluu Repository     | `# echo "deb https://repo.gluu.org/debian/ stable main" > /etc/apt/sources.list.d/gluu-repo.list`|
| Add Gluu GPG Key        | `# curl https://repo.gluu.org/debian/gluu-apt.key | apt-key add -` |
| Update/Clean Repo       | `# apt-get update`                         |
| Install Gluu Server extension pack     | `# apt-get install gluu-server-ext-3.1.4`      |

    
## Run the Setup Script

The cred-manager setup script, `setup_cred_mgr.py`, adds the application to Gluu Server, imports required data to LDAP, and applies a number of required configurations in Gluu Server chroot.

Log in to the Gluu Server chroot, as follows:

`$ service gluu-server-3.1.4 login`

Then `cd` to the setup scripts directory and run `setup_cred_mgr.py`: 

```
# cd /install/community-edition-setup
# ./setup_cred_mgr.py
```

Answer the setup questions as prompted. Hit Enter to accept the default value specified in square brackets, if appropriate. 

### oxd Installation 
Credential Manager can use an existing oxd installation, or a new installation can be deployed during the interactive setup. If oxd is installed during setup, upon starting it will try to connect to Gluu's license server to validate the license info. Ensure the host has Internet connectivity at least for the first time oxd is started. 

!!! Note
    oxd is commercial software and requires a license to operate. Get a free license at [https://oxd.gluu.org](https://oxd.gluu.org).

### Finish setup
After answering the setup script questions, the selections will be displayed with a prompt to finish installation. If everything looks good, hit Y to finish.

Upon successful installation, a confirmation message will appear that says: "Credential Manager installation successful! Point your browser to `https://<host>/cred-manager`".

Wait for some 30 seconds, then visit the URL and authenticate against Gluu to access Credential Manager. If oxd license details were not added during setup, follow the instructions to [manually add an oxd license](./faq.md#adding-license-manually).

By default the application is accesible at URL path `/cred-manager`. If you want Credential Manager to use a different context path please follow the steps listed [here](change-context-path.md). It is advisable to apply this customization before any credential enrollments take place.
