---
layout: post
title:  "Build your own RAID Array in Fedora, using LVM."
date:   2018-08-07 15:40:00
categories: [code]
comments: true
---

This guide not only demonstrates the creation of a RAID5 array in Fedora, but also explains everything we need to know to master LVM.

#### What is LVM?

LVM stands for Logical Volume Manager, and it is the default way of partitioning storage space in Fedora. LVM provides the tools to create virtual block devices from the physical ones, and much more.

<!--more-->

LVM has three main components:

* Physical Volume (PV) - Physical volumes are directly associated with physical block devices.
* Volume Group (VG) - Physical volumes can be grouped into Volume Groups.
* Logical Volume (LV) - Logical Volumes are the end-products of this chain. LV's use the space available in Volume groups.

### Creating RAID5

We will be creating RAID5 array, but these steps are almost exactly the same for any other RAID level.

Although we could create RAID5 array with any number of hard drives (greater than 2) let's assume that we have four for the sake of simplicity, since 4 devices define [standard RAID5](https://en.wikipedia.org/wiki/Standard_RAID_levels#RAID_5).

#### Preparing the devices

First we need four empty block devices, let's assume that these are:

* `/dev/sdc`
* `/dev/sdd`
* `/dev/sde`
* `/dev/sdf`

_(Useful command to display information about HDDs: `lsblk`)_

We can either use whole hard drives, or create partitions and then use those. We would be creating partitions, if for example our drives were not identical.

* **Using the whole disk:** In order to use the whole disk, it has to be empty - without partitions. We can achieve this in several ways, for example we could use `dd` to zero out blocks in question. In our example we will use `gdisk`:
  * `$ sudo gdisk /dev/sdc` -> Now we are in the gdisk interface, we can take a look at available commands with `?`. We need to enter the advanced mode with `x` command, and then use `z` to "zap (destroy)" the partition table **and all the data on the hard drive**.
  * Repeat the above step for all the drives.
* **Using partitions:** We could create LVM RAID5 with HDDs of sizes 1TB, 2TB, 3TB and maybe another 2TB, where we would create 4 partitions of the same sizes and then use those. We will have some leftover space on multiple drives, which we could then combine into a single logical volume and use it for storing data that doesn't need to be completely secure, like in an array.
  * Create 4 partitions of the same size using a tool of of our choice, in this example we will use gdisk. Start with the smallest of the drives, and create a partition that spans over the whole drive (default options)
  * `$ sudo gdisk /dev/sdc` -> Use the `?` command to display help, use `o` to create a new partition table (delete all the current partitions on the disk and start from scratch) and `n` to create new partitions. Follow the guided steps to create partitions of the same size. Hit `w` to write these changes to disk.
  * Now we will repeat the above step for the rest of the drives, where we can use the first and last sector identical to the smaller disk, to achieve exactly the same size.

#### Create Physical Volumes

Now that we have the hard drives ready, we can create physical volumes (PV) on all of them. We can do that with a single command:
```
$ sudo pvcreate /dev/sd[cdef]
```
The `[cdef]` is a list of last letters of our devices.

#### Create a Volume Group

The next step is to group these physical volumes into a single volume group. Here we can peek into the manual page `man vgcreate` to take a look at available parameters. The most notable one is the `--physicalextentsize` or `-s` where the description here does not tell us a whole lot, but we can find out everything about it in [the documentation](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/logical_volume_manager_administration/lv_overview). To save some time, the important info is that extent is kind of a unit that directly links a physical volume, with a logical volume. And they can have size. It is good practice to avoid having millions of extents, so we should increase this size depending on the size of our array. In our example we have four 4TB HDDs, so let's use 64MiB for extent size: `-s 64m`. The `raid5vg` is the name of our new volume group. And we can use the same sneaky regular expression we used for physical volumes to not have to specify every single one of them.
```
$ sudo vgcreate -s 64m raid5vg /dev/sd[cdef]
```

#### Create the Logical Volume

Let's take a look at the man page again! `man lvcreate` We can see some obvious parameters that we will need, such as `--name` or `--type`. These will be the name of our logical volume, and the type. The type should be `raid5`, right? Next parameter of interest is `--size` however we will not use it, we will use `--extents` because the size parameter is just an alternative way to specify extents, which gives us more options. We want to consume our whole volume group, so we can use `100%VG`. The last interesting parameter is `--stripes` which specifies how many of those physical volumes do we want to use. Since we have raid5, it assumes one parity drive already, so in order to use all four drives, we need four minus one for parity: `3`. The last argument is the name of our volume group `raid5vg`
```
$ sudo lvcreate --type raid5 --name raid5lv --extents 100%VG --stripes 3 raid5vg
```

#### Creating a filesystem and mounting it

We're almost done, all that's left is to create a filesystem of our choice. Let's use ext4 and mount it at /mnt/raid
```
$ sudo mkfs.ext4 /dev/raid5vg/raid5lv
```
And that's the path to our new logical volume, simple, isn't it?

Create the directory where we will mount our new array.
```
$ sudo mkdir /mnt/raid
```

In order to permanently mount it, we need to add a line into the `fstab`. Also, `vim` is awesome.
```
$ sudo vim /etc/fstab
```
Add the following line, where we can use mapper as a path to the device, then the folder where to mount it in the second column, filesystem type in the third, and then default mount options. Nothing fancy.
```
/dev/mapper/raid5vg-raid5lv   /mnt/raid   ext4   defaults   0 0
```

This will mount everything in `/etc/fstab` - an important test before rebooting computer!
```
$ sudo mount -a
```

#### Done!

These are useful:

* `pvdisplay`, `vgdisplay` and `lvdisplay` will display info about all the PV's, VG's and LV's respectively.
* `pvs`, `vgs` and `lvs` throws out a table with info, refer to the manual page on how to specify columns, etc...
* We can use `lvs` to query whether our array is healthy, for example:

```
$ sudo lvs raid5lv -o 'lv_name,copy_percent,vg_missing_pv_count'
  LV     Cpy%Sync  #PV Missing
  raid5  100.00              0
```

What next? Next we could set up monitoring, automated emails in case of failed drive. But that's a whole another article for another time. I just use a cron script that checks for failed drives and leaves a message for me. To get something useful for such script, we can simply add an `awk` to the above example:

```
lvs raid5lv -o 'lv_name,copy_percent,vg_missing_pv_count' | grep raid5lv | awk '{print $3}'
```

Thanks for reading! Feel free to shoot me a message on IRC (Freenode) `Rhea` or on [Discord](https://discord.gg/fedora) `Rhea#1234` should you find yourself in need of more answers **:]**

