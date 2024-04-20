---
layout: post
title:  "Restoring Windows EFI System Partition"
date:   2024-04-20 18:15:10 +0300
categories: windows administration
---

# Comprehensive Guide: Restoring Windows EFI System Partition

## Introduction
In the realm of system administration and programming, encountering challenges with the EFI (Extensible Firmware Interface) system partition is not uncommon, especially for those managing Windows environments. Whether due to inadvertent deletion, corruption, or other unforeseen circumstances, restoring the EFI system partition is crucial for the proper functioning of the operating system. In this comprehensive guide, tailored for programmers and system administrators, we'll provide a detailed walkthrough of the step-by-step process to restore the EFI system partition on your Windows PC using command-line tools.

## Step 1: Boot from Windows Installation Media
To initiate the restoration process, boot your system using the Windows installation media. Irrespective of the Windows version—be it 7, 8, 8.1, or 10—the procedure remains consistent. Upon reaching the installation screen, invoke the command prompt by pressing `SHIFT+F10`.

## Step 2: Accessing Command Prompt
With the command prompt interface activated, it's time to delve into the core of the restoration procedure. Commence by executing the `diskpart` command to initialize disk partitioning operations.

## Step 3: Partition Management
Execute `list disk` to enumerate all available disks on your system. Identify and select the relevant disk for the addition of the EFI System partition by utilizing the `select disk #` command, replacing `#` with the disk number.

Subsequently, list the partitions on the selected disk using `list partition`. Choose the Windows OS partition or the appropriate data partition (depending on the system configuration) by issuing the `select partition #` command.

To carve out space for the EFI partition, shrink the selected partition by the desired magnitude (e.g., `shrink desired=100`). Then, create a new EFI System partition with a size of 100 MB using `create partition efi size=100`.

## Step 4: Formatting and Assigning Drive Letters
Upon creating the EFI partition, proceed to format it for utilization. Employ the `format quick fs=fat32` command to format the partition with the FAT32 file system, ensuring compatibility with EFI.

Assign a drive letter to the EFI partition (e.g., `assign letter=s`) for seamless accessibility.

## Step 5: BCDBoot Configuration
The pivotal step entails configuring the boot files. Enumerate the partitions and volumes to ascertain the volume letter corresponding to the Windows OS installation.

Execute `bcdboot X:\windows /s S:` to replicate the boot files from the Windows partition (substitute `X` with the volume letter of the Windows OS partition) to the EFI System partition. This command also orchestrates the creation of the BCD store within the EFI partition.

## Step 6: Finalizing the Process
With the successful replication of boot files, it's imperative to conclude the restoration endeavor. Eject the Windows installation media and reboot the system. Enter the BIOS settings and designate the SSD (or the pertinent drive) as the First Boot Device, ensuring booting from the restored EFI partition.

## Conclusion
The restoration of the EFI System partition is paramount for preserving the integrity and functionality of your Windows environment, particularly in programming and system administration domains. By meticulously adhering to the steps elucidated in this guide, programmers and system administrators can proficiently reclaim the EFI partition, fostering smooth system booting. It is imperative to exercise caution while executing commands and validate actions to avert inadvertent consequences.

---

*Original Forum Post:* [Moving or Recreating EFI partition](https://www.tenforums.com/installation-upgrade/52837-moving-recreating-efi-partition.html#post698505) by **Kyhi**

