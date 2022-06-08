# AWS Certified Advanced Networking - Specialty (ANS-C01) Exam Guide 

# Domain 1: Network Design

## Task Statement 1.1: Design a solution that incorporates edge network services to optimize user performance and traffic management for global architectures.

###  Knowledge of Design patterns for the usage of content distribution networks (for example, Amazon CloudFront)

#### What is a [design pattern](https://en.wikipedia.org/wiki/Software_design_pattern)?
a design pattern is a general, reusable solution to a commonly occurring problem within a given context in software design. it is a description or template for how to solve a problem that can be used in many different situations. Design patterns are formalized best practices that the programmer can use to solve common problems when designing an application or system.

#### What is a content distribution network ([CDN](https://en.wikipedia.org/wiki/Content_delivery_network))?
![CDN](https://upload.wikimedia.org/wikipedia/commons/f/f9/NCDN_-_CDN.png) 
*(Left) Single server distribution (Right) CDN scheme of distribution*

A content delivery network, or content distribution network (CDN), is a geographically distributed network of proxy servers and their data centers. The goal is to provide high availability and performance by distributing the service spatially relative to end users. CDN is an umbrella term spanning different types of content delivery services: video streaming, software downloads, web and mobile content acceleration, licensed/managed CDN, transparent caching, and services to measure CDN performance, load balancing, Multi CDN switching and analytics and cloud intelligence.

#### What is Amazon [CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html)?
Amazon CloudFront is a web service that speeds up distribution of your static and dynamic web content, such as .html, .css, .js, and image files, to your users. CloudFront delivers your content through a worldwide network of data centers called edge locations. When a user requests content that you're serving with CloudFront, the request is routed to the edge location that provides the lowest latency (time delay), so that content is delivered with the best possible performance.

#### Use cases for [Cloudfront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/IntroductionUseCases.html)

#### Accelerate static website content delivery

![S3 + Orgin](https://d2908q01vomqb2.cloudfront.net/5b384ce32d8cdef02bc3a139d4cac0a22bb029e8/2020/06/07/S3-Blog-3-1024x576.jpg)
*Overview of cloudfront*

CloudFront can speed up the delivery of your static content (for example, images, style sheets, JavaScript, and so on) to viewers across the globe. By using CloudFront, you can take advantage of the AWS backbone network and CloudFront edge servers to give your viewers a fast, safe, and reliable experience when they visit your website.

A simple approach for storing and delivering static content is to use an Amazon S3 bucket. Using S3 together with CloudFront has a number of advantages, including the option to use Origin Access Identity (OAI) to easily restrict access to your S3 content.

![S3 + origin](https://d2908q01vomqb2.cloudfront.net/5b384ce32d8cdef02bc3a139d4cac0a22bb029e8/2018/06/27/4-v-2.png)

*Cloudfront traffic flow*

#### Serve video on demand or live streaming video
To deliver video on demand (VOD) streaming with CloudFront, use the following services:
1. Amazon S3 to store the content in its original format and to store the transcoded video.
2. An encoder (such as AWS Elemental MediaConvert) to transcode the video into streaming formats.
3. CloudFront to deliver the transcoded video to viewers. 

For broadcasting a live stream, you can cache media fragments at the edge, so that multiple requests for the manifest file that delivers the fragments in the right order can be combined, to reduce the load on your origin server.

#### Serving Private Content Using Amazon CloudFront & AWS Lambda@Edge

To serve private content using CloudFront, you do the following:
1. Require that your users (viewers) access content using signed URLs or signed cookies.
2. Restrict access to your origin so that it’s only available from CloudFront’s origin-facing servers.
   - For an Amazon S3 origin
     - use an origin access identity (OAI).
   - For a custom origin
     - use the CloudFront managed prefix list
     - Use a custom HTTP header to restrict access to only requests from CloudFront. 
     - use custom logic via Lambda@Edge

###  Knowledge of Design patterns for global traffic management (for example, AWS Global Accelerator)
#### What is [traffic management](https://en.wikipedia.org/wiki/Network_traffic_control)?
network traffic control is the process of managing, controlling or reducing the network traffic, particularly Internet bandwidth, e.g. by the network scheduler.[1] It is used by network administrators, to reduce congestion, latency and packet loss. This is part of bandwidth management. In order to use these tools effectively, it is necessary to measure the network traffic to determine the causes of network congestion and attack those problems specifically.

#### What is the [Global Accelerator](https://aws.amazon.com/global-accelerator/)?

AWS Global Accelerator combines advanced networking features with the dedicated AWS Global Network to improve your application network performance by up to 60%. TCP connections are terminated at the AWS Edge location closest to your users, instead of at your endpoint, accelerating data transfers globally.

By using AWS Global Accelerator, you can:

- Associate the static IP addresses provided by AWS Global Accelerator to regional AWS resources or endpoints, such as Network Load Balancers, Application Load Balancers, EC2 Instances, and Elastic IP addresses. 
- The IP addresses are anycast from AWS edge locations so they provide onboarding to the AWS global network close to your users. Easily move endpoints between Availability Zones or AWS Regions without needing to update your DNS configuration or change client-facing applications. Dial traffic up or down for a specific AWS Region by configuring a traffic dial percentage for your endpoint groups. 
- This is especially useful for testing performance and releasing updates. 
- Control the proportion of traffic directed to each endpoint within an endpoint group by assigning weights across the endpoints.

![Traditional network hops](https://d1.awsstatic.com/r2018/b/ubiquity/global-accelerator-before.46be83fdc7c630457bba963c7dc928cb676d9046.png)
*Traditional Network via internet*

![Global accelerator](https://d1.awsstatic.com/r2018/b/ubiquity/global-accelerator-after.2e404ac7f998e501219f2614bc048bb9c01f46d4.png)
*AWS Network via Global Accelerator*

###  Knowledge of Integration patterns for content distribution networks and global traffic management with other services (for example, Elastic Load Balancing, Amazon API Gateway)

CloudFront improves performance for both cacheable content (such as images and videos) and dynamic content (such as API acceleration and dynamic site delivery). Global Accelerator improves performance for a wide range of applications over TCP or UDP by proxying packets at the edge to applications running in one or more AWS Regions. Global Accelerator is a good fit for non-HTTP use cases, such as gaming (UDP), IoT (MQTT), or Voice over IP, as well as for HTTP use cases that specifically require static IP addresses or deterministic, fast regional failover. 

#### Cloudfront 

- Amazon CloudFront provides a simple API that lets you:
  - Distribute content with low latency and high data transfer rates by serving requests using a network of edge locations around the world.
- integrates with Amazon S3 for static objects, Amazon EC2 for dynamic content, and custom origins for third-party content, Elastic Load Balancing as origin servers, Amazon Route 53, WAF
- ACM manage certificate: you can now provision SSL/TLS certificates and associate them with CloudFront distributions within minutes. Simply provision a certificate using the new AWS Certificate Manager (ACM) and deploy it to your CloudFront distribution with a couple of clicks, and let ACM manage certificate renewals for you. ACM allows you to provision, deploy, and manage the certificate with no additional charges.
- log files are sent to s3 
- running code in response to CloudFront events (CloudFront Functions and Lambda@Edge)
  - CloudFront Functions was purpose-built for lightweight, high scale, and latency sensitive request/response transformations and manipulations. 
  - Use Lambda@Edge for computationally intensive operations.

#### Global Accelerator

- ELB provides load balancing within one Region, AWS Global Accelerator provides traffic management across multiple Regions. A regional ELB load balancer is an ideal target for AWS Global Accelerator.  

### Skills in Evaluating requirements of global inbound and outbound traffic from the internet to design an appropriate content distribution solution

#### LAB

## Task Statement 1.2: Design DNS solutions that meet public, private, and hybrid requirements.
Knowledge of:
• DNS protocol (for example, DNS records, timers, DNSSEC, DNS delegation, zones)
• DNS logging and monitoring
• Amazon Route 53 features (for example, alias records, traffic policies, resolvers, health checks)
• Integration of Route 53 with other AWS networking services (for example, Amazon VPC)
• Integration of Route 53 with hybrid, multi-account, and multi-Region options
• Domain registration
Skills in:
• Using Route 53 public hosted zones
• Using Route 53 private hosted zones
• Using Route 53 Resolver endpoints in hybrid and AWS architectures
• Using Route 53 for global traffic management
• Creating and managing domain registrations
## Task Statement 1.3: Design solutions that integrate load balancing to meet high availability, scalability,
and security requirements.
Knowledge of:
• How load balancing works at layer 3, layer 4, and layer 7 of the OSI model
• Different types of load balancers and how they meet requirements for network design, high
availability, and security
• Connectivity patterns that apply to load balancing based on the use case (for example, internal
load balancers, external load balancers)
• Scaling factors for load balancers
Version 1.0 ANS-C01 4 | PAGE
• Integrations of load balancers and other AWS services (for example, Global Accelerator,
CloudFront, AWS WAF, Route 53, Amazon Elastic Kubernetes Service [Amazon EKS], AWS
Certificate Manager [ACM])
• Configuration options for load balancers (for example, proxy protocol, cross-zone load
balancing, session affinity [sticky sessions], routing algorithms)
• Configuration options for load balancer target groups (for example, TCP, GENEVE, IP
compared with instance)
• AWS Load Balancer Controller for Kubernetes clusters
• Considerations for encryption and authentication with load balancers (for example, TLS
termination, TLS passthrough)
Skills in:
• Selecting an appropriate load balancer based on the use case
• Integrating auto scaling with load balancing solutions
• Integrating load balancers with existing application deployments
## Task Statement 1.4: Define logging and monitoring requirements across AWS and hybrid networks.
Knowledge of:
• Amazon CloudWatch metrics, agents, logs, alarms, dashboards, and insights in AWS
architectures to provide visibility
• AWS Transit Gateway Network Manager in architectures to provide visibility
• VPC Reachability Analyzer in architectures to provide visibility
• Flow logs and traffic mirroring in architecture to provide visibility
• Access logging (for example, load balancers, CloudFront)
Skills in:
• Identifying the logging and monitoring requirements
• Recommending appropriate metrics to provide visibility of the network status
• Capturing baseline network performance
## Task Statement 1.5: Design a routing strategy and connectivity architecture between on-premises
networks and the AWS Cloud.
Knowledge of:
• Routing fundamentals (for example, dynamic compared with static, BGP)
• Layer 1 and layer 2 concepts for physical interconnects (for example, VLAN, link aggregation
group [LAG], optics, jumbo frames)
• Encapsulation and encryption technologies (for example, Generic Routing Encapsulation [GRE],
IPsec)
• Resource sharing across AWS accounts
• Overlay networks
Version 1.0 ANS-C01 5 | PAGE
Skills in:
• Identifying the requirements for hybrid connectivity
• Designing a redundant hybrid connectivity model with AWS services (for example, AWS Direct
Connect, AWS Site-to-Site VPN)
• Designing BGP routing with BGP attributes to influence the traffic flows based on the desired
traffic patterns (load sharing, active/passive)
• Designing for integration of a software-defined wide area network (SD-WAN) with AWS (for
example, Transit Gateway Connect, overlay networks)
Task Statement 1.6: Design a routing strategy and connectivity architecture that include multiple AWS
accounts, AWS Regions, and VPCs to support different connectivity patterns.
Knowledge of:
• Different connectivity patterns and use cases (for example, VPC peering, Transit Gateway, AWS
PrivateLink)
• Capabilities and advantages of VPC sharing
• IP subnets and solutions accounting for IP address overlaps
Skills in:
• Connecting multiple VPCs by using the most appropriate services based on requirements (for
example, using VPC peering, Transit Gateway, PrivateLink)
• Using VPC sharing in a multi-account setup
• Managing IP overlaps by using different available services and options (for example, NAT,
PrivateLink, Transit Gateway routing)

# Domain 2: Network Implementation
## Task Statement 2.1: Implement routing and connectivity between on-premises networks and the AWS
Cloud.
Knowledge of:
• Routing protocols (for example, static, dynamic)
• VPNs (for example, security, accelerated VPN)
• Layer 1 and types of hardware to use (for example, Letter of Authorization [LOA] documents,
colocation facilities, Direct Connect)
• Layer 2 and layer 3 (for example, VLANs, IP addressing, gateways, routing, switching)
• Traffic management and SD-WAN (for example, Transit Gateway Connect)
• DNS (for example, conditional forwarding, hosted zones, resolvers)
• Security appliances (for example, firewalls)
• Load balancing (for example, layer 4 compared with layer 7, reverse proxies, layer 3)
• Infrastructure automation
• AWS Organizations and AWS Resource Access Manager (AWS RAM) (for example, multiaccount Transit Gateway, Direct Connect, Amazon VPC, Route 53)
Version 1.0 ANS-C01 6 | PAGE
• Test connectivity (for example, Route Analyzer, Reachability Analyzer)
• Networking services of VPCs
Skills in:
• Configuring the physical network requirements for hybrid connectivity solutions
• Configuring static or dynamic routing protocols to work with hybrid connectivity solutions
• Configuring existing on-premises networks to connect with the AWS Cloud
• Configuring existing on-premises name resolution with the AWS Cloud
• Configuring and implementing load balancing solutions
• Configuring network monitoring and logging for AWS services
• Testing and validating connectivity between environments
## Task Statement 2.2: Implement routing and connectivity across multiple AWS accounts, Regions, and
VPCs to support different connectivity patterns.
Knowledge of:
• Inter-VPC and multi-account connectivity (for example, VPC peering, Transit Gateway, VPN,
third-party vendors, SD-WAN, multiprotocol label switching [MPLS])
• Private application connectivity (for example, PrivateLink)
• Methods of expanding AWS networking connectivity (for example, Organizations, AWS RAM)
• Host and service name resolution for applications and clients (for example, DNS)
• Infrastructure automation
• Authentication and authorization (for example, SAML, Active Directory)
• Security (for example, security groups, network ACLs, AWS Network Firewall)
• Test connectivity (for example, Route Analyzer, Reachability Analyzer, tooling)
Skills in:
• Configuring network connectivity architectures by using AWS services in a single-VPC or multiVPC design (for example, DHCP, routing, security groups)
• Configuring hybrid connectivity with existing third-party vendor solutions
• Configuring a hub-and-spoke network architecture (for example, Transit Gateway, transit VPC)
• Configuring a DNS solution to make hybrid connectivity possible
• Implementing security between network boundaries
• Configuring network monitoring and logging by using AWS solutions
## Task Statement 2.3: Implement complex hybrid and multi-account DNS architectures.
Knowledge of:
• When to use private hosted zones and public hosted zones
• Methods to alter traffic management (for example, based on latency, geography, weighting)
• DNS delegation and forwarding (for example, conditional forwarding)
• Different DNS record types (for example, A, AAAA, TXT, pointer records, alias records)
• DNSSEC
Version 1.0 ANS-C01 7 | PAGE
• How to share DNS services between accounts (for example, AWS RAM)
• Requirements and implementation options for outbound and inbound endpoints
Skills in:
• Configuring DNS zones and conditional forwarding
• Configuring traffic management by using DNS solutions
• Configuring DNS for hybrid networks
• Configuring appropriate DNS records
• Configuring DNSSEC on Route 53
• Configuring DNS within a centralized or distributed network architecture
• Configuring DNS monitoring and logging on Route 53
## Task Statement 2.4: Automate and configure network infrastructure.
Knowledge of:
• Infrastructure as code (IaC) (for example, AWS Cloud Development Kit [AWS CDK], AWS
CloudFormation, AWS CLI, AWS SDK, APIs)
• Event-driven network automation
• Common problems of using hardcoded instructions in IaC templates when provisioning cloud
networking resources
Skills in:
• Creating and managing repeatable network configurations
• Integrating event-driven networking functions
• Integrating hybrid network automation options with AWS native IaC
• Eliminating risk and achieving efficiency in a cloud networking environment while maintaining
the lowest possible cost
• Automating the process of optimizing cloud network resources with IaC

# Domain 3: Network Management and Operations
## Task Statement 3.1: Maintain routing and connectivity on AWS and hybrid networks.
Knowledge of:
• Industry-standard routing protocols that are used in AWS hybrid networks (for example, BGP
over Direct Connect)
• Connectivity methods for AWS and hybrid networks (for example, Direct Connect gateway,
Transit Gateway, VIFs)
• How limits and quotas affect AWS networking services (for example, bandwidth limits, route
limits)
• Available private and public access methods for custom services (for example, PrivateLink, VPC
peering)
• Available inter-Regional and intra-Regional communication patterns
Version 1.0 ANS-C01 8 | PAGE
Skills in:
• Managing routing protocols for AWS and hybrid connectivity options (for example, over a
Direct Connect connection, VPN)
• Maintaining private access to custom services (for example, PrivateLink, VPC peering)
• Using route tables to direct traffic appropriately (for example, automatic propagation, BGP)
• Setting up private access or public access to AWS services (for example, Direct Connect, VPN)
• Optimizing routing over dynamic and static routing protocols (for example, summarizing
routes, CIDR overlap)
## Task Statement 3.2: Monitor and analyze network traffic to troubleshoot and optimize connectivity
patterns.
Knowledge of:
• Network performance metrics and reachability constraints (for example, routing, packet size)
• Appropriate logs and metrics to assess network performance and reachability issues (for
example, packet loss)
• Tools to collect and analyze logs and metrics (for example, CloudWatch, VPC Flow Logs, VPC
Traffic Mirroring)
• Tools to analyze routing patterns and issues (for example, Reachability Analyzer, Transit
Gateway Network Manager)
Skills in:
• Analyzing tool output to assess network performance and troubleshoot connectivity (for
example, VPC Flow Logs, Amazon CloudWatch Logs)
• Mapping or understanding network topology (for example, Transit Gateway Network Manager)
• Analyzing packets to identify issues in packet shaping (for example, VPC Traffic Mirroring)
• Troubleshooting connectivity issues that are caused by network misconfiguration (for example,
Reachability Analyzer)
• Verifying that a network configuration meets network design requirements (for example,
Reachability Analyzer)
• Automating the verification of connectivity intent as a network configuration changes (for
example, Reachability Analyzer)
• Troubleshooting packet size mismatches in a VPC to restore network connectivity
## Task Statement 3.3: Optimize AWS networks for performance, reliability, and cost-effectiveness.
Knowledge of:
• Situations in which a VPC peer or a transit gateway are appropriate
• Different methods to reduce bandwidth utilization (for example, unicast compared with
multicast, CloudFront)
• Cost-effective connectivity options for data transfer between a VPC and on-premises
environments
• Different types of network interfaces on AWS
• High-availability features in Route 53 (for example, DNS load balancing using health checks
with latency and weighted record sets)
Version 1.0 ANS-C01 9 | PAGE
• Availability of options from Route 53 that provide reliability
• Load balancing and traffic distribution patterns
• VPC subnet optimization
• Frame size optimization for bandwidth across different connection types
Skills in:
• Optimizing for network throughput
• Selecting the right network interface for the best performance (for example, elastic network
interface, Elastic Network Adapter [ENA], Elastic Fabric Adapter [EFA])
• Choosing between VPC peering, proxy patterns, or a transit gateway connection based on
analysis of the network requirements provided
• Implementing a solution on an appropriate network connectivity service (for example, VPC
peering, Transit Gateway, VPN connection) to meet network requirements
• Implementing a multicast capability within a VPC and on-premises environments
• Creating Route 53 public hosted zones and private hosted zones and records to optimize
application availability (for example, private zonal DNS entry to route traffic to multiple
Availability Zones)
• Updating and optimizing subnets for auto scaling configurations to support increased
application load
• Updating and optimizing subnets to prevent the depletion of available IP addresses within a
VPC (for example, secondary CIDR)
• Configuring jumbo frame support across connection types
• Optimizing network connectivity by using Global Accelerator to improve network performance
and application availability

# Domain 4: Network Security, Compliance, and Governance
## Task Statement 4.1: Implement and maintain network features to meet security and compliance needs
and requirements.
Knowledge of:
• Different threat models based on application architecture
• Common security threats
• Mechanisms to secure different application flows
• AWS network architecture that meets security and compliance requirements
Skills in:
• Securing inbound traffic flows into AWS (for example, AWS WAF, AWS Shield, Network
Firewall)
• Securing outbound traffic flows from AWS (for example, Network Firewall, proxies, Gateway
Load Balancers)
• Securing inter-VPC traffic within an account or across multiple accounts (for example, security
groups, network ACLs, VPC endpoint policies)
• Implementing an AWS network architecture to meet security and compliance requirements
(for example, untrusted network, perimeter VPC, three-tier architecture)
Version 1.0 ANS-C01 10 | PAGE
• Developing a threat model and identifying appropriate mitigation strategies for a given
network architecture
• Testing compliance with the initial requirements (for example, failover test, resiliency)
• Automating security incident reporting and alerting using AWS
## Task Statement 4.2: Validate and audit security by using network monitoring and logging services.
Knowledge of:
• Network monitoring and logging services that are available in AWS (for example, CloudWatch,
AWS CloudTrail, VPC Traffic Mirroring, VPC Flow Logs, Transit Gateway Network Manager)
• Alert mechanisms (for example, CloudWatch alarms)
• Log creation in different AWS services (for example, VPC flow logs, load balancer access logs,
CloudFront access logs)
• Log delivery mechanisms (for example, Amazon Kinesis, Route 53, CloudWatch)
• Mechanisms to audit network security configurations (for example, security groups, AWS
Firewall Manager, AWS Trusted Advisor)
Skills in:
• Creating and analyzing a VPC flow log (including base and extended fields of flow logs)
• Creating and analyzing network traffic mirroring (for example, using VPC Traffic Mirroring)
• Implementing automated alarms by using CloudWatch
• Implementing customized metrics by using CloudWatch
• Correlating and analyzing information across single or multiple AWS log sources
• Implementing log delivery solutions
• Implementing a network audit strategy across single or multiple AWS network services and
accounts (for example, Firewall Manager, security groups, network ACLs)
## Task Statement 4.3: Implement and maintain confidentiality of data and communications of the
network.
Knowledge of:
• Network encryption options that are available on AWS
• VPN connectivity over Direct Connect
• Encryption methods for data in transit (for example, IPsec)
• Network encryption under the AWS shared responsibility model
• Security methods for DNS communications (for example, DNSSEC)
Skills in:
• Implementing network encryption methods to meet application compliance requirements (for
example, IPsec, TLS)
• Implementing encryption solutions to secure data in transit (for example, CloudFront,
Application Load Balancers and Network Load Balancers, VPN over Direct Connect, AWS
managed databases, Amazon S3, custom solutions on Amazon EC2, Transit Gateway)
Version 1.0 ANS-C01 11 | PAGE
• Implementing a certificate management solution by using a certificate authority (for example,
ACM, AWS Certificate Manager Private Certificate Authority [ACM PCA])
• Implementing secure DNS communications
