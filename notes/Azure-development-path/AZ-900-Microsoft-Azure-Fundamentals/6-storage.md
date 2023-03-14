# [Storage](https://learn.microsoft.com/hu-hu/training/modules/describe-azure-storage-services/2-accounts)
Storage Account = Unique Azure Namespace

## Storage account endpoints
One of the benefits of using an Azure Storage Account is having a unique namespace in Azure for your data. In order to do this, every storage account in Azure must have a unique-in-Azure account name. The combination of the account name and the Azure Storage service endpoint forms the endpoints for your storage account.

When naming your storage account, keep these rules in mind:

- Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.
- Your storage account name must be unique within Azure. No two storage accounts can have the same name. This supports the ability to have a unique, accessible namespace in Azure.
The following table shows the endpoint format for Azure Storage services.

![image](https://user-images.githubusercontent.com/48266482/224895641-8191146a-2433-42d6-8853-21490a26a9ee.png)
  
## Blob
- Images
- All types
- Streaming audio/vido
- Log files
- Data store: Store any kind of data at scale, such as for archiving, backup, restore and disaster recovery.

### Blob types
- Block: Store text and binary data up to 4.7TB. Made up of individually managed blocks of data.
- Appended: Block blobs that are optimized for append operations. Works well for logging where data is constantly appended.
- Page: Store files up to 8TB. Any part of the file could be accessed at any time, for example a virtual hard drive.

### Pricing Tiers
- Hot: Frequently accessed files. Lower access times and higher access costs.
- Cool: Lower storage costs and higher access times. Data remains here for at least 30 days.
- Archive: Lowest costs

## Disc
- Azure Manages: You don't have to worry aboout backup and uptime
- Size and Performance: MIcrosoft and Azure guarantees size and perfromance as per your agreement with them.
- Upgrade: Easy to upgrade your disk and type.

### Disk Types
- HDD: Low cost and suitable for backups.
- SSD: Standard for production. Higher reliability, scalability and lower latency over HDD.
- Premium SSD: Super fast and high performance. Very low latancy. Use for critical workloads.
- Ultra Disk: For the most demanding, dataintensive workloads. Disks up to 64TB.

## File
- Sharing: Share access to the Azure file storage across machines and provide acess to your on-premises infrastructure.
- Managed: You don't have to worry about hardware or operating system.
- Resilient: Network and power outages won't affect your storage.

### Scanario
- Hybrid: Supplement or replace your existing on-premises file storage solution.
- Lift and shift: Move your existing file storages and related services to Azure.

## Archive
- Requirement: Policies, legislation and recovery can be requirements for archiving data. These can be very large amounts of data.
- Lowest Price: The archive tier is the lowest price for storage on Azure. A few dollars a month can get you terabytes of space.
- Features: Durable, encrypted and stable. Perfectly suited for data that is accessed infrequently.
- Free Up Premium Storage: With cheap archive storage you can free up your more premium on-premisies storage.
- Secure: Fully secure to allow for any personal data such as financial records, medical data and more.
- Blob: Archive storage is blob storage, so the same tools will work for both.

## Azure storage redundancy
Azure Storage always stores multiple copies of your data so that it's protected from planned and unplanned events such as transient hardware failures, network or power outages, and natural disasters. Redundancy ensures that your storage account meets its availability and durability targets even in the face of failures.

When deciding which redundancy option is best for your scenario, consider the tradeoffs between lower costs and higher availability. The factors that help determine which redundancy option you should choose include:

- How your data is replicated in the primary region.
- Whether your data is replicated to a second region that is geographically distant to the primary region, to protect against regional disasters.
- Whether your application requires read access to the replicated data in the secondary region if the primary region becomes unavailable.
  
![image](https://user-images.githubusercontent.com/48266482/224895390-70e64578-7cb4-47db-8ab6-6cc05487a27e.png)

### Redundancy in the primary region
Data in an Azure Storage account is always replicated three times in the primary region. Azure Storage offers two options for how your data is replicated in the primary region, locally redundant storage (LRS) and zone-redundant storage (ZRS).
  
### Single Region
  - Locally Redundant Storage (LRS)
  - Zone-Redundant Storage (ZRS)

### Multi Region
  - Geo-Redundant Storage (GRS)
  - Geo-Zone-Redundant Storage (GZRS)
  
 ### All options include:
  - Three copies in primary region
  - Three copies in secondary region (multi-region options)
  
### Locally Redundant Sotrage (LRS)
Locally redundant storage (LRS) replicates your data three times within a single data center in the primary region. LRS provides at least 11 nines of durability (99.999999999%) of objects over a given year.

![image](https://user-images.githubusercontent.com/48266482/224896621-c8a77018-1ada-42bc-9bb7-da71556d743e.png)

LRS is the lowest-cost redundancy option and offers the least durability compared to other options. LRS protects your data against server rack and drive failures. However, if a disaster such as fire or flooding occurs within the data center, all replicas of a storage account using LRS may be lost or unrecoverable. To mitigate this risk, Microsoft recommends using zone-redundant storage (ZRS), geo-redundant storage (GRS), or geo-zone-redundant storage (GZRS).
  
- Lowest-cost option
- Protect against single disk failure
- Does not protect against zome or regional outage.

### Zone-Redundant Storage (ZRS)
For Availability Zone-enabled Regions, zone-redundant storage (ZRS) replicates your Azure Storage data synchronously across three Azure availability zones in the primary region. ZRS offers durability for Azure Storage data objects of at least 12 nines (99.9999999999%) over a given year.
  
![image](https://user-images.githubusercontent.com/48266482/224897014-27db5918-0296-415b-bcc6-f1f6e641c1d2.png)

With ZRS, your data is still accessible for both read and write operations even if a zone becomes unavailable. No remounting of Azure file shares from the connected clients is required. If a zone becomes unavailable, Azure undertakes networking updates, such as DNS repointing. These updates may affect your application if you access data before the updates have completed.

Microsoft recommends using ZRS in the primary region for scenarios that require high availability. ZRS is also recommended for restricting replication of data within a country or region to meet data governance requirements.

- One copy in each zone
- Protect against zone outage but not regional outage

### Redundancy in a secondary region
For applications requiring high durability, you can choose to additionally copy the data in your storage account to a secondary region that is hundreds of miles away from the primary region. If the data in your storage account is copied to a secondary region, then your data is durable even in the event of a catastrophic failure that prevents the data in the primary region from being recovered.

When you create a storage account, you select the primary region for the account. The paired secondary region is based on Azure Region Pairs, and can't be changed.

Azure Storage offers two options for copying your data to a secondary region: geo-redundant storage (GRS) and geo-zone-redundant storage (GZRS). GRS is similar to running LRS in two regions, and GZRS is similar to running ZRS in the primary region and LRS in the secondary region.

By default, data in the secondary region isn't available for read or write access unless there's a failover to the secondary region. If the primary region becomes unavailable, you can choose to fail over to the secondary region. After the failover has completed, the secondary region becomes the primary region, and you can again read and write data.

>**Important**:
>Because data is replicated to the secondary region asynchronously, a failure that affects the primary region may result in data loss if the primary region can't be recovered. The interval between the most recent writes to the primary region and the last write to the secondary region is known as the recovery point objective (RPO). The RPO indicates the point in time to which data can be recovered. Azure Storage typically has an RPO of less than 15 minutes, although there's currently no SLA on how long it takes to replicate data to the secondary region.

### Geo-Redundant Storage (GRS)
GRS copies your data synchronously three times within a single physical location in the primary region using LRS. It then copies your data asynchronously to a single physical location in the secondary region (the region pair) using LRS. GRS offers durability for Azure Storage data objects of at least 16 nines (99.99999999999999%) over a given year.

![image](https://user-images.githubusercontent.com/48266482/224897847-ffcfb5c3-2c8f-42c2-a721-2845c2848b11.png)
  
- Three copies in primary regional physical location (LRS)
- Three copies in secondary (paired) region physical location (LRS)
- Protect against primary region failure but no primary region zone redundancy
- Can configure read access from seconday region for high availability
  
### Geo-Zone-Redundant Storage (GZRS)
GZRS combines the high availability provided by redundancy across availability zones with protection from regional outages provided by geo-replication. Data in a GZRS storage account is copied across three Azure availability zones in the primary region (similar to ZRS) and is also replicated to a secondary geographic region, using LRS, for protection from regional disasters. Microsoft recommends using GZRS for applications requiring maximum consistency, durability, and availability, excellent performance, and resilience for disaster recovery.
GZRS is designed to provide at least 16 nines (99.99999999999999%) of durability of objects over a given year.
 
![image](https://user-images.githubusercontent.com/48266482/224898092-985f9f0b-fbb0-4ede-88d5-2f46f0d3a790.png)
 
- Copy accross three availability zones in primary region (ZRS)
- Three copies in secondary region physical location/zone (LRS)
- Protect against primary region failure AND primary region zone failure
- Can also configure read access from seconday region for high availablity

### Read access to data in the secondary region
Geo-redundant storage (with GRS or GZRS) replicates your data to another physical location in the secondary region to protect against regional outages. However, that data is available to be read only if the customer or Microsoft initiates a failover from the primary to secondary region. However, if you enable read access to the secondary region, your data is always available, even when the primary region is running optimally. For read access to the secondary region, enable read-access geo-redundant storage (RA-GRS) or read-access geo-zone-redundant storage (RA-GZRS).

> **Important:**
> Remember that the data in your secondary region may not be up-to-date due to RPO.

## Moving Data

## Additional Migration Options

## Premium Performance Options
