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

## The Language of Cloud Ecomomics

### Capital and Operational Expenditure

#### Capital Expenditure (CapEx)
- Money spent by a business or organisation on acquiring or maintaining fixed, such as land, builings, and equipment.
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

## [Cloud Service Models](https://github.com/kisstamasj/notes/blob/main/Azure%20development%20path/1-azure-organization-and-infrastructure.md#iaas-paas-and-saas)

### Infrastructure-as-a-Service (IaaS)
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
- Provideing a managed service
- Pay an access fee to use
- No maintenancet and latest features

![image](https://user-images.githubusercontent.com/48266482/219363985-eae7d422-d34f-4ab3-a933-c8941749d3ea.png)

### Serverless
- Of course there are servers!
- Azure Functions is the best known serverkess service
- Extreme PaaS

![image](https://user-images.githubusercontent.com/48266482/219364265-78ddb4f0-bc00-4de6-b104-a078ca3cc34f.png)

### Identifying Cloud Service Models
![image](https://user-images.githubusercontent.com/48266482/219364364-f69e4f79-6e50-4b7e-bc4a-9281f9a87443.png)



