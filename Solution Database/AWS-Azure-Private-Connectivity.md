# Private Connectivity Considerations for Azure and AWS

Both public cloud providers AWS and Azure provide customers the ability to access their services via private connections. The point discussed at GroupSolve was design considerations for accessing public endpoints, specifically the misconception that these public sub-interfaces provide truly private connection. 

There are two distinct types of connections that can be setup over DirectConnect (AWS) and XpressRoute (Azure), public and private. Private focuses on providing the ability to establish a virtual layer 2 or 3 connection to virtual private networks in the associated cloud subscriptions. In other words, private connections let organizations connect to virtualized data centers in Azure and AWS via standard private connectivity options (L2 handoff and/or MPLS). 

For organizations moving critical workloads that have latency concerns or data security concerns to these provides from existing data centers, private connections are proffered over P2P iPSEC VPN tunnels in most circumstances as they offer higher stability and bandwidth. 

Where the misconceptions arise is when we apply similar assumptions to public connections. Both DirectConnect and XpressRoute provide the ability to connect to their public IP address spaces over these connections. Once configured organizations redistribute all public IP subnets associated with a given region of the public cloud provider and route these redistributed public subnets over the private connections. However, this is where major consideration needs to be taken for where the virtual interface is created in the organization’s network. If it is created inside the DMZ the flow of data for any endpoint hosted on these public addresses will now flow round the DMZ and directly out the private connection creating a potential issue for organizations who have specific perimeter scanning and security tools. This presents a substantial perimeter security hole if configured improperly. 

The main benefit to public peering is consistent network performance. Many organizations tend to assume that these public peering connections provide “more secure” connection to public services but instead they should be viewed similarly to normal internet connections and the same controls should be applied. 

## Info from AWS and Azure:

* https://aws.amazon.com/premiumsupport/knowledge-center/direct-connect-types/
* https://docs.microsoft.com/en-us/azure/expressroute/expressroute-circuit-peerings

### AWS Direct Connect, Public Virtual Interface: 

“To connect to AWS public endpoints (for example, Amazon EC2 or Amazon S3) with dedicated network performance, use a public virtual interface.
A public virtual interface allows you to connect to all AWS public IP spaces for your respective region. AWS Direct Connect is a regional service with the exception that in North America, you can reach Amazon public services in other North America regions. For a list of AWS public IP ranges available by region for the public virtual interface, see AWS IP Address Ranges.”

### Azure XpressRoute, Public Peering:

*“Services such as Azure Storage, SQL databases, and Websites are offered on public IP addresses. You can privately connect to services hosted on public IP addresses, including VIPs of your cloud services, through the public peering routing domain. You can connect the public peering domain to your DMZ and connect to all Azure services on their public IP addresses from your WAN without having to connect through the internet.

Connectivity is always initiated from your WAN to Microsoft Azure services. Microsoft Azure services will not be able to initiate connections into your network through this routing domain. Once public peering is enabled, you will be able to connect to all Azure services. We do not allow you to selectively pick services for which we advertise routes to. You can review the list of prefixes we advertise to you through this peering on the Microsoft Azure Datacenter IP Ranges page. The page is updated weekly.”*
