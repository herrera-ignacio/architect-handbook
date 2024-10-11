# RAID

## Overview

*Redundant Array of Inexpensive/Independent Disks* is a **data storage virtualization** technology that combines multiple physical disk drive components into one or more logical units for the purposes of **data redundancy**, **performance improvement**, or both.

> This was in contrast to the previous concept of highly reliable mainframe disk dives referred to as *Single Large Expensive Disk (SLED)*.

Data is distributed across the drives in one of several ways, referred to as RAID levels, depending on the required level of redundancy and performance. Each scheme, or RAID level, provides a different balance among the key goals: **reliability**, **availability**, **performance**, and **capacity**.

> RAID levels greater than RAID 0 provide protection against unrecoverable sector read errors, as well as against failures of whole physical drives.

RAID can also provide data security with SSDs without the expense of an all-SSD system.

> For example, a fast SSD can be mirrored with a mechanical drive. For this configuration to provide a significant speed advantage an appropriate controller is needed that uses the fast SSD for all read operations.

Many RAID levels employ an error protection scheme alled "**parity**", a widely used method in information technology to provide **fault tolerance** in a given set of data. Most use simple XOR, but RAID 6 uses two separate parities based respectively on addition and multiplication in a particular *Galois field* or *Reed-Solomon error correction*.

## History

The term RAID was introduced in the 1988 paper *"A Case for Redundant Arrays of Inexpensive Disks (RAID)"* where it's argued that the top-performing mainframe disk drives of the time could be beaten on performance by an array of the inexpensive drives that had been developed for the growing personal computer market. Although failures would rise in proportion to the number of drives, by configuring for redundancy, the reliability of an array far exceed that of any large single drive.
