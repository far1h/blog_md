---
title: Google Associate Cloud Engineer Notes
excerpt: lets get the infinity stones. clean cloud.
---
[[reasons behind using cloud|why use cloud?]]

https://www.in28minutes.com/gcp-bookshelf  
https://www.in28minutes.com/downloads/09-google-certified-associate-cloud-engineer/CoursePresentation-GoogleCertifiedAssociateCloudEngineer.pdf  

how do projects work in [[gcp]]?
# [[Region|Regions]] and [[Zone|Zones]]

# [[cloud-compute|Compute]]

# [[cloud-billing|Billing and Cost Planning]]

# Google Compute - Optimizing Costs and Performance in Google Cloud Platform

# Gcloud for Associate Cloud Engineer

# Instance Groups in Google Cloud

# Load Balancing in Google Cloud Platform

# Managed Services in Google Cloud Platform

# Google App Engine

# Google Kubernetes Engine

# Google Cloud Functions

# Google Cloud Run

# Google Cloud Functions Gen 2

# Encryption in Google Cloud with Cloud KMS

# Block and File Storage in Google Cloud Platform - GCP

# Object Storage in Google Cloud Platform - Cloud Storage

# Authentication and Authorization in Google Cloud with Cloud IAM

# Database in Google Cloud Platform

# Asynchronous Communication in Google Cloud with Cloud Pub Sub

# Private Networks in Google Cloud - Cloud VPC

# Operations in Google Cloud Platform - GCP

# Organizations and IAM - Organizing Google Cloud Resources

# GCP - Pricing Calculator

# Other Important Services

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
### Google Cloud Resource Hierarchy
1. **Hierarchy Levels**:
   - **Resources**: Includes VMs, Cloud Storage, VPCs, etc.
   - **Projects**: Organize resources, enable billing, and control access.
   - **Folders**: Group projects or subfolders (departmental organization).
   - **Organization Node**: Top-level for all resources within a domain.

2. **Policies and Inheritance**:
   - Policies apply to nodes at any level and inherit downward.
   - Specific policies can apply to resources directly (e.g., access permissions).

3. **Projects**:
   - Enable Cloud services, manage APIs, billing, and permissions.
   - **Project ID**: Unique and immutable after creation.
   - **Project Name**: Not unique and can be changed.
   - **Project Number**: Assigned by Google Cloud, primarily for internal tracking.

4. **Resource Manager**:
   - API to create, list, update, and delete projects.
   - Supports RPC and REST API access.

### Identity and Access Management (IAM)
1. **Role Types**:
   - **Basic Roles**: Broad permissions (e.g., Owner, Editor, Viewer).
   - **Predefined Roles**: Specific to services, e.g., `instanceAdmin` for Compute Engine.
   - **Custom Roles**: Tailored permissions, supporting least-privilege model.

2. **Service Accounts**:
   - Allow non-human identities to access resources.
   - Each account identified by an email, using cryptographic keys.
   - Used in scenarios like VM interactions with Cloud Storage.

3. **Cloud Identity**:
   - Manages user and group access within organizations.
   - Centralized management of user permissions.

### Interacting with Google Cloud
1. **Methods of Interaction**:
   - **Google Cloud Console**: GUI for managing resources.
   - **Cloud SDK and Cloud Shell**: Command-line tools, with `gcloud` and `bq` for BigQuery.
   - **APIs**: Programmatic access with API Explorer and client libraries.
   - **Google Cloud App**: Mobile management tool, with features like billing alerts and customizable metrics.

### Quiz Tips
1. **Services and APIs**:
   - Enabled on a per-**Project** basis.

2. **IAM Role Granularity**:
   - **Basic > Predefined > Custom** (broadest to finest-grained).

3. **Unique Identifiers**:
   - **Project ID** is globally unique, unchangeable post-creation.

### Lab Practice
1. **Cloud Marketplace**:
   - Practice deploying LAMP stacks and other preconfigured environments.
   - Use Bitnami LAMP Stack for a full Linux web development setup.

## Virtual Machines and Networks in the Cloud

## Storage in the Cloud

## Containers in the Cloud

## Applications in the Cloud

Status: #MOC  
Tags: [[cloud]], [[gcp]]  

---
