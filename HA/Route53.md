# Route 53
Amazon Route 53 is a highly available and scalable Domain Name System (DNS) web service. You can use Route 53 to perform three main functions in any combination: domain registration, DNS routing, and health checking. 

## Main Concepts
- Alias: A type of record that you can create with Amazon Route 53 to route traffic to AWS resources such as Amazon CloudFront distributions and Amazon S3 buckets. For more information, see Choosing between alias and non-alias records.
- Hosted Zone: A container for records, which include information about how you want to route traffic for a domain (such as example.com) and all of its subdomains (such as www.example.com, retail.example.com, and seattle.accounting.example.com). A hosted zone has the same name as the corresponding domain. 
- Record: An object in a hosted zone that you use to define how you want to route traffic for the domain or a subdomain. For example, you might create records for example.com and www.example.com that route traffic to a web server that has an IP address of 192.0.2.234.

## Routing Policies
- Simple routing policy – Use to route internet traffic to a single resource that performs a given function for your domain, for example, a web server that serves content for the example.com website.

- Failover routing policy – Use when you want to configure active-passive failover.

- Geolocation routing policy – Use when you want to route internet traffic to your resources based on the location of your users.

- Geoproximity routing policy – Use when you want to route traffic based on the location of your resources and, optionally, shift traffic from resources in one location to resources in another.

- Latency routing policy – Use when you have resources in multiple locations and you want to route traffic to the resource that provides the best latency.

- IP-based routing policy – Use when you want to route traffic based on the location of your users, and have the IP addresses that the traffic originates from.

- Multivalue answer routing policy – Use when you want Route 53 to respond to DNS queries with up to eight healthy records selected at random.

- Weighted routing policy – Use to route traffic to multiple resources in proportions that you specify.

---------------
[Go Home](../README.md)