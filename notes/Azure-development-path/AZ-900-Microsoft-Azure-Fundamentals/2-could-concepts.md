# [Cloud concepts](https://learn.microsoft.com/en-us/training/paths/microsoft-azure-fundamentals-describe-cloud-concepts/)

## The Language of Cloud Computing

### High availability
When you’re deploying an application, a service, or any IT resources, it’s important the resources are available when needed. High availability focuses on ensuring maximum availability, regardless of disruptions or events that may occur.

When you’re architecting your solution, you’ll need to account for service availability guarantees. Azure is a highly available cloud environment with uptime guarantees depending on the service. These guarantees are part of the service-level agreements (SLAs).

https://bluexp.netapp.com/blog/azure-high-availability-basic-concepts-and-a-checklist

### Reliability
Reliability is the ability of a system to recover from failures and continue to function. It's also one of the pillars of the Microsoft Azure Well-Architected Framework.

The cloud, by virtue of its decentralized design, naturally supports a reliable and resilient infrastructure. With a decentralized design, the cloud enables you to have resources deployed in regions around the world. With this global scale, even if one region has a catastrophic event other regions are still up and running. You can design your applications to automatically take advantage of this increased reliability. In some cases, your cloud environment itself will automatically shift to a different region for you, with no action needed on your part. You’ll learn more about how Azure leverages global scale to provide reliability later in this series.

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

The other benefit of scalability is that you aren't overpaying for services. Because the cloud is a [consumption-based](./2-could-concepts.md#consumption-based-model) model, you only pay for what you use. If demand drops off, you can reduce your resources and thereby reduce your costs.

Scaling generally comes in two varieties: vertical and horizontal. Vertical scaling is focused on increasing or decreasing the capabilities of resources. Horizontal scaling is adding or subtracting the number of resources.

#### Scaling Out (Horizontal scaling)

With horizontal scaling, if you suddenly experienced a steep jump in demand, your deployed resources could be scaled out (either automatically or manually). For example, you could add additional virtual machines or containers, scaling out. In the same manner, if there was a significant drop in demand, deployed resources could be scaled in (either automatically or manually), scaling in.

- Incrase instace count of existing resources
- Incrasing the servers number to handle more request
- Non-disruptive

#### Scaling Up (Vertical scaling)

With vertical scaling, if you were developing an app and you needed more processing power, you could vertically scale up to add more CPUs or RAM to the virtual machine. Conversely, if you realized you had over-specified the needs, you could vertically scale down by lowering the CPU or RAM specifications.

- Incrase instace size of existing resource
- Get a bigger server: more CPU, RAM etc..
- Disruptive

#### Scaling down
Decrase instace size of existing resource

### Predicatability
Predictability includes transparent cost usage, including accurate forecasts on future costs based on current usage.

One aspect of predictability known that your application will consistently perform as expected even if user load increases. This is accomplished with cloud computing features such as load balancing, high availability, and autoscaling.

Predictability in the cloud lets you move forward with confidence. Predictability can be focused on performance predictability or cost predictability. Both performance and cost predictability are heavily influenced by the Microsoft Azure Well-Architected Framework. Deploy a solution that’s built around this framework and you have a solution whose cost and performance are predictable.

####  Performance
Performance predictability focuses on predicting the resources needed to deliver a positive experience for your customers. Autoscaling, load balancing, and high availability are just some cloud concepts that support performance predictability. If you suddenly need more resources, autoscaling can deploy additional resources to meet the demand, and then scale back when the demand drops. Or if the traffic is heavily focused on one area, load balancing will help redirect some overload to less stressed areas.

- Consistent experience for customers regardless of traffic
- Autoscaling, load balancing, and high availability provide a consistence experience

#### Costs
Cost predictability is focused on predicting or forecasting the cost of the cloud spend. With the cloud, you can track your resource use in real time, monitor resources to ensure that you’re using them in the most efficient way, and apply data analytics to find patterns and trends that help better plan resource deployments. By operating in the cloud and using cloud analytics and information, you can predict future costs and adjust your resources as needed. You can even use tools like the Total Cost of Ownership (TCO) or Pricing Calculator to get an estimate of potential cloud spend.

- No unexpected surprises
- Track and forecast resource usage (costs) in real time
- Analytics provide patterns/trends to optimize usage

### Governance
Whether you’re deploying infrastructure as a service or software as a service, cloud features support governance and compliance. Things like set templates help ensure that all your deployed resources meet corporate standards and government regulatory requirements. Plus, you can update all your deployed resources to new standards as standards change. Cloud-based auditing helps flag any resource that’s out of compliance with your corporate standards and provides mitigation strategies. Depending on your operating model, software patches and updates may also automatically be applied, which helps with both governance and security.

- Standardized environments
- regulatory requirements
- audit for compliance

Governance is all about standardization and compliance, which is especially useful for meeting corporate standards and/or meeting government regulations.

### Security
On the security side, you can find a cloud solution that matches your security needs. If you want maximum control of security, infrastructure as a service provides you with physical resources but lets you manage the operating systems and installed software, including patches and maintenance. If you want patches and maintenance taken care of automatically, platform as a service or software as a service deployments may be the best cloud strategies for you.

And because the cloud is intended as an over-the-internet delivery of IT resources, cloud providers are typically well suited to handle things like distributed denial of service (DDoS) attacks, making your network more robust and secure.

### Manageability
A major benefit of cloud computing is the manageability options. There are two types of manageability for cloud computing that you’ll learn about in this series, and both are excellent benefits.

#### Management of the cloud:
Management of the cloud speaks to managing your cloud resources. In the cloud, you can:
- Automatically scale resource deployment based on need.
- Monitor the health of resources and automatically replace failing resources.
- Deploy resources based on a preconfigured template, removing the need for manual configuration.
- Receive automatic alerts based on configured metrics, so you’re aware of performance in real time.

#### Management in the cloud
Management in the cloud speaks to how you’re able to manage your cloud environment and resources. You can manage these:
- Through a web portal. (Azure Portal)
- Using a command line interface. (CLI)
- Using APIs.
- Using PowerShell.

## The Language of Cloud Economics

### Capital and Operational Expenditure (Consumption-based model)
When comparing IT infrastructure models, there are two types of expenses to consider. Capital expenditure (CapEx) and operational expenditure (OpEx).

### Capital Expenditure (CapEx)
CapEx is typically a one-time, up-front expenditure to purchase or secure tangible resources. A new building, repaving the parking lot, building a datacenter, or buying a company vehicle are examples of CapEx.

- Money spent by a business or organisation on acquiring or maintaining fixed, such as land, buildings, and equipment.
- Ex: Buying more servers
- Large upfront investment.

### Operational Expenditure (OpEx)
In contrast, OpEx is spending money on services or products over time. Renting a convention center, leasing a company vehicle, or signing up for cloud services are all examples of OpEx.

- An ongoing cost of running a product, buisness, or system on a day-to-day basis, including annual costs
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

![image](https://user-images.githubusercontent.com/48266482/219339858-1586da84-3271-44e6-9286-28b39ba2abf3.png)

### Compare cloud pricing models
Cloud computing is the delivery of computing services over the internet by using a pay-as-you-go pricing model. You typically pay only for the cloud services you use, which helps you:

- Plan and manage your operating costs.
- Run your infrastructure more efficiently.
- Scale as your business needs change.

To put it another way, cloud computing is a way to rent compute power and storage from someone else’s datacenter. You can treat cloud resources like you would resources in your own datacenter. However, unlike in your own datacenter, when you're done using cloud resources, you give them back. You’re billed only for what you use.

Instead of maintaining CPUs and storage in your datacenter, you rent them for the time that you need them. The cloud provider takes care of maintaining the underlying infrastructure for you. The cloud enables you to quickly solve your toughest business challenges and bring cutting-edge solutions to your users.

## Cloud Service Models
![image](https://user-images.githubusercontent.com/48266482/217860079-e5b3f20d-4a9b-4a04-9126-93cd69d76a69.png)

### Infrastructure-as-a-Service (IaaS)
Infrastructure as a service (IaaS) is the most flexible category of cloud services, as it provides you the maximum amount of control for your cloud resources. In an IaaS model, the cloud provider is responsible for maintaining the hardware, network connectivity (to the internet), and physical security. You’re responsible for everything else: operating system installation, configuration, and maintenance; network configuration; database and storage configuration; and so on. With IaaS, you’re essentially renting the hardware in a cloud datacenter, but what you do with that hardware is up to you.

- Infrastructure = actual servers
- Scaling is fast
- No ownership of hardware

![image](https://user-images.githubusercontent.com/48266482/219362881-8565801e-0511-423e-bb89-a2e65172c140.png)

#### Shared responsibility model
The shared responsibility model applies to all the cloud service types. IaaS places the largest share of responsibility with you. The cloud provider is responsible for maintaining the physical infrastructure and its access to the internet. You’re responsible for installation and configuration, patching and updates, and security.

![image](https://learn.microsoft.com/en-us/training/wwl-azure/describe-cloud-service-types/media/shared-responsibility-b3829bfe.svg)

#### Scenarios
Some common scenarios where IaaS might make sense include:

- Lift-and-shift migration: You’re standing up cloud resources similar to your on-prem datacenter, and then simply moving the things running on-prem to running on the IaaS infrastructure.
- Testing and development: You have established configurations for development and test environments that you need to rapidly replicate. You can stand up or shut down the different environments rapidly with an IaaS structure, while maintaining complete control.

### Platfrom-as-a-Service
Platform as a service (PaaS) is a middle ground between renting space in a datacenter (infrastructure as a service) and paying for a complete and deployed solution (software as a service). In a PaaS environment, the cloud provider maintains the physical infrastructure, physical security, and connection to the internet. They also maintain the operating systems, middleware, development tools, and business intelligence services that make up a cloud solution. In a PaaS scenario, you don't have to worry about the licensing or patching for operating systems and databases.

PaaS is well suited to provide a complete development environment without the headache of maintaining all the development infrastructure.

- Superset of IaaS
- PaaS supports web application life cycle
- Avoid software license hell

![image](https://user-images.githubusercontent.com/48266482/219363567-6a6f87bd-39c1-4c33-84bd-93229262676b.png)

#### Shared responsibility model
The shared responsibility model applies to all the cloud service types. PaaS splits the responsibility between you and the cloud provider. The cloud provider is responsible for maintaining the physical infrastructure and its access to the internet, just like in IaaS. In the PaaS model, the cloud provider will also maintain the operating systems, databases, and development tools. Think of PaaS like using a domain joined machine: IT maintains the device with regular updates, patches, and refreshes.

Depending on the configuration, you or the cloud provider may be responsible for networking settings and connectivity within your cloud environment, network and application security, and the directory infrastructure.

![image](https://learn.microsoft.com/en-us/training/wwl-azure/describe-cloud-service-types/media/shared-responsibility-b3829bfe.svg)

#### Scenarios
Some common scenarios where PaaS might make sense include:

- Development framework: PaaS provides a framework that developers can build upon to develop or customize cloud-based applications. Similar to the way you create an Excel macro, PaaS lets developers create applications using built-in software components. Cloud features such as scalability, high-availability, and multi-tenant capability are included, reducing the amount of coding that developers must do.
- Analytics or business intelligence: Tools provided as a service with PaaS allow organizations to analyze and mine their data, finding insights and patterns and predicting outcomes to improve forecasting, product design decisions, investment returns, and other business decisions.

### Software-as-a-Service
Software as a service (SaaS) is the most complete cloud service model from a product perspective. With SaaS, you’re essentially renting or using a fully developed application. Email, financial software, messaging applications, and connectivity software are all common examples of a SaaS implementation.

While the SaaS model may be the least flexible, it’s also the easiest to get up and running. It requires the least amount of technical knowledge or expertise to fully employ.

- Providing a managed service
- Pay an access fee to use
- No maintenancet and latest features

![image](https://user-images.githubusercontent.com/48266482/219363985-eae7d422-d34f-4ab3-a933-c8941749d3ea.png)

#### Shared responsibility model
The shared responsibility model applies to all the cloud service types. SaaS is the model that places the most responsibility with the cloud provider and the least responsibility with the user. In a SaaS environment you’re responsible for the data that you put into the system, the devices that you allow to connect to the system, and the users that have access. Nearly everything else falls to the cloud provider. The cloud provider is responsible for physical security of the datacenters, power, network connectivity, and application development and patching.

![image](https://learn.microsoft.com/en-us/training/wwl-azure/describe-cloud-service-types/media/shared-responsibility-b3829bfe.svg)

#### Scenarios
Some common scenarios for SaaS are:

- Email and messaging.
- Business productivity applications.
- Finance and expense tracking.

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
- Serverless means that you don't have any servers. Let a single function be hosted, deployed, run and managed on its own

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
