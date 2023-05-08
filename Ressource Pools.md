Two reasons why they introduced SCOM Ressource Pools

	- Remove the single Point of Failure
	- Provide a mechanism for high availability of agentless/remote workflows

Primary "role" components

Members	Observers	Default Observers

is set to "Enabled" or "Disabled" for every Pool. Normally it is set to "enabled" by default for every Pool. Is it set to "disalbled" by default, using the New-ResourcePool Command via PowerShell


The reason: 
		To allow for a pool to have high availability when you have two management servers in a pool
Are Management Servers of Gateway Servers	"observers-only roles". Management Server or Gateway Server , that do NOT participate in lodading Workflows. They are only introduced into particitape in quorum desicions	

A pool requires ONE more members

A pool requires Three (quorum voting) members to estabish high availability
	
- The reason we need THREE (quorum voting) members (not two) for high availability is because of the quorum algorithm

"Scenarios"

Single Management Server in Pool	Two Management Server in Pool	Three Management Server in Pool	Four Management Server in Pool	Five or more management Server in Pool
- Default observer is enabledb by default	- Default observer is enabled by default	- Default Observer is enabled by default	- Default Observer is enabled by default	- Default Observer is enabled by default
- No high availability for the Pool	- Three voting members - high availability	- Four voiting members - high availability	- Five voiting members - high availability ( 4MS + Default Observer)	- 6 voiting members - high availability (5 MS+ Default Observer)
- Single point of failure	- If disable the default observer - lose high availabilty	- Only ONE Management Server can go down (greater than 50% Rule)	- TWO Management Server can go down (greater than 50% Rule)	- TWO management Server can go down ( greater than 50% Role)
- Default server - no benefit				

"Gateways as Ressource Pool Members"
Single Gateway Server in Pool	Two Gateway Server in Pool 	Three Gateway server in Pool
- Default Observer is enabled	- Default Observer is enabled by default	- Default Observer is enabled by default
- No high availability - Gateway Server is a single point of failure	- No high availability - only TWO members of this pool	- Three voiting members (3 GW`S)- high availability
- Default Observer should not be used, because Gateways do not have local SDK Service 	- Only availability - 3 GW`S in Ressource Pool	- ONE Gateway Server can go down (50% Rule)
	- Default Oberserver should not be used, because GW do not habe local SDK Servcice	- Default Observer should not be used, because GW do not have local SDK Service


