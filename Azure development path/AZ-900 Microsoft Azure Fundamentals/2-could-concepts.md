# Cloud concepts

## The Language of Cloud Computing

### High availability
- Core to the cloud
- you don't own the hardware
- add more servers with a click
- If hardware fails, replace it instantly
- Use clusters to ensure high availability

### Reliability

> a.k.a Fault Tolearance/Disaster recovery

- Resilience: The ability of a system to recover from failures and continue to function
- Deploy in multiple locations:
  - Global-scale computing
  - Protects agains regional failures/disaster
- No single point of failure
  - Resource in multiple locations
  - If one computer goes down, others pick up the load

### Scalability
Scalability is the process of adding more resource on an as-needed basis.
- Scaling Out (Horizontal scaling)
  - Incrase instace count of existing resources
  - Incrasing the servers number to handle more request
  - Non-disruptive
- Scaling Up (Vertical scaling)
  - Incrase instace size of existing resource
  - Get a bigger server: more CPU, RAM etc..
  - Disruptive
- Scaling down
  - Decrase instace size of existing resource

### Predicatability
Predictable performance and costs

- Performance
  - Consistent experience for customers regardless of traffic
  - Autoscaling, load balancing, and high availability provide a consistence experience
- Costs
  - No unexpected surprises
  - Track and forecast resource usage (costs) in real time
  - Analytics provide patterns/trends to optimize usage

### Security
Full control of the security of your cloud environment. Patches, maintenance, network control, and more.

### Governance
Is standardizing cloud deployments to meet requirements/compony standards
- Standardized environments
- regulatory requirements
- audit for compliance

### Manageability
- Management of the cloud:
  - Autoscaling
  - Monitoring
  - Templage-based deployments
- Management in the cloud
  - Portal
  - CLI
  - APIs

## The Language of Cloud Economics

### Capital and Operational Expenditure

#### Capital Expenditure (CapEx)
- Money spent by a business or organisation on acquiring or maintaining fixed, such as land, buildings, and equipment.
- Ex: Buying more servers
- Large upfront investment.

#### Operational Expenditure (OpEx)
- An ongoing cost of running a product,  buisness, or system on a day-to-day basis, including annual costs
- Ex: The power that could be the power to run the server.
- Pay-as-you-go

### Cloud pricing models
![image](https://user-images.githubusercontent.com/48266482/219339858-1586da84-3271-44e6-9286-28b39ba2abf3.png)

#### Consumption-based Pricing
You pay:
- Per Execution
- Per Second
- Combination

Low usage = Low cost

## Cloud Service Models
![image](https://user-images.githubusercontent.com/48266482/217860079-e5b3f20d-4a9b-4a04-9126-93cd69d76a69.png)

### Infrastructure-as-a-Service (IaaS)
Infrastructure as a service (IaaS) is a type of cloud computing service that offers essential compute, storage, and networking resources on demand, on a pay-as-you-go basis. IaaS lets you bypass the cost and complexity of buying and managing physical servers and datacenter infrastructure. Each resource is offered as a separate service component, and you only pay for a particular resource for as long as you need it.

- Infrastructure = actual servers
- Scaling is fast
- No ownership of hardware

![image](https://user-images.githubusercontent.com/48266482/219362881-8565801e-0511-423e-bb89-a2e65172c140.png)

### Platfrom-as-a-Service
- Superset of IaaS
- PaaS supports web application life cycle
- Avoid software license hell

![image](https://user-images.githubusercontent.com/48266482/219363567-6a6f87bd-39c1-4c33-84bd-93229262676b.png)

### Software-as-a-Service
- Providing a managed service
- Pay an access fee to use
- No maintenancet and latest features

![image](https://user-images.githubusercontent.com/48266482/219363985-eae7d422-d34f-4ab3-a933-c8941749d3ea.png)

### Serverless
- Of course there are servers!
- Azure Functions is the best known serverless service
- Extreme PaaS

![image](https://user-images.githubusercontent.com/48266482/219364265-78ddb4f0-bc00-4de6-b104-a078ca3cc34f.png)

### Identifying Cloud Service Models
![image](https://user-images.githubusercontent.com/48266482/219364364-f69e4f79-6e50-4b7e-bc4a-9281f9a87443.png)

### Shared Responsibility Model
![image](https://user-images.githubusercontent.com/48266482/219366346-a5da7611-cbda-4318-9210-f5b6a655c6b8.png)

### Exam Tips
**Service is the core of Azure, and there are three main ways to go about it.**

- IaaS provides servers, storage and networking as a service
- PaaS is a superset of IaaS and also includes middleware, such as database management tools
- SaaS is when a service is built on top of PaaS, like Office 365
- Serverless means that you don't have any servers. Let's a single function be hosted, deployed, run and managed on its own

## Azure Marketplace
- Solutions and Services
  - Large selection from Microsoft and partners. Apps, VMs, templates, services and much more.
- Azure App store
  - Buy cloud services with a single click (almost). Many categories of itmes to acquire.
- Easy to Integrate
  - Use from Portal, Cli or PowerShell. Some are free, some are paid.
- Publish Your Own
  - If you are a Microsoft Partner, publish your own services in the Marketplace.

### Benefits
- Certified and less maintenance
  - Less maintenance than creating your own service or application from scratch. All Marketplace offerings are certified by Microsoft.
- Efficient
  - It is much faster to build a project prototype by using ready-to-go services on the Marketplace
- New Markets 
  - You can venture into new markets by getting the full exposure of the Marketplace
- Suppert
  - There is both technical, design and architectural design support available when you list a service on the Marketplace.

## Cloud Architecture Models
### Private Cloud
![image](https://user-images.githubusercontent.com/48266482/219373937-654a6a82-09a9-4e06-a145-c0ef27a78b3f.png)

### Public Cloud
![image](https://user-images.githubusercontent.com/48266482/219374242-fb435926-f377-4dd3-bac5-87f0269f2098.png)

### Hybrid Cloud
Microsoft defines hybrid cloud as combining a public cloud (such as Azure) with on-premises infrastructure (private cloud).

A private cloud consists of cloud computing resources used exclusively by one business or organization. The private cloud can be physically located at your organization’s on-site datacenter, or it can be hosted by a third-party service provider. But in a private cloud, the services and infrastructure are always maintained on a private network, and the hardware and software are dedicated solely to your organization. Reference: What is a private cloud?

Microsoft defines private clouds as being able to be hosted at your datacenter or hosted by a third-party service. Microsoft considers private clouds as offering more flexibility, control, and scalability. Note: Other cloud vendors would not agree with those advantages of private clouds, but it is best to be aware of Microsoft's view in case it comes up on the exam.

![image](https://user-images.githubusercontent.com/48266482/219374502-6ebce696-00b1-43b2-8f21-f6b7a75579ee.png)

### Exam Tips
**Choose your cloud architecture model wisly**

- Private cloud is Azure on your own hardware in a location of your choice. All the benefits of puvlic cloud, but you can lock it down. A lot of staff required.
- Public cloud is Azure, AWS, GCP. Nu upfront costs, but monthly usage. Little control over services and infrastucture.
- A hybrid cloud model is the best of private and public, but could be complex




