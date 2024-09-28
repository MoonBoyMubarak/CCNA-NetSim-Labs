# NAT (Network Address Translation)
Network Address Translation (NAT) is a protocol that translates private IPv4 addresses into public IPv4 addresses, enabling devices on a private network to communicate with the internet.

### Types of NAT:
**Static NAT**: A one-to-one mapping between a private (local) IP address and a public (global) IP address.

**Dynamic NAT**: Maps private IP addresses to a pool of public IP addresses.

### Lab Overview:
In this lab, I configured Static NAT, which involves setting up NAT interfaces for hosts based on their location. The two location perspectives are:

- **Inside** (the internal network)
  - config command:
    - R1 (config-if)# ip nat inside
- **Outside** (the external network, usually the internet)
  - config command:
    - R1 (config-if)# ip nat outside
  
  Each host is assigned a Global NAT IP, where its private IP is referred to as local.

### Key Terms:
- **Inside Local**: The private IPv4 address of the source host before NAT.
- **Inside Global**: The public IPv4 address of the source host after NAT.
- **Outside Local**: The public IPv4 address of the destination host before NAT.
- **Outside Global**: The public IPv4 address of the destination host after NAT.

### Troubleshooting commands
- **show ip nat translations**: Displays the current NAT translations.
- **show ip nat statistics**: Displays NAT statistics, including the number of active translations, hits, and misses. 
- **clear ip nat translation***:Clears specific or all NAT translations from the NAT table, resetting NAT mappings.
- **debug ip nat**: Displays NAT debug information.

*****

##### Kindly refer to the configuration file for Router R1 for more configuration command details.  More notes comming up as I proceed.

Thanks.