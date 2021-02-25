# VPC

A VPC endpoint enables you to privately connect your VPC to supported AWS
services and VPC endpoint services (using PrivateLink) without an internet 
gateway/NAT device/VPN connection/Direct Connect connection. Uses private IPs
and never leaves the Amazon network.

## VPC Endpoints

Allows access to AWS public services (such as S3, SQS, DynamoDB, etc) to
resources in a VPC subnet without any internet connectivity.

### Use Cases

Depending on IT security, a company may not want a VPC to be public at all, or
some subnets to be completely private and is where VPC comes in handy.

### Types

### Gateway endpoint

#### Where does it live

Exist as a logical entity inside the VPC, but outside any subnet.

#### Facts

* Are region specific and highly available in that region.

### Questions

* How do NACLs affect what traffic flows through the VPC endpoint?
    * Could I use a NACL to allow S3, but restrict DynamoDB?
        * VPC endpoints can be referenced in your route table and each endpoint
          is specific to a service and region, such as S3 US-east-2.
        * You can be secured by using policies on the resource/service you want
          access to, via VPC or VPCe restriction. If you try to restrict by IP
          it will cause problems.
    * What services do they support now?

### Interface endpoint

An elastic network interface with a private IP address from the IP address
range of your subnet. It serves as an entry point for traffic destined to a 
supported AWS service or a VPC endpoint service. 

#### Where does it Live

Are a physical entity inside an AZ, thus require setup in multiple AZs for high
availability.

#### Facts

* Are powered by AWS PrivateLink.
* Are elastic network interfaces and use security groups to restrict access.
* Create unique DNS names for the zone and region they are in.
* Can use private DNS to override the public DNS name or a service so that you
  don’t need to modify code.

* Bandwidth is restricted to 10G/s.
    * You can increase that by using multiple endpoints and modifying code to
      use private DNS in the case of Interface endpoints or have a plist point
      to a different Gateway endpoint in each subnet's route table.

* Alternatives
    * Use a NAT gateway, but then resources would have access to the public
      internet.
