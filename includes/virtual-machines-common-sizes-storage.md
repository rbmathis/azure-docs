---
 title: include file
 description: include file
 services: virtual-machines
 author: jonbeck7
 ms.service: virtual-machines
 ms.topic: include
 ms.date: 07/06/2018
 ms.author: azcspmt;jonbeck;cynthn
 ms.custom: include file
---

Storage optimized VM sizes offer high disk throughput and IO, and are ideal for Big Data, SQL, NoSQL databases, data warehousing and large transactional databases.  Examples include Cassandra, MongoDB, Cloudera and Redis. This article provides information about the number of vCPUs, data disks and NICs as well as local storage throughput and network bandwidth for each optimized size.

The Lsv2-series features high throughput, low latency, directly mapped local NVMe storage running on the [AMD EPYC<sup>TM</sup> 7551 processor](https://www.amd.com/en/products/epyc-7000-series) with an all core boost of 2.55GHz and a max boost of 3.0GHz. The Lsv2-series VMs come in sizes from 8 to 80 vCPU in a simultaneous multi-threading configuration.  There is 8 GiB of memory per vCPU, and one 1.92TB NVMe SSD M.2 device per 8 vCPUs, with up to 19.2TB (10x1.92TB) available on the L80s v2.

The Ls-series offers up to 32 vCPUs, using the [Intel® Xeon® processor E5 v3 family](http://www.intel.com/content/www/us/en/processors/xeon/xeon-e5-solutions.html). The Ls-series gets the same CPU performance as the G/GS-Series and comes with 8 GiB of memory per vCPU.

> [!NOTE]
> The Lsv2-series VMs are optimized to use the local disk on the node attached directly to the VM    rather than using durable data disks.  This allows for greater IOPs / throughput for your workloads.  The Lsv2 and Ls-series do not support the creation of a local cache to increase the IOPS achievable by durable data disks. The high throughput and IOPS of the local disk makes the Lsv2 and Ls-series VMs ideal for NoSQL stores such as Apache Cassandra and MongoDB which replicate data across multiple VMs to achieve persistence in the event of the failure of a single VM. 

## Lsv2-series
ACU: 150-175

Premium Storage: Supported

Preminu Storage Caching: Not Supported

| Size          | vCPU | Memory (GiB) | Temp disk<sup>1</sup> (GiB) | NVMe Disks | NVMe Disk throughput<sup>2</sup> (Read IOPS / MBps) | Host Cache Size<sup>3</sup> | Max Data Disks | Max NICs / Expected network bandwidth (Mbps) | 
|---------------|-----------|-------------|--------------------------|----------------|---------------------------------------------------|-------------------------------------------|------------------------------|------------------------------| 
| Standard_L8s_v2   |  8 |  64 |  80 |  1x1.92 TB  | 340,000 / 2,000 | N/A | 16 | 2 / 3,200  | 
| Standard_L16s_v2  | 16 | 128 | 160 |  2x1.92 TB  | 680,000 / 4,500 | N/A | 32 | 4 / 6,400  | 
| Standard_L32s_v2  | 32 | 256 | 320 |  4x1.92 TB  | 1.4M / 9,000    | N/A | 32 | 8 / 12,800 | 
| Standard_L64s_v2  | 64 | 512 | 640 |  8x1.92 TB  | 2.7M / 18,000   | N/A | 32 | 8 / 25,600 |
| Standard_L80s_v2  | 80 | 640 | 800 | 10x1.92TB   | 3.4M / 22,000   | N/A | 32 | 8 / 32,000 |
 
<sup>1</sup> Lsv2-series VMs have a standard SCSI based temp resource disk for OS paging/swap file use (D: on Windows, /dev/sdb on Linux). This disk provides 80 GiB of storage, 4,000 IOPS, and 80 MBps transfer rate for every 8 vCPUs (e.g. Standard_L80s_v2 provides 800 GiB at 40,000 IOPS and 800 MBPS). This ensures the NVMe drives can be fully dedicated to application use.

<sup>2</sup> Hyper-V NVMe Direct technology provides unthrottled access to NVMe drives mapped securely into the guest VM space.  Achieving maximum performance requires using either the latest WS2019 build or Ubuntu 18.04 or 16.04 from the Azure Marketplace.  Write performance varies based on IO size, drive load, and capacity utilization.

<sup>3</sup> Lsv2-series VMs do not provide host cache for data disk as it does not benefit the Lsv2 workloads.  However, Lsv2 VMs can accommodate Azure’s Ephemeral VM OS disk option (up to 30 GiB). 



## Ls-series
ACU: 180-240

Premium Storage:  Supported

Premium Storage Caching:  Not Supported
 
| Size          | vCPU | Memory (GiB) | Temp storage (GiB) | Max data disks | Max temp storage throughput (IOPS / MBps) | Max uncached disk throughput (IOPS / MBps) | Max NICs / Expected network bandwidth (Mbps) | 
|----------------|-----------|-------------|--------------------------|----------------|-------------------------------------------------------------|-------------------------------------------|------------------------------| 
| Standard_L4s   | 4  | 32  | 678   | 16 | 20,000 / 200 | 5,000 / 125  | 2 / 4,000  | 
| Standard_L8s   | 8  | 64  | 1,388 | 32 | 40,000 / 400 | 10,000 / 250 | 4 / 8,000  | 
| Standard_L16s  | 16 | 128 | 2,807 | 64 | 80,000 / 800 | 20,000 / 500 | 8 / 16,000 | 
| Standard_L32s <sup>1</sup> | 32   | 256  | 5,630 | 64   | 160,000 / 1,600   | 40,000 / 1,000     | 8 / 20,000 | 
 

The maximum disk throughput possible with Ls-series VMs may be limited by the number, size, and striping of any attached disks. For details, see [Premium Storage: High-performance storage for Azure virtual machine workloads](../articles/virtual-machines/windows/premium-storage.md).

<sup>1</sup> Instance is isolated to hardware dedicated to a single customer.

## Size table definitions

- Storage capacity is shown in units of GiB or 1024^3 bytes. When comparing disks measured in GB (1000^3 bytes) to disks measured in GiB (1024^3) remember that capacity numbers given in GiB may appear smaller. For example, 1023 GiB = 1098.4 GB
- Disk throughput is measured in input/output operations per second (IOPS) and MBps where MBps = 10^6 bytes/sec.
- If you want to get the best performance for your VMs, you should limit the number of data disks to 2 disks per vCPU.
- **Expected network bandwidth** is the maximum aggregated [bandwidth allocated per VM type](../articles/virtual-network/virtual-machine-network-throughput.md) across all NICs, for all destinations. Upper limits are not guaranteed, but are intended to provide guidance for selecting the right VM type for the intended application. Actual network performance will depend on a variety of factors including network congestion, application loads, and network settings. For information on optimizing network throughput, see [Optimizing network throughput for Windows and Linux](../articles/virtual-network/virtual-network-optimize-network-bandwidth.md). To achieve the expected network performance on Linux or Windows, it may be necessary to select a specific version or optimize your VM. For more information, see [How to reliably test for virtual machine throughput](../articles/virtual-network/virtual-network-bandwidth-testing.md).
