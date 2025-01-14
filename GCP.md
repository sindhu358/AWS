### Data Lake :
it is a large centralized large repo for storing you data into a single location
It will be in the same raw data




## Regions
Specific geographical locations to host local resources
advantages:
High availability
low latency
Global footprint
Adhere to govt regulations


Google cloud has multiple zones
Each region has --> 3 zones
                      |
                  Each zone has
                  one or more discrete cluster
CLuster: distinct physical infrastructure that is housed in a data centre.


## Compute Engine

Generaly in corporate data centres, applications are delpoyed to physical servers.
Whereas in Cloud you deploy applications as by:
1. Renting the virtual servers
2. Virtual Machines - Virtual servers in GCP
3. Google Compute ENgine(GCE): Provisional and Manage VM


## Ip Addresses - VM
- Internal IP - Permanent Internal IP Addres which does not change during the lifetime of an instance.
- External IP - It changes if we stop and restart it again 
- Static IP - Permananent external IP adress that can be attached to a VM 


## Instance Template(created with public image-Debian)
1.creating an instance template
  - machine type, image,labels,startup script and other properties
2.It is used to create VM instances and managed instance groups(group of vm)
  - can create similar instances
3.cannot be updated
4.make a copy of an existing template and modify that - Creating a new one


## Reducing launch time with cutom image
instance1(Compute ENgine)--> Image --> Instances

Installing OS patches and software at launch of VM instances increases boot up time

 create an image - can be created from an instance, a persistenet disk, a snapshot, another image or a file in cloud storage 
- shareed across 
- Deprecate old image
**Hardeneing an image** - customize/creating an image which adheres to all of our/corporate security standards
prefer using CUstom image to startuo script
Steps:
- Copy existing instance template and crate image
- Create an instance template with cutomized image from the copied instance
- Create a VM from it

## Preemptible VM
can be stopped by GCP at any time within 24 hrs
Instances get 30 secnd warning(to save anything  they want to save)
Use Preepmt if:
  - Application is fault tolerant
  - cost sensitive
  - workload is not immediate
  eg: Non immediate batch processing jobs
restriction:
  - not always available
  - no SLA and cannot be migrated to regular VM's
  - no automatic Restarts
  - free tier cannot be applicable
spot vm: 

## Sole-tenant- Nodes
vm are created in a HOst computer 
default tenancy is shared tenancy SI
**Sharered tenancy**: Single host machine can have instances from multiplecustomers.
**Sole-tenant Nodes**: Virtualized instances on hardware dedicated to one customer.
1. Security and compliances requirments: You want your VM's to be physically separated from those in other projects
2. High performance : Groups ur vms together
3. Licensing : Using per-core or per-processor "Bring your own licenses"

No.of instances
Type of OS
Disk

## CUstom Machine types:
Create a mchine type customized to your need when predefined VM optins are not appropriate for ur workload
then we use a Custom machine type
- Adjust CPU's, memory and GPUs
- choose between E2,N2, or N1 machine types
supports a wide variety of Operating systems: CentOS, CoreOS, Debian, RedHat, UBUNtu, windows,etc
- Billed per vCPUs, memory provisional to each instance

### VM Costs
2 primary costs
1.Infrastructure to run ur VM's
2. Licensing cost for ur OS(only for Premium mImages)
   - Premium Image Examples: Redhat ENterprise,Linux,SUSE Linux,UBUNTU, etc..
   - Options for Licensing:
       * PAYG : PAy as you Go
       * WIthin a lot of Constraints: use ur existing license/subscription(Bring ur own license- BYOS/BYOL)

## Scenarios- Compute Engine
| Scenario| Service|
|---------|--------|
|I want to ensure my VM runs a specific OS and Software stack for my application| Custom image|
|I need to optimize my VM for a specialized workload requring a unique mix of CPU,memory and storage| Custom Machine Types|
|My application requires a fied IP address that doesn't change between reboots or reassignments| Static IP Addresses|
|I have predictable resource needs and want to commit to a 1 or 3-year plan to enjoy deeper dicounts| Commited use discounts|
|I need to run short-lived,fault-tolerant workload that can tolertae interruptions in exhange for lower costs| preemptible VM's|

## Instance Group
Instance Group: Group of VM instance managed as a single entity
- managed: Identical VMs created using a template:\\
  Features: autoscaling,autohealing and managed releases
- Unmanaged: Different configuration for VMs in same group:
  - Doesn't offer auto-scaling or healing and other services
  - Not recommended unless u need a different kind id VM's
  Location can be ZOnal or Regional
   - regional is best as ir provides higher availability

**Managed Instance Group (MIG)** 
Identical VM's are created using a instance template
  - Stateless- web applications
  - Stateful-db based
 **Feature**:
  - If instance is crashed, MIG launches another instance(Maintain certain no.of instances)
  - Detect the application failures using health check (`Self Healing`)
  - Increase and decrease instances based on load(`Auto Scaling`).

      configure auto-scaling automatically adjust the no.of instances based on load:  
        * `cool-down period`: How long to wait before looking at autoscaling again  
        * `scale in controls`: Prevent in sudden drop in noof VM instances,  
            EG: Don't scale more than 10% or 3 instances in 5 min
  - Add `LoadBalancer` to distribute the load
  - Create instances in multiple zones
  - Release new applicati0n versions without downtime
     * Rolling Updates: Release new version step by step(gradually).Update a percentage of instance to the the new verions at a time
     * Canary Deployment: Test new verion with a grp of instance before releasing it across all instances.     

  ### Cloud Load Balancing 
  It distributes traffic across VM instances in 1 or more regions
    1.**Managed Services**:
      - Google cloud ensures that it is highly available
      - Auto scales handles huge loads
      - Load Balancers can be private or public
    **Types**:
     - External HTTPS
     - Internal HTTPS
     - SSL Proxy
     - TCP proxy
     - External Network TCP/UDP
     - Internal TCP/UDP
    ![image](https://github.com/user-attachments/assets/30ca85b0-3af6-4fd1-8a6b-9afd5c4f9641)

    ![image](https://github.com/user-attachments/assets/339706e3-29e8-4b07-beea-846a4c2c1511)



## Managed Services:
- IaaS
- Paas
- Faas(Function as service)
- Caas(Container as service)
- Serverless
#### Iaas (Infrastructure as a Sevice):
Use only **infrastructure** from cloud provider
Using VM to deploy your appications or databases
Deploying a python application
Taking a VM 
choosing the right OS
installing applcation runtime(pytho/java/Node JS)
application code 
setup the configuration for it 

Virtualization, Physical Hardware, Networking 

#### PAAS: Platform as a Service:
Use only **Platform** from cloud provider

You are responsible for:
- Configuration(of Applcation and Services)
- Application code(if needed)

Cloud provider is responsible for:
- OS(incl,upgrades and patches)
- Application runtime
- Auto Scaling, Availability and Load balancing, etc..
- Virtualization
- Physical Hardware
- Networking

Database - Relational & No SQL(Amazon, RDS, Google cloud,SQL, AZUre SQL DB,etc), Queues, AI, ML, Operations,etc

#### Caas(Container as Service):
ENterprises are heading towards microservices architecture
- Build small microservices
- Flexibility to innovate and build applications in different programming languages(Go,Java, Python,etc..)
  But deployments become complex due to multiple languages
  **Container - Docker**
  Create a Docker images for each microservice
  Docker image has all needs of a microservice
  - Application Runtime(JDK or Python or Node JS)
  - Application code and Dependencies
 Runs the same way on any infrastructure
 - Your  local machine
 - Corporate data center
 - CLoud
Advantages:
-Docker containers are light weight and Compared to VM as they do not have a Fuest OS
-DOcker provides isolation for containers
- It is Cloud neutral

##### Container Orchestration:
 I want 10 instances of Micr A, 15 instances of mic
 Container Image  Configuration
 Container Orchestrator(Kubernetes)
 CLuster
 Virtual Server 1,2,3

 **Features**
 - Auto scaling- Scale containers based on demand
 - Service discovery- Help microservices find one another
 - Load Balancer - Distribute load among multiple instances or microservce
 - Self healing - Do health check and replace failing instances
 - Zer Downtime Deployment - Relaes new versions without downtime

#### Serverless:
- Zero visibility into infratructure 
  - Flexible scaling and automated high availability

Allowing to focusing on code and the cloud managed service takes care of all that is needed to scale your code to serve millions pf requests
   you pay requests(invocations of your application) not for servers
  eg: Faas

  #### Saas (Software as a Service):
  Centrally hosted software(most;y on the cloud)
  - Offered on a subscription basis(pay-as-you-go)
    EX:
    -  Email, calendering and office tools(such as Outlook 365, microsoft Office 365, Gmail, Google Docs)
    -  Customer relationship management(CRM), enterprise resource planning(ERP) and document management tools.
  - Cloud provider is reponsible for :
      - OS(incl,upgrades and patches)
      - Application runtime
      - Auto Scaling, Availability and Load balancing, etc.
      - Application code and/or
      - Application Configuration(memory,instance)
  - Customer is responsible for :
      - Configuring the software
 ### Shared Responsibility Model
 - Security in cloud is a Shared Responsibility:
     Between GCp and the Customer
 - GCP provides features to make security easy:
     - Encryption at rest by default
     - IAM
     - KMS etc
 - Customer responsibility vary eith the model:
     - Saas: Content+Access Policies + Usage
     - Paas: Saas + Deployment + Web Application Security
     - Iaas: Paas + Operations + Networking Security + Guest OS
  
## GCP Managed Services for Compute:

| Service| Details|Category
|---------|--------|------|
| Compute Engine| High-Performance and general purpose VMs that scale globally | IaaS |
| Google Kubernetes Engine| Orchestrate containerized microservices on Kubernetes Needs advanced cluster configuration and monitoring | CaaS |
| App Engine| Build highly scalable applications on a fully managed platform using open and familiar languages and tools | Paas(CaaS, Serverless) |
| Cloud Functions | Build event driven applications using simple, single-purpose functions | Cloud Functions |
| Cloud Run | develop and deploy highly scalable containerized applications, Doesn't need a cluster | Caas(Serverless) | 


### APP Engine
It is a simplest way to deploy and scale your application in GCP
- Provides end-to- end application management
- Use custom run-time and can write code in any language
-  Connect to variety of GCP storage products(Cloud SQL, etc)
Features:
- automatic load balancing and Aut-scaling
- Managed platform updates and application helath monitoring
- Application versioning
- Traffic splitting

  For **Compute Engine**
   - IAAS
   - More flexibility
   - More responsibility
      - Choosing image
      - Installing Software
      - Choosing Hardware
      - Fine Grained Access/Permisions(Certifictaes/Firewalls)
      - Availability,etc
    FOr **App Engine**
  - Paas
  - Serverless
  - Lesser Responsibility
  - Lower flexibilty







