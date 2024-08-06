### What is EtherChannel:

EtherChannel is a protocol that creates a virtual port grouping physical links into one logical connection between two networking devices in Layer2 and Layer3 

EtherChannel has 3 Protocol modes which are LACP,PAgP and Static
	-LACP mode could be : ACTIVE or PASSIVE
	-PAgp mode could be : Decirable or auto
	-Static mode        : On
  
### Why do we need EtherChannel:

a. EtherChannel tend to solve some spanning-tree complications
b. Make management more easier
c. Load balancing  
d. It improves bandwidth speed 
e. Avoids link redundancy as it effectively uses all links in the channel

### Where is it used:

It's is used in switches and routers i.e Layer 2 and 3 connections. 

### How is it configured:
	- int port-channel 'number'
		>>creates an etherchannel
	- channel-group 'number' mode {dedirable | auto | active | passive} 
		>>configures an interface to be part of an etherchannel
	- port-channel load-balance {scr-dst-ip| src-dst-mac}
		>>configures the load balance method

	##### Verification commands:
		- show etherchannel summary
		- show etherchannel  load-balance 
