# Direct Connect
AWS Direct Connect links your internal network to an AWS Direct Connect location over a standard Ethernet fiber-optic cable. One end of the cable is connected to your router, the other to an AWS Direct Connect router. With this connection.
![Diagram](https://docs.aws.amazon.com/directconnect/latest/UserGuide/images/direct-connect-overview.png)

## Connections
There are two types of connections:

- Dedicated Connection: A physical Ethernet connection associated with a single customer. Customers can request a dedicated connection through the AWS Direct Connect console, the CLI, or the API.
- Hosted Connection: A physical Ethernet connection that an AWS Direct Connect Partner provisions on behalf of a customer. Customers request a hosted connection by contacting a partner in the AWS Direct Connect Partner Program, who provisions the connection.

## Virtual Interfaces
You must create one of the following virtual interfaces to begin using your AWS Direct Connect connection.

- Private virtual interface: A private virtual interface should be used to access an Amazon VPC using private IP addresses.
- Public virtual interface: A public virtual interface can access all AWS public services using public IP addresses.
- Transit virtual interface: A transit virtual interface should be used to access one or more Amazon VPC Transit Gateways associated with Direct Connect gateways.

---------------
[Go Home](../README.md)