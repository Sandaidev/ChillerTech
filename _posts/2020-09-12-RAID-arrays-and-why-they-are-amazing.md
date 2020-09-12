---
title: RAID Arrays and why they're amazing
---

# Concept

RAID stands for "**R**edundant **A**rray of **I**ndependent **D**isks", and it has different levels that are each tailored for a specific use case.

**Here's a short list of the most popular ones**:

    - RAID 0
  
    - RAID 1
  
    - RAID 5
  
    - RAID 6
    
    - (a few more standard and non-standard ones as well but they're not as popular so we won't cover them.)

So, let's explain each of them in more detail shall we?

### RAID 0

Benefit: **It spreads your data evenly accross all your drives.** Say, for example, you have four HDDs, each containing 1 TB of capacity. You want to write a 4 GB file to the array, the RAID 0 will then split your file in four chunks of 1 GB and distribute them to each drive. So when you'll want to read the 4 GB file from the array, the RAID 0 will take advantage of this and will read the four chunks of 1 GB in parallel, thus improving the read speed 4 times!

Drawbacks: You must have a finite number of drives with the same capacity, if not, the array will span your drives using the smallest capacity of one drive you have, so if you have a 1x250 GB drive and 3x1 TB drives, you'll get an array of 4x250 GBs, with the remaining space on your 3x1 TB drives left unused.

Please also notice that the more drives you add to a RAID 0 array, the more it is prone to data loss. that is because the data you store on the array is ***NOT*** redundant;

> ***A note about redundancy***
>
> In a RAID array, having a redundant layout is having a protection mechanism in the event that a drive fails. Meaning in the simplest example, you have 2x1 TB drives, if you're writing a 4 GB file to the first drive, it gets transparently duplicated to the second drive. Now, let's say that your first drive fails, the second drive takes over the first one and your data is still there!

### RAID 1

Just like the previous note, a RAID 1 array takes **two drives** and duplicates the data from the first drive to the second drive. if your first drive fails, the second one takes over. Now, when you'll replace the failed drive, the array will effectively do what we call a "*rebuild*", meaning that it will copy the entire contents of the first drive to the new one.

### RAID 5

In the simplest terms, it's a RAID 0 with redundancy. this layout spreads your data to all drives and adds in *parity bits*. Let's say you have 5x1 TB drives, the data is spread between the five drives. Now, if a drive was to fail, the array can "guess" what was on the faulty drive and rebuild the array using the information stored on the other healthy drives.

Though having a layout setup like this has a few drawbacks, the first one is that you have a write speed penalty, because the RAID must compute and write the additional parity bits to the different drives, and the more drives you have, the more parity bits must be computed and written, thus, if you have more drives, your write speeds will be slower.

A RAID 5 array can support up to ***one*** drive failing at any given time. after a drive has failed, the array must be rebuilt, until then, you've got no protection. If two drives fail at the same time or before an array rebuild, your data goes kaput.

### RAID 6

That's a RAID 5 with double parity. it can support up two ***two*** drives failing at the same time or before an array rebuild. For this, you'd need a minimum of 4 drives. But as with most RAID array layouts, this comes with a drawback: Depending on the implementation, the write speeds will be, at best, the sames as a RAID 5, and at worst, two times slower than a RAID 5.

Read speeds are on-par with the likes of a RAID 5.

## The notion of space efficiency

Each RAID level store data differently, thus, one layout can be more efficient on storing data than another. the "*space efficiency*" is a percentage that represents the usable space that can be used for storing data.

| RAID level | Space efficiency | Minimum number of drives | Fault tolerance |
|:----------:|:----------------:|:------------------------:|:---------------:|
|   RAID 0   |         1        |         2 drives         |       None      |
|   RAID 1   |       1/*n*      |         2 drives         |   *n*-1 drives  |
|   RAID 5   |     1-(1/*n*)    |         3 drives         |     1 drive     |
|   RAID 6   |     1-(2/*n*)    |         4 drives         |     2 drives    |

Where *n* is the number of drives you have in the array.

## Redundancy does not always mean data safety

A redundant array can protect you from a hardware failure, but it ***cannot*** protect you from a software error. If your data were to be corrupted for whatever reason, the RAID array would still happily replicate it to all of your drives, and you'd have no way to prevent that without making regular backups to a separate media.
