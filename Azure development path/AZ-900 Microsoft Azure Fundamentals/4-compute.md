# [Compute](https://learn.microsoft.com/hu-hu/training/modules/azure-compute-fundamentals/?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

## Virtual Machines (VMs)
Virtual machines are software emulations of physical computers. They include a virtual processor, memory, storage, and networking resources. VMs host an operating system, and you can install and run software just like a physical computer. When using a remote desktop client, you can use and control the VM as if you were sitting in front of it.

With Azure Virtual Machines, you can create and use VMs in the cloud. Virtual Machines provides infrastructure as a service (IaaS) and can be used in different ways. When you need total control over an operating system and environment, VMs are an ideal choice. Just like a physical computer, you can customize all the software running on the VM. This ability is helpful when you're running custom software or custom hosting configurations.

![image](https://user-images.githubusercontent.com/48266482/219572969-0af6cc89-389e-40d2-98b5-19be2428a082.png)

### Features
- **Infrastructure-as-a-Service (IaaS):** Manage everything except the hardware. This includes the networking components.
- **Tools:** Use the Azure Portal to manage large numbers of VMs and even hybrid clouds.
- **Compliance:** Use Azure blueprints to make your VMs comply with a company guidlines
- **Recommendations:** Azure will recommend improvements to ensure better scurity, higher availability and greater performance.
- **Choice:**: Choose amount of RAM, number of CPUs, Windows or Linux
- There are new virtual machines with dedicated GPUs for artificial intelligence and deep learning scenarios.
- 

### Pricing
- Calculated hourly
- Depends on the amount of resources

### Use Cases
- **Pros**:
  - **Control**: Use virtual machines when you need to control all aspects of an environment or machine. (OS, hosting configurations etc..)
  - **Application**: Install specific applications on your Windows or Linux machines
  - **Existing infrastructure**: You can move existing resources and virtual machines to Azure from on-premises or another cloud provider.
- **Cons**:
  - **Not for everything**: If you can use another Azure service instead, it is often worth it.
  -  **Maintenance**: A lot of maintenance with VMs. Operating system updates, patches, security concerns.

### Examples of when to use VMs
- **During testing and development**. VMs provide a quick and easy way to create different OS and application configurations. Test and development personnel can then easily delete the VMs when they no longer need them.
- **When running applications in the cloud**. The ability to run certain applications in the public cloud as opposed to creating a traditional infrastructure to run them can provide substantial economic benefits. For example, an application might need to handle fluctuations in demand. Shutting down VMs when you don't need them or quickly starting them up to meet a sudden increase in demand means you pay only for the resources you use.
- **When extending your datacenter to the cloud**. An organization can extend the capabilities of its own on-premises network by creating a virtual network in Azure and adding VMs to that virtual network. Applications like SharePoint can then run on an Azure VM instead of running locally. This arrangement makes it easier or less expensive to deploy than in an on-premises environment.
- **During disaster recovery**. As with running certain types of applications in the cloud and extending an on-premises network to the cloud, you can get significant cost savings by using an IaaS-based approach to disaster recovery. If a primary datacenter fails, you can create VMs running on Azure to run your critical applications and then shut them down when the primary datacenter becomes operational again.
  
### Exam tips
Virtual Machines are at the core of Azure compute and are widely used.
- A virtual machine is your machine exclusivly.
- You don't buy, own or control any hardware. Azure does this.
- Virtual machines are an IaaS offering, where you are responsible for the entire machine.
- Azure virtual machines take advantage of Azure tools.
- Pricing goes up as resources go up, and you pay by the hour.

## Scale Sets
Virtual machine scale sets are an Azure compute resource that you can use to deploy and manage a set of identical VMs. With all VMs configured the same, virtual machine scale sets are designed to support true autoscale. No pre-provisioning of VMs is required. For this reason, it's easier to build large-scale services targeting big compute, big data, and containerized workloads. As demand goes up, more VM instances can be added. As demand goes down, VM instances can be removed. The process can be manual, automated, or a combination of both.

## App Services
With Azure App Service, you can quickly build, deploy, and scale enterprise-grade web, mobile, and API apps running on any platform. You can meet rigorous performance, scalability, security, and compliance requirements while using a fully managed platform to perform infrastructure maintenance. App Service is a platform as a service (PaaS) offering.

## Azure Container Instances
Container Instances and Azure Kubernetes Service are Azure compute resources that you can use to deploy and manage containers. Containers are lightweight, virtualized application environments. They're designed to be quickly created, scaled out, and stopped dynamically. You can run multiple instances of a containerized application on a single host machine.

## Azure Kubernetes Services

## Windows Virtual Desktop

## Functions
Functions are ideal when you're concerned only about the code running your service and not the underlying platform or infrastructure. They're commonly used when you need to perform work in response to an event (often via a REST request), timer, or message from another Azure service, and when that work can be completed quickly, within seconds or less.
