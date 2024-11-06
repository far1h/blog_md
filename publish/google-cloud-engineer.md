---
title: Google Cloud Engineer Notes
---
## Introducing Google Cloud
### An overview of cloud computing 

offerings:
- compute
- storage
- big data
- machine learning
- application services

cloud computing traits
- computing resources that are on-demand and self-service
- get access to those resources over the internet, from anywhere
- a pool resources for users to use
- resources are elastic
- pay only for what they use

The history of cloud computing
1. Colocation
2. Virtualized data center
3. ==Container-based architecture??== 
### IaaS and PaaS 

Infrastructure as a service includes:
- raw compute
- storage
- network capabilities

>Pay for what they allocate

Platform as a Service delivers and manages all the hardware and software through the cloud. Ex: App Engine
>Pay for what they use

SaaS provides the entire application stack, delivering an entire cloud-based application that customers can access and use. Ex: Gmail, Docs, and Drive
### The Google Cloud network 

five major geographic locations: 
1. North America, 
2. South America, 
3. Europe, 
4. Asia, and 
5. Australia

> Each of these locations are divided into a number of different **regions** and **zones**.

Regions: independent geographic areas, and are composed of zones.
Zone: an area where Google Cloud resources get deployed

### Environmental impact 

- all existing data centers use roughly 2% of the world’s electricity
- first to achieve ISO 14001 certification
- commitment to carbon free by 2030
### Security 

#### Hardware infrastructure level
- Hardware design and provenance: Server boards, chips, and he networking equipment in Google data centers custom designed by Google.
- Secure boot stack: Google's server machines ensure that they are booting the correct software stack.
- Premises security: Google data centers incorporate multiple layers of physical security protections.

#### Service deployment level
- Encryption of inter-service communication: Services communicate with each other using remote procedure calls (“RPCs”). Google’s infrastructure encrypts all infrastructure RPC traffic between data centers.

#### User identity level
- User identity: Intelligently challenges users for additional information based on certain risk factors. Users can use secondary factors when signing in, including Factor (U2F) open standard.

#### Storage services level
- Encryption at rest: Most Google applications access file storage indirectly via storage services and encryption. Using centrally managed keys, encryption is applied at the layer of these storage services. Google also enables hardware encryption support in hard drives and SSDs.

#### Internet communication level
- Google Front End ("GFE"): Google Front End ensures that all registered services use TLS connections incorporating the correct certificates and following best practices.
- Denial of Service ("DoS") protection: Google has multi-tier, multi-layer DoS protections that reduce the risk of any DoS impact on a service running behind a GFE.

#### Operational security level

- Intrusion detection: Rules and machine intelligence give operational security engineers warnings of possible incidents.
- Reducing insider risk: Google limits and monitors the activities of employees who have access to the infrastructure.
- Employee Universal Second Factor (U2F) use: All Google employee accounts require use of U2F-compatible Security Keys.
- Software development practices: Google employs central source control and requires two-party review of any new code.
### Open APIs and open source 
### Pricing and billing
per-second billing
## Resources and Access in the Cloud

## Virtual Machines and Networks in the Cloud

## Storage in the Cloud

## Containers in the Cloud

## Applications in the Cloud