## NVME

<https://www.youtube.com/watch?v=Fwv_85YRovQ>

accessing ssd through tcp

nvme is an standard on top of PciE and ssds.

___

nvme
writes of a single logicval block *must* be atomic.
block? sector? journal? raid | write cache?s

```
. Commands rare submitted to devices using a set of queues. 
At some tmie, the device acknowledges that the command have complete. There is no ordering guaranteed between commands. 
    . Host or application is required to enfornce that ordering.
        -> Software needs to wait for commands to complete before issuing the next commands. 
    . Guaranteed to return the most ocmpleted write, although they may also return data from uncompleted writes that have been queued. 

In the case of concurrent writes to overlapping ranges, what are the permitted results? 
    . Not specified ;  weak ordering, sematics similar to memory in multithreading. 
```

___

## SSD

<https://www.youtube.com/watch?v=CjUdp1UY3uM>

SSD is a block device. You can only read and write in blocks - Usually 4k bytes sizes.

Blocks are a storage of pages.

How do we know the address of those blocks?
. The application could just send a "update block 10" -> The ssd moves stuff around all the time
. So, we use the Logical Block Addressing - The ssd internally creates and maintain a mapping from logical to physical block.
.. the Flash Translation Layer is what does this mapping.
.. Where does it store the mapping? DRAM
.. This mapping can be smaller if we use a coarser block size, and vice-versa
... If we do a page-level addressing, it requires large amounts of ram.
.. WHy does it needs it anyway??

Erase Unit
.. To write to a block, we must first erase its previous contents.
.. We could send a a Erase and then a Write - But then things egt slow, since we're doing 2 operations.
.. Erasing is expensive at ssd - so we do it in large units
.. To erase, a physical larger current is applied to the cell - Over time , this wears the cell down

Namespaces
Helps with multi-tenancy

SSDs do Garbage Collection
. There is no guarantees about the contiguity of data from each file
. When writing and updating files, the blocks aren't immediately erased, just marked as invalid.
. At some point, every block is in use or invalid, so we must clean the space somehow.
. We must them, clean an erase unit - but it isn't completely invalid, it contain good blocks.
. So, we must pick the good data and place it temporally to some place - but the ssd is full, so -
. we place it in an area called over-provisioning -> It is dedicated for the system.  -> Paid , but not used
. The process of writing to a buffer, erasing the unit, then writing it back generates write amplification ( 4x )
. During this garbage collection time, reads to file which contains blocks at the erase unit are blocked ;

Wear Leveling
. Data access is not uniform - There are places that are cold and others that are hot.
. Therefore, the hot cells wear out first.
. The ssd then moves cold and hot data around to level the wear out.

___

## RAid

```
Raid
    . Redundant Array of Inexpensive Disks
    . Improve disk size and performance in the most cost-effective way
    . Take 10-20 drive, but the PC looks at it as only one
    . Improves size , performance and redundancy of storage

    . Raid- 0 
        .. Best for disk performance ( striped writes)
        .. VERY fast
        .. Low fault tolerance 
        .. If you're using RAID-0, your disks WILL go down, just a matter of when. you need BACKUP.
        .. BACKUP BACKUP BACKUP
        .. Some flavor of RAID-0 is the only way to get acceptable performance on the cloud
            ... 64k IOPS is the maximum you can get in a ebs volume, vs 1M of a off-the-shelf disk
            ... If you need 1M IOPS from EBS, you need to pack 15 of these dirves together
        .. Too risky. Hard drive for video game computers ; Video Editing ; 
    . Raid-1
        .. Best for redundancy ( Mirroring )
        .. Real time backup 
        .. very slow. expensive ,   doesn't increase capacity, performance isn't great
    . Raid-5
        .. Balance of speed and redundancy
        .. Each One of the drives reserves some capacity to parity
        .. Not very common on the cloud,  because it adds latency ( and 64k IOPS is already low enough. )
        .. Very good on-prem
    . Raid-10
        .. Basically only opiton in the cloud to get the necessary IOPS. 
        .. Very expensive, since you need double the number of drives



Raid
    . Redundant Array of Inexpensive Disks
    . Improve disk size and performance in the most cost-effective way
    . Take 10-20 drive, but the PC looks at it as only one
    . Improves size , performance and redundancy of storage



    . Raid- 0 
        .. Best for disk performance ( striped writes)
        .. VERY fast
        .. Low fault tolerance 
        .. If you're using RAID-0, your disks WILL go down, just a matter of when. you need BACKUP.
        .. BACKUP BACKUP BACKUP
        .. Some flavor of RAID-0 is the only way to get acceptable performance on the cloud
            ... 64k IOPS is the maximum you can get in a ebs volume, vs 1M of a off-the-shelf disk
            ... If you need 1M IOPS from EBS, you need to pack 15 of these dirves together
        .. Too risky. Hard drive for video game computers ; Video Editing ; 
    . Raid-1
        .. Best for redundancy ( Mirroring )
        .. Real time backup 
        .. very slow. expensive ,   doesn't increase capacity, performance isn't great
    . Raid-5
        .. Balance of speed and redundancy
        .. Each One of the drives reserves some capacity to parity
        .. Not very common on the cloud,  because it adds latency ( and 64k IOPS is already low enough. )
        .. Very good on-prem
    . Raid-10
        .. Basically only opiton in the cloud to get the necessary IOPS. 
        .. Very expensive, since you need double the number of drives
```
