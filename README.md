#Readme

This ansible role deploys xl2tpd over IPsec (client) for Ubuntu 12.04 (tested on vagrant)

##Prerequisite
* Having ansible installed on your workstation. 
* A host or node to deploy the vpn client on
* VPN Server (tested with openswan)

##How to install
* Use github to clone/fork in your role directory
* ansible galaxy ```ansible-galaxy install adham.helal.ansible-l2tp_ipsec ```

##Variables 
  All the default variables are located **defaults/main.yml**. Mostly you would need to configure the following variables. 

  - *vpn_server:* The vpn server hostname or IP (required)

    ```vpn_server : vpn.example.com```

  - *vpn_PSK:* vpn Pre-shared key (required)

    ```vpn_PSK : "shared_key"```
  
  - *vpn_username:* vpn user name (required)

    ```vpn_username : "username"```
    
  - *vpn_password:* vpn password (required)

    ```vpn_password : "password"```  
    
  - *vpn_routing:* You can define one or more subnets and gateway
 
      ```
     vpn_routing:
     - subnet   : "10.224.24.00/22"
       gateway  : "10.55.55.4"
     - subnet   : "192.168.55.0/32"
       gateway  : "10.55.55.4"
      ```
##Configure
You can configure your variables in ansible with one of the following

 * Create a variable in host/group variables directory. (recommended)
 * Editing var/main.yml
 * Run ansible-playbook with -e
 * Edit the default/main.yml (not recommended)

##Run
**By default the vpn will fail because the configuration uses a bogus vpn server you need to use a valid vpn server**
    
  ```ansible-playbook -l hostname l2to_ipsec.yml```

##Test
 1. you should have a ppp0 if you type ```ip addr show```
 2. you should be able to ping your vpn gateway 

##Possible issues
I have not tested the playbook long enough to check for timeouts but vpn will probably break after a while. 
