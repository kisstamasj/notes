# [Cloud concepts](https://learn.microsoft.com/en-us/training/paths/microsoft-azure-fundamentals-describe-cloud-concepts/)

## The Language of Cloud Computing

### High availability
When you’re deploying an application, a service, or any IT resources, it’s important the resources are available when needed. High availability focuses on ensuring maximum availability, regardless of disruptions or events that may occur.

When you’re architecting your solution, you’ll need to account for service availability guarantees. Azure is a highly available cloud environment with uptime guarantees depending on the service. These guarantees are part of the service-level agreements (SLAs).

https://bluexp.netapp.com/blog/azure-high-availability-basic-concepts-and-a-checklist

### Reliability

> a.k.a Fault Tolearance/Disaster recovery

- Resilience: The ability of a system to recover from failures and continue to function
- Deploy in multiple locations:
  - Global-scale computing
  - Protects agains regional failures/disaster
- No single point of failure
  - Resource in multiple locations
  - If one computer goes down, others pick up the load

Reliability means a failure can occur on Azure services and applications, but it will not affect its availability.

### Scalability
Another major benefit of cloud computing is the scalability of cloud resources. Scalability refers to the ability to adjust resources to meet demand. If you suddenly experience peak traffic and your systems are overwhelmed, the ability to scale means you can add more resources to better handle the increased demand.

The other benefit of scalability is that you aren't overpaying for services. Because the cloud is a [consumption-based]() model, you only pay for what you use. If demand drops off, you can reduce your resources and thereby reduce your costs.

Scaling generally comes in two varieties: vertical and horizontal. Vertical scaling is focused on increasing or decreasing the capabilities of resources. Horizontal scaling is adding or subtracting the number of resources.

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
Predictability includes transparent cost usage, including accurate forecasts on future costs based on current usage.

One aspect of predictability is knowing that your application will consistently perform as expected even if user load increases. This is accomplished with cloud computing features such as load balancing, high availability, and autoscaling.

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

Governance is all about standardization and compliance, which is especially useful for meeting corporate standards and/or meeting government regulations.

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

### Capital and Operational Expenditure (Consumption-based model)
When comparing IT infrastructure models, there are two types of expenses to consider. Capital expenditure (CapEx) and operational expenditure (OpEx).

#### Capital Expenditure (CapEx)
CapEx is typically a one-time, up-front expenditure to purchase or secure tangible resources. A new building, repaving the parking lot, building a datacenter, or buying a company vehicle are examples of CapEx.

- Money spent by a business or organisation on acquiring or maintaining fixed, such as land, buildings, and equipment.
- Ex: Buying more servers
- Large upfront investment.

#### Operational Expenditure (OpEx)
In contrast, OpEx is spending money on services or products over time. Renting a convention center, leasing a company vehicle, or signing up for cloud services are all examples of OpEx.

- An ongoing cost of running a product,  buisness, or system on a day-to-day basis, including annual costs
- Ex: The power that could be the power to run the server.
- Pay-as-you-go

### Difference between CapEx and OpEx
Knowing the difference between OpEx and CapEx is critical to get the best value out of Azure for your company. Capital expenditures (CapEx) generally result in the acquisition and maintenance of assets, such as server hardware. Operating expenditures (OpEx) are the ongoing costs of running a business, such as paying for cloud services on a recurring basis. By moving costs to OpEx, businesses can plan for ongoing costs rather than large investments.

Cloud computing falls under OpEx because cloud computing operates on a consumption-based model. With cloud computing, you don’t pay for the physical infrastructure, the electricity, the security, or anything else associated with maintaining a datacenter. Instead, you pay for the IT resources you use. If you don’t use any IT resources this month, you don’t pay for any IT resources.

This consumption-based model has many benefits, including:

- No upfront costs.
- No need to purchase and manage costly infrastructure that users might not use to its fullest potential.
- The ability to pay for more resources when they're needed.
- The ability to stop paying for resources that are no longer needed.

With a traditional datacenter, you try to estimate the future resource needs. If you overestimate, you spend more on your datacenter than you need to and potentially waste money. If you underestimate, your datacenter will quickly reach capacity and your applications and services may suffer from decreased performance. Fixing an under-provisioned datacenter can take a long time. You may need to order, receive, and install more hardware. You'll also need to add power, cooling, and networking for the extra hardware.

In a cloud-based model, you don’t have to worry about getting the resource needs just right. If you find that you need more virtual machines, you add more. If the demand drops and you don’t need as many virtual machines, you remove machines as needed. Either way, you’re only paying for the virtual machines that you use, not the “extra capacity” that the cloud provider has on hand.

### Cloud pricing models
![image](https://user-images.githubusercontent.com/48266482/219339858-1586da84-3271-44e6-9286-28b39ba2abf3.png)

#### Consumption-based Model
You pay:
- Per Execution
- Per Second
- Combination

Low usage = Low cost

#### Compare cloud pricing models
Cloud computing is the delivery of computing services over the internet by using a pay-as-you-go pricing model. You typically pay only for the cloud services you use, which helps you:

- Plan and manage your operating costs.
- Run your infrastructure more efficiently.
- Scale as your business needs change.

To put it another way, cloud computing is a way to rent compute power and storage from someone else’s datacenter. You can treat cloud resources like you would resources in your own datacenter. However, unlike in your own datacenter, when you're done using cloud resources, you give them back. You’re billed only for what you use.

Instead of maintaining CPUs and storage in your datacenter, you rent them for the time that you need them. The cloud provider takes care of maintaining the underlying infrastructure for you. The cloud enables you to quickly solve your toughest business challenges and bring cutting-edge solutions to your users.

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

Start with a traditional corporate datacenter. The company is responsible for maintaining the physical space, ensuring security, and maintaining or replacing the servers if anything happens. The IT department is responsible for maintaining all the infrastructure and software needed to keep the datacenter up and running. They’re also likely to be responsible for keeping all systems patched and on the correct version.

With the shared responsibility model, these responsibilities get shared between the cloud provider and the consumer. Physical security, power, cooling, and network connectivity are the responsibility of the cloud provider. The consumer isn’t collocated with the datacenter, so it wouldn’t make sense for the consumer to have any of those responsibilities.

At the same time, the consumer is responsible for the data and information stored in the cloud. (You wouldn’t want the cloud provider to be able to read your information.) The consumer is also responsible for access security, meaning you only give access to those who need it.

Then, for some things, the responsibility depends on the situation. If you’re using a cloud SQL database, the cloud provider would be responsible for maintaining the actual database. However, you’re still responsible for the data that gets ingested into the database. If you deployed a virtual machine and installed an SQL database on it, you’d be responsible for database patches and updates, as well as maintaining the data and information stored in the database.

With an on-premises datacenter, you’re responsible for everything. With cloud computing, those responsibilities shift. The shared responsibility model is heavily tied into the cloud service types (covered later in this learning path): infrastructure as a service (IaaS), platform as a service (PaaS), and software as a service (SaaS). IaaS places the most responsibility on the consumer, with the cloud provider being responsible for the basics of physical security, power, and connectivity. On the other end of the spectrum, SaaS places most of the responsibility with the cloud provider. PaaS, being a middle ground between IaaS and SaaS, rests somewhere in the middle and evenly distributes responsibility between the cloud provider and the consumer.

The following diagram highlights how the Shared Responsibility Model informs who is responsible for what, depending on the cloud service type.

![image](https://learn.microsoft.com/hu-hu/training/wwl-azure/describe-cloud-compute/media/shared-responsibility-b3829bfe.svg)

You’ll always be responsible for:

- The information and data stored in the cloud
- Devices that are allowed to connect to your cloud (cell phones, computers, and so on)
- The accounts and identities of the people, services, and devices within your organization

The cloud provider is always responsible for:

- The physical datacenter
- The physical network
- The physical hosts

Your service model will determine responsibility for things like:

- Operating systems
- Network controls
- Applications
- Identity and infrastructure

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
Microsoft defines private clouds as being able to be hosted at your datacenter or hosted by a third-party service. Microsoft considers private clouds as offering more flexibility, control, and scalability. Note: Other cloud vendors would not agree with those advantages of private clouds, but it is best to be aware of Microsoft's view in case it comes up on the exam.

A private cloud consists of cloud computing resources used exclusively by one business or organization. The private cloud can be physically located at your organization’s on-site datacenter, or it can be hosted by a third-party service provider. But in a private cloud, the services and infrastructure are always maintained on a private network, and the hardware and software are dedicated solely to your organization.

Microsoft defines hybrid cloud as combining a public cloud (such as Azure) with on-premises infrastructure (private cloud).

![image](https://user-images.githubusercontent.com/48266482/219373937-654a6a82-09a9-4e06-a145-c0ef27a78b3f.png)

### Public Cloud
A public cloud is built, controlled, and maintained by a third-party cloud provider. With a public cloud, anyone that wants to purchase cloud services can access and use resources. The general public availability is a key difference between public and private clouds.

![image](https://user-images.githubusercontent.com/48266482/219374242-fb435926-f377-4dd3-bac5-87f0269f2098.png)

### Hybrid Cloud
Microsoft defines hybrid cloud as combining a public cloud (such as Azure) with on-premises infrastructure (private cloud).

A private cloud consists of cloud computing resources used exclusively by one business or organization. The private cloud can be physically located at your organization’s on-site datacenter, or it can be hosted by a third-party service provider. But in a private cloud, the services and infrastructure are always maintained on a private network, and the hardware and software are dedicated solely to your organization.

Microsoft defines private clouds as being able to be hosted at your datacenter or hosted by a third-party service. Microsoft considers private clouds as offering more flexibility, control, and scalability. Note: Other cloud vendors would not agree with those advantages of private clouds, but it is best to be aware of Microsoft's view in case it comes up on the exam.

![image](https://user-images.githubusercontent.com/48266482/219374502-6ebce696-00b1-43b2-8f21-f6b7a75579ee.png)

### Multi-cloud
A fourth, and increasingly likely scenario is a multi-cloud scenario. In a multi-cloud scenario, you use multiple public cloud providers. Maybe you use different features from different cloud providers. Or maybe you started your cloud journey with one provider and are in the process of migrating to a different provider. Regardless, in a multi-cloud environment you deal with two (or more) public cloud providers and manage resources and security in both environments.

### Azure Arc
Azure Arc is a set of technologies that helps manage your cloud environment. Azure Arc can help manage your cloud environment, whether it's a public cloud solely on Azure, a private cloud in your datacenter, a hybrid configuration, or even a multi-cloud environment running on multiple cloud providers at once.

### Azure VMware Solution
What if you’re already established with VMware in a private cloud environment but want to migrate to a public or hybrid cloud? Azure VMware Solution lets you run your VMware workloads in Azure with seamless integration and scalability.

### Exam Tips
**Choose your cloud architecture model wisly**

- Private cloud is Azure on your own hardware in a location of your choice. All the benefits of puvlic cloud, but you can lock it down. A lot of staff required.
- Public cloud is Azure, AWS, GCP. Nu upfront costs, but monthly usage. Little control over services and infrastucture.
- A hybrid cloud model is the best of private and public, but could be complex
