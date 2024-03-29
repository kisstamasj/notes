# Azure development path
# Azure Concepts

## Benefits and considerations
- High availability
  - Data center redundancies:
    - Power
    - Cooling
    - Networking
    - etc..
  - Availability Zone Redundancies
    - 1 or more data centers
  - Region redundancies
    - Multiple availability zones
- Fault tolerance
  - Proactive
    - Regularly back up data/apps/resources
    - Deploy to multiple availability zones or regions
    - Load balance across multiple availability zones or regions
    - Monitor health of data/apps/resources
   - Reactive
     - Restore data/apps/resources to different availability zones or regions
     - Deploy to different availability zones or regions   
- Disaster recovery
   - On-premises to on-premises
   - On-premises to Azrue
   - Other cloud to Azure
   - Azure to Azure

Inside Azure data center:
https://www.youtube.com/watch?v=69PrhWQorEM

## Scalability
The ability to incrase the instace count or size of existing resources
- Scaling Out (Horizontal scaling)
  - Incrase instace count of existing resources
  - Incrasing the servers number to handle more request
  - Non-disruptive
- Scaling Up (Vertical scaling)
  - Incrase instace size of existing resource
  - Get a bigger server: more CPU, RAM etc..
  - Disruptive

## Elasticity
The ability to incrase or decrase the instance count or size of existing resource based on fluctuatuins in traffic or load, or in resource workload.
- Ability to scale in both directions (in + out, up + down)
- Can be manual or automatic
- Based on changes in load or workload
- Pay only for what you use

## Buisness Agility
An organisation's ability to rapidly adapt to market and environmental changes in productive and cost-effective ways and take advantage of scalable resources to meet customer demands

![image](https://user-images.githubusercontent.com/48266482/219025849-5b7102c3-bbf0-4d3b-bccc-83ba499f78db.png)

## Subscriptions
![image](https://user-images.githubusercontent.com/48266482/219029871-a7872364-64e7-4f4c-beb7-8d4c7c251ee2.png)

## Active Directory (AD)
![image](https://user-images.githubusercontent.com/48266482/219032348-69efb058-5e15-4099-b2c9-54fc19522e51.png)

## Virtual networks (VNs)
Communication between devices or resources.

![image](https://user-images.githubusercontent.com/48266482/219034535-50b5217c-77f1-4966-86c5-fde8940883cd.png)

## Virtual Machines (VMs)
![image](https://user-images.githubusercontent.com/48266482/219035740-2f575e19-562c-4dd9-bd3d-5f0413823363.png)

### What for?
- Processor intensive activities (calculation in a database table)

## Azure Storage 
![image](https://user-images.githubusercontent.com/48266482/219042316-71ef0ae8-9da4-4f72-93e9-62dce0d72a62.png)

- distributed storage (multiple computers and storage)
  - fault tolerant: different network, different power

