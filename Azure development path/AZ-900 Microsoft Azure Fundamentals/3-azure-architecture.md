# Azure Architecture

## Regions 
A region is a set of datacenters deployed within a latency-defined perimeter and connected through a dedicated regional low-latency network

### "A set of datacenters"
Each region has more than one data center, which is a physical location.
Ex.: East US has an official location of Virginia, but there will be more than one datacenter there.

### "Latency defined perimeter"
Latency is the time it takes data to travel. Also means that datacenters are not "too far" from each other.

### Regional low-latency network
A fiber connection between data centers in the region.

### How to choose a region

#### Location
Choose a region closest to your users to minimize latency.

#### Features
Some features aren't in all regions. If you need a specific feature, some regions might be unavailable.

#### Price
The price of services vary from region to region. 
Ex.: The price for a VM can be 20-30% difference  from region to region.

> You will often have to choose which is the most important: location, feature or price

### Paired Region
#### Each Region is Paired
Paired within same geographic area except Brazil south.
Ex.: East US is paired with West US, France Central is paired with France South, Australia East is paired with Australia Southeast. The exception is Brazil South which is paired with South Central US.

#### Outage Failover
If the primary region has an outage you can failover to the secondary region.
In the event of an outage affecting multiple regions, at least one region in each pair will be prioritized for recovery.

#### Planned Updates
Only one region in a pair is updated at any one time.

#### Replication 
Some services used paired regions for replication.


## Availability Zones
- Phisical Location: Each availability zone is a physical location within a region.
- Independent: Each zone has itsh own power, cooling and networking.
- Zones: Each region has a minimum of three zones.

![image](https://user-images.githubusercontent.com/48266482/219389259-6b108948-123b-4f73-a22d-e1a2e8a0efcd.png)


## Resource Groups

## Azure Resource Manager
