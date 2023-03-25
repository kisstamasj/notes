# Monitoring and Management

## Governance

### Azure Policy
Governance validates that your organization can achieve its goals through effective and efficient us of IT. 
The plocies are set of rules.

### Role-Based Access Control (RBAC)
- **Define user access**: You can define specific user access to individual resources.
- **Minimum access**: RBAC enable minimum access necessary to resources. This ensures only users with valid access can manage resources.
- **Target specifc use cases**: Be very explicit about uses and access. For example, allow an application access to certain resources or allow a user to manage resources in a resource group.

![image](https://user-images.githubusercontent.com/48266482/227698157-630c3ef4-cf7c-45ed-932e-e8edd8a2c19e.png)

![image](https://user-images.githubusercontent.com/48266482/227698177-3041ff0d-122b-44a8-8bbf-8f9360af4630.png)

### Locks
- **Assigning**: Assign a lock to a subscription, resource group or resource.
- **Types**: A lock can be of two types. Delete where you can't delete the locked object. Read-Only, where you can't make any changes to the object.
- **Locked means locked**: A lock needs to be removed before the locked actions can be performed again.

### Azure Blueprints
Blueprints are templates for creating Azure resources.

![image](https://user-images.githubusercontent.com/48266482/227698362-15b520fc-f874-482f-87ca-e0695e40db15.png)

### Cloud adoption framework
- **Collection of Documents**: Lots of resources to guide you through the cloud adoption process.
- **Guidance**: Help to define strategies for adoption, planning the move, "being ready" for the cloud, adoption reason, governance practices, and managing a living, breathing cloud architecture.
- **Governance**: Key to the cloud adoption process is governance of the process. The Cloud Adoption Framework is a big step in that process.

### Exam tips:
Governance keeps you compliant and out of trouble.

- Azure Policy ensures that policies applied to resources are compliant.
- A policy is a set of rules to ensure compliant resources.
- Role Based Access Control (RBAC) ensures user compliance through assigning a role to a user. A role is a combination of security principal, role definition and scope.
- Locks make sure that subscriptions, resource groups or resources are either not modified or not deleted.
- Blueprints are templates for creating standard Azure environments.
- The Azure Advisor for Security Assistance is part of the Security Center.

## Azure Monitor
Azure Monitor is a platform for collecting data on your resources, analyzing that data, visualizing the information, and even acting on the results. Azure Monitor can monitor Azure resources, your on-premises resources, and even multi-cloud resources like virtual machines hosted with a different cloud provider.

The following diagram illustrates just how comprehensive Azure Monitor is:

![image](https://user-images.githubusercontent.com/48266482/227698687-dd3f7cd7-4958-4215-a468-b93761f84126.png)

On the left is a list of the sources of logging and metric data that can be collected at every layer in your application architecture, from application to operating system and network.

In the center, the logging and metric data are stored in central repositories.

On the right, the data is used in several ways. You can view real-time and historical performance across each layer of your architecture or aggregated and detailed information. The data is displayed at different levels for different audiences. You can view high-level reports on the Azure Monitor Dashboard or create custom views by using Power BI and Kusto queries.

Additionally, you can use the data to help you react to critical events in real time, through alerts delivered to teams via SMS, email, and so on. Or you can use thresholds to trigger autoscaling functionality to scale to meet the demand.

### Azure Log Analytics
Azure Log Analytics is the tool in the Azure portal where you’ll write and run log queries on the data gathered by Azure Monitor. Log Analytics is a robust tool that supports both simple, complex queries, and data analysis. You can write a simple query that returns a set of records and then use features of Log Analytics to sort, filter, and analyze the records. You can write an advanced query to perform statistical analysis and visualize the results in a chart to identify a particular trend. Whether you work with the results of your queries interactively or use them with other Azure Monitor features such as log query alerts or workbooks, Log Analytics is the tool that you're going to use to write and test those queries.

![image](https://user-images.githubusercontent.com/48266482/227700232-4cc23c61-d670-4818-b008-3da10a0abe59.png)

![image](https://user-images.githubusercontent.com/48266482/227700247-5d48647d-cb8f-4ab9-89e8-49c767c435e8.png)


### Azure Monitor Alerts
Azure Monitor Alerts are an automated way to stay informed when Azure Monitor detects a threshold being crossed. You set the alert conditions, the notification actions, and then Azure Monitor Alerts notifies when an alert is triggered. Depending on your configuration, Azure Monitor Alerts can also attempt corrective action.

![image](https://user-images.githubusercontent.com/48266482/227698705-56aa9f27-4523-4024-91f8-94a5945c78a3.png)

Alerts can be set up to monitor the logs and trigger on certain log events, or they can be set to monitor metrics and trigger when certain metrics are crossed. For example, you could set a metric-based alert up to notify you when the CPU usage on a virtual machine exceeded 80%. Alert rules based on metrics provide near real time alerts based on numeric values. Rules based on logs allow for complex logic across data from multiple sources.

Azure Monitor Alerts use action groups to configure who to notify and what action to take. An action group is simply a collection of notification and action preferences that you associate with one or multiple alerts. Azure Monitor, Service Health, and Azure Advisor all use actions groups to notify you when an alert has been triggered.

![image](https://user-images.githubusercontent.com/48266482/227700542-3244081b-8f4d-4f40-8e71-3d72480ecbeb.png)

### Application Insights
Application Insights, an Azure Monitor feature, monitors your web applications. Application Insights is capable of monitoring applications that are running in Azure, on-premises, or in a different cloud environment.

There are two ways to configure Application Insights to help monitor your application. You can either install an SDK in your application, or you can use the Application Insights agent. The Application Insights agent is supported in C#.NET, VB.NET, Java, JavaScript, Node.js, and Python.

Once Application Insights is up and running, you can use it to monitor a broad array of information, such as:

- Request rates, response times, and failure rates
- Dependency rates, response times, and failure rates, to show whether external services are slowing down performance
- Page views and load performance reported by users' browsers
- AJAX calls from web pages, including rates, response times, and failure rates
- User and session counts
- Performance counters from Windows or Linux server machines, such as CPU, memory, and network usage

Not only does Application Insights help you monitor the performance of your application, but you can also configure it to periodically send synthetic requests to your application, allowing you to check the status and monitor your application even during periods of low activity.

![image](https://user-images.githubusercontent.com/48266482/227700311-28881849-4197-430d-b50c-275a73fc3cd4.png)

![image](https://user-images.githubusercontent.com/48266482/227700330-675fa3bc-9124-4460-8793-e0f8aefc681d.png)

## Azure Service Health
Microsoft Azure provides a global cloud solution to help you manage your infrastructure needs, reach your customers, innovate, and adapt rapidly. Knowing the status of the global Azure infrastructure and your individual resources could seem like a daunting task. Azure Service Health helps you keep track of Azure resource, both your specifically deployed resources and the overall status of Azure. Azure service health does this by combining three different Azure services:

- **Azure Status** is a broad picture of the status of Azure globally. Azure status informs you of service outages in Azure on the Azure Status page. The page is a global view of the health of all Azure services across all Azure regions. It’s a good reference for incidents with widespread impact.
- **Service Health** provides a narrower view of Azure services and regions. It focuses on the Azure services and regions you're using. This is the best place to look for service impacting communications about outages, planned maintenance activities, and other health advisories because the authenticated Service Health experience knows which services and resources you currently use. You can even set up Service Health alerts to notify you when service issues, planned maintenance, or other changes may affect the Azure services and regions you use.
- **Resource Health** is a tailored view of your actual Azure resources. It provides information about the health of your individual cloud resources, such as a specific virtual machine instance. Using Azure Monitor, you can also configure alerts to notify you of availability changes to your cloud resources.

By using Azure status, Service health, and Resource health, Azure Service Health gives you a complete view of your Azure environment-all the way from the global status of Azure services and regions down to specific resources. Additionally, historical alerts are stored and accessible for later review. Something you initially thought was a simple anomaly that turned into a trend, can readily be reviewed and investigated thanks to the historical alerts.

Finally, in the event that a workload you’re running is impacted by an event, Azure Service Health provides links to support.

### Azure Advisor
Azure Advisor evaluates your Azure resources and makes recommendations to help improve reliability, security, and performance, achieve operational excellence, and reduce costs. Azure Advisor is designed to help you save time on cloud optimization. The recommendation service includes suggested actions you can take right away, postpone, or dismiss.

The recommendations are available via the Azure portal and the API, and you can set up notifications to alert you to new recommendations.

When you're in the Azure portal, the Advisor dashboard displays personalized recommendations for all your subscriptions. You can use filters to select recommendations for specific subscriptions, resource groups, or services. The recommendations are divided into five categories:

- **Reliability** is used to ensure and improve the continuity of your business-critical applications.
- **Security** is used to detect threats and vulnerabilities that might lead to security breaches.
- **Performance** is used to improve the speed of your applications.
- **Operational Excellence** is used to help you achieve process and workflow efficiency, resource manageability, and deployment best practices.
- **Cost** is used to optimize and reduce your overall Azure spending.

The following image shows the Azure Advisor dashboard.
![image](https://user-images.githubusercontent.com/48266482/227699642-aff15928-6c04-4908-ad8f-104323e83eeb.png)


## Compliance

![image](https://user-images.githubusercontent.com/48266482/227700945-487d2857-7085-4abb-acaf-5358308d8b21.png)

### Azure Compliance Manager
Azure knows about compliance and resources, and can give you recommendations through the Compliance Manager

![image](https://user-images.githubusercontent.com/48266482/227701004-f975a40d-fe94-4c46-bb35-171df1a442b4.png)

- **Recommendations**: Get recommendations for ensuring compliance with GDPR, ISO, NIST and others.
- **Tasks**: Assign compliance tasks to learn members and track progress.
- **Compliance Score**: Chase a prefect score to be 100% compliant. Gamification for the win!
- **Secure Storage**: Upload documents to prove compliance and store them securly.
- **Reports**: Get reports of compliance data to provide to managers and auditors.

![image](https://user-images.githubusercontent.com/48266482/227701187-d15bddda-cc9e-42e8-a8c4-50eb59e3c022.png)

![image](https://user-images.githubusercontent.com/48266482/227701220-e532ee3d-4f72-4540-bb14-7400e5389773.png)

### Exam tips
**Compliance is not negotiable.**

- GDPR, ISO and NIST are regulations and standards to ensure compliance with applicable legislation.
- Azure Compliance Manager provides recommendations, tasks to assign team members, a compliance score, secure document storage and reports.
- Azure Government Cloud provides dedicated datacenters to US Government bodies. Compliant with US federal, state and local requirements.
- Azure China region contains all data and datacenters within China. Complies with all applicable Chinese regulations.

## Privacy
### Azure Privacy
- **Azure information Protection**: Classify, label and protect data based on data sensitivity.
- **Azure Policy**: Define and enforce rules to ensure privacy and external egulations.
- **Guides**: Use guides on Azure to respond and comply with GDPR privacy requrests.
- **Compliance Manager**: Make sure you are following privacy guidelines.

## Trust
![image](https://user-images.githubusercontent.com/48266482/227701619-591591c8-fd1e-41d0-86aa-0c8a08678512.png)

## Azure Arc
![image](https://user-images.githubusercontent.com/48266482/227701705-50bc6901-41a6-4c94-b545-390430fd680c.png)

Centralized governance and management for on-premises and multi-cloud computing resources.
- Manage non-Azure resources as if they were in Azure.
- Extend Azure cloud management and services to non-Azure locations.

![image](https://user-images.githubusercontent.com/48266482/227701838-00d0833c-e7df-4704-8dd1-cab89a8a1b9f.png)

### Benefits
- Manage Azure and non-Azure resources in same place
- Manage non-Azure kubernetes clusters
- Deploy Azure-managed database services to non-Azure locations
  - Ex.: Azure SQL Managed Instance
- Manage and protect non.Azure servers
  - Monitor non-Azure OSs alongside Azure VMs
  - Protect with Microsoft Defender for cloud
  - Apply Azure Automation runbooks
- Apply Azure governance
  - RBAC
  - Azure Policies
  - Azure Blueprints
- Deploy Azure serverless services to non-Azure hardware
  - Azure App Service
  - Azure Functions
  - Azure Logic Apps
  - And more!

![image](https://user-images.githubusercontent.com/48266482/227702011-24277bec-86fc-4b0b-91b2-5f7b6f84658f.png)




