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


## Availability Zones

## Resource Groups

## Azure Resource Manager
