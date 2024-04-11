
#### Project ID

A [Google Cloud project](https://cloud.google.com/docs/overview/#projects) is an organizing entity for your Google Cloud resources. It often contains resources and services; for example, it may hold a pool of virtual machines, a set of databases, and a network that connects them together. Projects also contain settings and permissions, which specify security rules and who has access to what resources.

A _Project ID_ is a unique identifier that is used to link Google Cloud resources and APIs to your specific project. Project IDs are unique across Google Cloud: there can be only one **qwiklabs-gcp-xxx....**, which makes it globally identifiable.

#### Username and Password

These credentials represent an identity in the Cloud Identity and Access Management (Cloud IAM) service. This identity has access permissions (a role or roles) that allow you to work with Google Cloud resources in the project you've been allocated. These credentials are _temporary_ and will only work for the access time of the lab. When the timer reaches 00:00:00, you will no longer have access to your Google Cloud project with those credentials.

student-04-d37ae6124544@qwiklabs.net
qGYhBZKH7vsb
qwiklabs-gcp-00-41ba7c7b2c74

---
#### Roles and Permissions

In addition to cloud computing services, Google Cloud also contains a collection of permissions and roles that define who has access to what resources. You can use the [Cloud Identity and Access Management (Cloud IAM)](https://cloud.google.com/iam/) service to inspect and modify these roles and permissions.

The following table pulls definitions from the [roles documentation](https://cloud.google.com/iam/docs/understanding-roles/#primitive\_roles), which gives a brief overview of viewer, editor, and owner role permissions:

| Role Name    | Permissions                                                                                                                                                                      |
| ------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| roles/viewer | Permissions for read-only actions that do not affect state, such as viewing (but not modifying) existing resources or data.                                                      |
| roles/editor | All viewer permissions, plus permissions for actions that modify state, such as changing existing resources.                                                                     |
| roles/owner  | All editor permissions and permissions for the following actions: manage roles and permissions for a project and all resources within the project; set up billing for a project. |

---
#### APIs and services

Google Cloud APIs are a key part of Google Cloud. Like services, the 200+ APIs, in areas that range from business administration to machine learning, all easily integrate with Google Cloud projects and applications.

APIs are _application programming interfaces_ that you can call directly or via the client libraries. Cloud APIs use resource-oriented design principles as described in the [API Design Guide](https://cloud.google.com/apis/design/).


#### Google Cloud Resource Hierarchy 

![[Pasted image 20240327000401.png]]

This Diagram determines how policies are applied on GCP resources, those are inherited downwards (from organizations to resources).

Every project has 3 attributes: 

* Project ID - Global unique identifier for the project (immutable, unique and used to reffer a context).
* Project Name - Mutable project title 
* Project Number - Globaly unique, immutable and used by gcp also

Resource Manager Tool - AWS Config from GCP and can be used to recover deleted projects, create new or validate exhinsting resources

_Folders_ enable the delegation of permissions for GCP resources under it

Organizations - Creates and manages workspaces based on the Google Workspace service (if client: projects will belong to an organization, else: they will be attached to an cloud identity).

---
#### IAM - Identity and Access Management

The identity model used by GCP is RBAC and has the following attributes: 

* WHO - A principal type (mostly an e-mail address) that is capable of assuming a role to execute something
* CAN/CAN't - A role is used to define the permission set that an principal may assume during executions. Roles may be one of 3:
	* Basic IAM role: Are broad in scope and reach all the project (examples are: Owner, Editor, Viewer and Billing Admin).
	* Predifined IAM role: Are roles delivered by GCP services (Instance profiles, Resource profiles, etc for executing specific actions on that service).
	* Custom IAM role: Fine grained managed policies for minimum privilege based (Organization and Project level only).



Service Accounts == Instance Profiles

Cloud Identity - Is a tool for centralizing access to GCP with Identity Providers (such as LDAP) and allows Identity Administrators to fully manage identities on cloud.

Access points for identities on GCP: 

* APIs 
* Google Cloud App
* Google Cloud Console 
* Cloud SDK and Cloud Shell 

---
### VPC - Virtual Private Cloud 

Restricted network inside Google Cloud (SDN). 

Differently from other Cloud Providers, GCP VPCs are global and divide their subnet in regions/zones. 

Connecting other VPCs with GCP: 

* VPN - Create a tunnel over the internet between peers (using Cloud Router with Border Gateway Protocol). 
* Direct Peering - Creates a P2P link across datacenter and GCP.
* Carrier Peering - Direct access from on-premises network through an service provider network (such as vivo backbone - works well for small businesses).
* Dedicated Interconnect - Private direct and private connect with google (attached with VPN). 
* Partner Interconnect - Puts a middle man between the interconnect facilty.
* Cross-Cloud Interconnect - Connects another Cloud providers VPCs.

---
### Compute Engine 

Service for provisioning VMs on Google Cloud using the minimal parametrization as possible and enabling autoscaling, load balancing, private networking, machine types and subscriptions. 

Not really the focus of the platform. 

Spot Instance == Preemptible VM

---
### Load Balancers

* Global HTTP(S) - Cross-region for web apps 
* Global SSL - Cross-region non http
* Global TCP - Cross-region TCP non-encrypted
* Regional External - UDP only and regional 
* Regional Internal - Proxyed/Passthrough/Application loadbalancer for Compute VMs (reverse)
* Cross-Region Internal - Layer 7 for balancing across all features

---
### Cloud DNS

Managed DNS Service for low latency and custom DNS entries. Also works with Cloud CDN for caching contents and balancing of the content.

---
### Storage

Types of data supported by GCP: 

* Structured
* Unstructured
* Transactional
* Relational 

- Cloud Storage - Object Storage (Key/Value Hierarchy), supports versioning, lifecycles,url shares and it is stored in binary format (streams) that can be shared across programatcly or in web format. 
	- Standard - Hot data 
	- Nearline - Access once per month 
	- Coldline - Access up to 90 days 
	- Archive - Online backup and DR
	- Autoclass - Automaticly apply lifecycles based on the access patterns 
- Cloud SQL - Storage for relational data using data centered VM nodes with primary, backup and replication types.

- Cloud Spanner - Sacales horizontaly, SQL indexers, Global Consistent and I/O intense (looks like etl spirit)

- Firestore - Flexible NoSQL database for app development, it organize data into documents and collections (just like mongo). It is billed by transactions and bandwith, offering a daily free workload for usage. 

- Biigtable - Big Data database service, designed for massive data workloads for semi/structured data.
---
### GKE - Google Kubernetes Enginge 

Uses Cloud load balancing and hosts from compute engine. 

Logging and monitoring with GCloud suite.

---
### Cloud Run 

Cloud Run is a serverless code runner for small projects that removes the need for managing infrastructure on projects. 

It runs kubernetes under the hood using Knative and Buildpacks. 

Cloud Run only takes Docker Hub or Artifact Registry for container images to be ran in the service.
