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
Virtual machine scale sets are an Azure compute resource that you can use to deploy and manage a set of identical VMs. With all VMs configured the same, virtual machine scale sets are designed to support true autoscale. No pre-provisioning of VMs is required. For this reason, it's easier to build large-scale services targeting big compute, big data, and containerized workloads. As demand goes up, more VM instances can be added. As demand goes down, VM instances can be removed. The process can be manual, automated, or a combination of both (schedule the scaling). 

![image](https://user-images.githubusercontent.com/48266482/219665789-86139135-90d6-4403-85bc-c4bec5065f51.png)

### Benefits
- **Multiple VMs**: Simple multiple identical VMs using a load balancer.
- **High Availability**: If one VM fails or stops, the others in the scale set will keep working.
- **Auto Scaling**: Automatically match demand by adding or removing VMs from the scale set.
- **Large Scale**: Run up to 1000 VMs in a single scale set.
- **No extra cost**: No added cost for using scale sets.

### Use Cases
Intermittent load.

### Exam tips
Scale sets are taking virtual machines to the next level. And keeping your sanity.
- Scale sets are identical VMs. They can be activated or deactivated as needed.
- A baseline VM for the scale set ensures application stability. A baseline VM is what you copy to make up the scale set VMs.
- As resource usage increases, more VMs are activated to take the load.
- You only pay for the VM, storage and networking resources you use. Nothing addittional for scale sets.

## App Services
With Azure App Service, you can quickly build, deploy, and scale enterprise-grade web, mobile, and API apps running on any platform. You can meet rigorous performance, scalability, security, and compliance requirements while using a fully managed platform to perform infrastructure maintenance. App Service is a platform as a service (PaaS) offering.
App Service enables you to build and host web apps, background jobs, mobile back-ends, and RESTful APIs in the programming language of your choice without managing infrastructure. It offers automatic scaling and high availability. App Service supports Windows and Linux and enables automated deployments from GitHub, Azure DevOps, or any Git repo to support a continuous deployment model.
This platform as a service (PaaS) environment allows you to focus on the website and API logic while Azure handles the infrastructure to run and scale your web applications.

![image](https://user-images.githubusercontent.com/48266482/219681031-9ab09aee-0bd3-4b80-9969-347e8e1a3274.png)

### Azure App Service costs
You pay for the Azure compute resources your app uses while it processes requests based on the App Service plan you choose. The App Service plan determines how much hardware is devoted to your host. For example, the plan determines whether it's dedicated or shared hardware and how much memory is reserved for it. There's even a free tier you can use to host small, low-traffic sites.

### Types of app services
With App Service, you can host most common app service styles like:

- Web apps
- Web Apps for Containers
- API apps
- WebJobs
- Mobile apps

App Service handles most of the infrastructure decisions you deal with in hosting web-accessible apps:

- Deployment and management are integrated into the platform.
- Endpoints can be secured.
- Sites can be scaled quickly to handle high traffic loads.
- The built-in load balancing and traffic manager provide high availability.

All of these app styles are hosted in the same infrastructure and share these benefits. This flexibility makes App Service the ideal choice to host web-oriented applications.

#### Web Apps
Website and online applications hosted on Azure's managed platform.
- Runs on both Windows and Linux platforms
- Supports a lot of languages, such as .NET Core, JAVA, Node.js, PHP, Python and Ruby
- Azure integration for easier deployment
- Auto-scaling and load balancing

#### Web Apps for containers
Deploy and run containerized applications in Azure
- Container is completaly self-contained
- All dependencies are shipped inside the container
- Deploy anywhere with a consistent experience
- Reliable between environments

#### API Apps
Expose and connect your data backend
- Application Programming Interface
- No graphical component. No user interface
- Connect other applications programmatically
- Use a ranage of programming languages

#### WebJobs
You can use the WebJobs feature to run a program (.exe, Java, PHP, Python, or Node.js) or script (.cmd, .bat, PowerShell, or Bash) in the same context as a web app, API app, or mobile app. They can be scheduled or run by a trigger. WebJobs are often used to run background tasks as part of your application logic.

#### Mobile apps
Use the Mobile Apps feature of App Service to quickly build a back end for iOS and Android apps. With just a few clicks in the Azure portal, you can:

- Store mobile app data in a cloud-based SQL database.
- Authenticate customers against common social providers, such as MSA, Google, Twitter, and Facebook.
- Send push notifications.
- Execute custom back-end logic in C# or Node.js.

On the mobile app side, there's SDK support for native iOS and Android, Xamarin, and React native apps.

### Exam tips
App services is an easy way to host and manage your web application.
- App services are a PaaS offering on Azure
- Web Apps are used to host web sites and web applications.
- Web Apps for Containers can host your existing container images.
- API Apps can host your data backend services

## Azure Container Instances (ACI)
Container Instances and Azure Kubernetes Service are Azure compute resources that you can use to deploy and manage containers. Containers are lightweight, virtualized application environments. They're designed to be quickly created, scaled out, and stopped dynamically. You can run multiple instances of a containerized application on a single host machine. Useful when your application or software designed with different component, such as multiple Node.JS service, Redis in memory database or SQL database as well.

### What are Containers?
Containers are a virtualization environment. Much like running multiple virtual machines on a single physical host, you can run multiple containers on a single physical or virtual host. Unlike virtual machines, you don't manage the operating system for a container. Virtual machines appear to be an instance of an operating system that you can connect to and manage, but containers are lightweight and designed to be created, scaled out, and stopped dynamically. While it's possible to create and deploy virtual machines as application demand increases, containers are designed to allow you to respond to changes on demand. With containers, you can quickly restart in case of a crash or hardware interruption. One of the most popular container engines is Docker, which is supported by Azure.

> VM vs Container: VM virtualize the computer while Container virtualize the OS. Virtual Machine needs much more power and resource like containers. Containers are lightweight virtualization solutions.

### Features
- **Manage Application Dependencies**: All the dependencies for an application are included in the container image. You can manage the application and its dependencies with confidence.
- **Less Overhead**: Virtual machines required a lot more maintenance and updates. Containers don't have any components relating to the operating system tahe require maintenace.
- **Increased Portability**: Applications running in containers can be deployed easily to multiple differen operating systems and hardware platforms.
- **Efficiency**: Development, deployment and maintenance are all more efficient when using containers. Scaling and patching is much simpler.
- **Consistency**: The operations team can rely on containers being the same every time, no matter which target they are being deployed to.

### Workflow
1. Develop your software
2. Build container image
3. Deploy to Azure Container Instances

## Azure Kubernetes Services (AKS)
The task of automating, managing, scaling and interacting with a large number of containers is known as orchestration. Azure Kubernetes Service is a complete orchestration service for containers with distributed architectures and large volumes of containers. Kubernetes is open-source.

- **Open source**: Public code base and community involvment in the product.
- **Orchestration**: Keeps track of lots of parts of a system. Makes sure containers are configured correctly to work together.
- **Automatic application deployment**: Kubernetes will deploy more images of containers as needed.
- **Automatic scaling**: Automatic monitoring of application load to determine when to scale the number of containers used.

### Features
- **Replicate Containers Architectures**: Reuse your container architecture by managing it in Kubernetes. This makes your setup yuicker and confidence in the system increase
- **Standard Azure Services Included**: You don't have to worry about infrastructure and hardware. Get identity access management, elastic provisioning and much more.
- **Global Reach**: Use Kubernetes with supported Azure regions and on-premises installations using Azure Stack.á

### Azure Container Registry (ACR)
- Keep track of the current valid container images
- Manages files and artifacts for containers
- Feeds container images to ACI and AKs
- Use Azure identify and security features

![image](https://user-images.githubusercontent.com/48266482/219695471-277734cd-f0fa-4f14-b0a4-3228b42353ac.png)

## Windows Virtual Desktop

## Functions
Functions are ideal when you're concerned only about the code running your service and not the underlying platform or infrastructure. They're commonly used when you need to perform work in response to an event (often via a REST request), timer, or message from another Azure service, and when that work can be completed quickly, within seconds or less.
