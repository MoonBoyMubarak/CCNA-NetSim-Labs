# NAT (Network Address Translation)
Network Address Translation (NAT) is a protocol that translates private IPv4 addresses into public IPv4 addresses, enabling devices on a private network to communicate with the internet.

### Types of NAT:
**Static NAT**: A one-to-one mapping between a private (local) IP address and a public (global) IP address.

**Dynamic NAT**: Maps private IP addresses to a pool of public IP addresses.

**Port Address Translation (PAT) / NAT Overload**: PAT allows multiple devices on a private network to share a single public IP by assigning unique port numbers to each connection. It can use the router's public IP or another public IP, making efficient use of limited IPs.

*****
### Lab Overview:
In this exercise, I configured and tested Static NAT, Dynamic NAT, and PAT on R1. 

Static NAT config:
1. Attempt to ping from PC1 to 8.8.8.8.  Does the ping work?

2. Configure static NAT on R1.
  - Configure the appropriate inside/outside interfaces
    - R1(config)# interface GigabitEthernet0/1
    - R1(config-if)# ip nat inside
    - R1(config-if)# exit

    - R1(config)# interface GigabitEthernet0/0
    - R1(config-if)# ip nat outside
    - R1(config-if)# exit


- Map the IP addresses of PC1, PC2, and PC3 to 100.0.0.x/24
  - R1(config)# ip nat inside source static 172.16.0.1 100.0.0.1
  - R1(config)# ip nat inside source static 172.16.0.2 100.0.0.2
  - R1(config)# ip nat inside source static 172.16.0.2 100.0.0.3


3. Ping 8.8.8.8 from PC1 again.  Does the ping work?

4. Ping google.com from each PC, and then check the NAT translations on R1.

5. Clear the NAT translations on R1.  Which entries remain?




  Dynamic NAT & PAT Lab config:
1. Configure dynamic NAT on R1.
  - Configure the appropriate inside/outside interfaces:
    - R1(config)# interface GigabitEthernet0/1
    - R1(config-if)# ip nat inside
    - R1(config-if)# exit

    - R1(config)# interface GigabitEthernet0/0
    - R1(config-if)# ip nat outside
    - R1(config-if)# exit

  - Translate all traffic from 172.16.0.0/24:
    - R1(config)# access-list 1 permit 172.16.0.0 0.0.0.255 

  - Create a pool of 100.0.0.1 to 100.0.0.2 from the 100.0.0.0/24 subnet:
    - R1(config)# ip nat pool POOL1 100.0.0.1 100.0.0.2 netmask 255.255.255.0  
    - R1(config)# ip nat inside source list 1 pool POOL1


2. Ping google.com from PC1 and PC2.  Then, ping it from PC3.  
    What happens to PC3's ping?

3. Clear the NAT translations and remove the current NAT configuration.
    - R1# clear ip nat translation *
    - R1(config)# no ip nat inside source list 1 pool POOL1
    - R1(config)# no ip nat pool POOL1
    - R1(config)# no access-list 1
  - Switch the configuration to PAT using R1's public IP address:
    - R1(config)# access-list 1 permit 172.16.0.0 0.0.0.255
    - R1(config)# ip nat inside source list 1 interface GigabitEthernet0/0 overload



4. Ping google.com from each PC.  Do the pings work?
  - Examine the NAT translations on R1:
      - R1# show ip nat translations
  

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

##### Refer to the relevant config files for the complete configuration. Let me know if you need further clarification or details. Thanks! 