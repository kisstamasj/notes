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

## Storage Redundancy
Azure Storage always create multiple copies of your data:
- Automatic
- Minimum of three copies
- Invisible to end user
  
![image](https://user-images.githubusercontent.com/48266482/224895390-70e64578-7cb4-47db-8ab6-6cc05487a27e.png)
  
### Multiple Redundancy options
- Different location scopes
  - Single zone, multi zone, multi regions
- Higher availablity = higher cost
  
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
Three copies in single location (datacenter/zone)

![image](https://user-images.githubusercontent.com/48266482/224627316-19996fef-79b9-4ff0-b7f1-5b9a9fa0b9d9.png)
  
  - Lowest-cost option
  - Protect against single disk failure
  - Does not protect against zome or regional outage.

### Zone-Redundant Storage (ZRS)
Three copies across three availability zones.
  
![image](https://user-images.githubusercontent.com/48266482/224627647-b967343e-149c-4ad1-9c99-6022e0d50074.png)

  - One copy in each zone
  - Protect against zone outage but not regional outage
  
### Geo-Redundant Storage (GRS)
Three copies in two different regions

![image](https://user-images.githubusercontent.com/48266482/224628282-dff1103e-6b4e-4499-9a9c-de174c8539b1.png)
  
  - Three copies in primary regional physical location (LRS)
  - Three copies in secondary (paired) region physical location (LRS)
  - Protect against primary region failure but no primary region zone redundancy
  - Can configure read access from seconday region for high availability
  
### Geo-Zone-Redundant Storage (GZRS)
Maximum redundancy
 
![image](https://user-images.githubusercontent.com/48266482/224629110-5ca468f2-0bc8-4c0d-842c-94dbdd043d87.png)
 
  - Copy acreoss three availability zones in primary region (ZRS)
  - Three copies in secondary region physical location/zone (LRS)
  - Protect against primary region failure AND primary region zone failure
  - Can also configure read access from seconday region for high availablity
  
## Moving Data

## Additional Migration Options

## Premium Performance Options
