# VPN

## Site-Site VPN

Connect on-premises hardware to a VPC. A hardware based, highly available VPN 
to allow you to connect your on-premises networks and your VPCs. (Look this up
for a better definition) dsds

Uses cases: 

### Facts

* Quick to set up, can only take minutes as opposed to DIrect connect which can
  take weeks/months.
* They are cheap for sporadic or low usage.
* Charge per hour for running an active and data charge (charge is higher than
  direct connect), so this is only economical when usage is going to be low.
* Performance is limited by customer gateway equipment.
* VPNs use encryption end-to-end, which means there is compute overhead that
  also affects performance and cost.
* Since it's over the internet, that also affects performance.

### VPN Routing Priority (how important is this for the exam?)
    
1. Local
2. Longest prefix “Destination” column name
3. Static
4. Direct Connect
5. Propagated (dynamic IP)
6. if 2 connections have an equal prefix, then static over dynamic.
7. Propagated Dynamic

## Direct Connect Architecture

Abbreviated as “DX”, is a more performant and stable connection, it's a private
(physical) connection between your corporate on-premises network to AWS.

### Use Cases

When transferring terabytes of data and setup time is not an issue.
Need consistency and low latency for performance.

### Facts

* Specific to a region, as it is a physical connection.
* Public Virtual Interfaces (or VIFs), while they operate in a single region,
  do allow you to connect to AWS public services (ex. S3, DynamoDB, etc) in
  other regions.
* Private VIFs can only connect to Virtual Private Gateways.
* Connections are not encrypted, so you had to use a workaround if you needed
  encryption.
* Direct Connect Gateways is a global resource
    * You are able to associate private VIFs, then associate any private gateways,
      in any region, thus allowing private VIFs access to resources in any region.
      However, it's not transitive, so VPCs connected cannot just start talking to
      each other, that has to be configured.
    * Can reduce admin overhead, by reducing the number of connections to maintain.
    * Charge for active ports (1GB/10GB); a charge for traffic that is transferred
      out.

## Transit Gateways

The business has a need for full interconnectivity between on premises networks
and the VPCs and between all the VPCs.

### Where Does It Live

As a logical networking device within an availability zone, so once need to be
placed in an availability zone to access the VPCs in those zones.

### Facts

* Can reduce admin overhead significantly.
* Support full hub-and-spoke architectures.
* Support RAM, so they can be shared between AWS accounts.
* Replace Virtual Private Gateways for VPC to on-premise connectivity.

### Helpful

* [](https://aws.amazon.com/blogs/networking-and-content-delivery/building-a-global-network-using-aws-transit-gateway-inter-region-peering/)
