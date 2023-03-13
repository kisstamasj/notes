# Storage
Storage Account = Unique Azre Namespace

- Every object in Azure has its own web address
  - Example: acloudguru.<storage-type>.core.windows.net
  
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

## Moving Data

## Additional Migration Options

## Premium Performance Options
