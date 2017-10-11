# How to make a disk image (from [ask Ubuntu](https://askubuntu.com) and [superuser](https://superuser.com))

## [First example](https://askubuntu.com/questions/19901/how-to-make-a-disk-image-and-restore-from-it-later/19910#19910)
`dd` is the low level utility that you can use to accomplish this task, it essentially 
a low level byte-for-byte copy utility. 
If you want the "UNIX" way of accomplishing this, then read on.

All references to the file system and hard disks are located locally on the virtual 
`/dev/` filesystem. 
There are a multitude of "nodes" in /dev/ that are interfaces to almost all the 
devices on your computer. For example, `/dev/hda` or `/dev/sda would` refer to the 
first hard drive in your system (hda vs sda depends on the hard drive), 
and `/dev/hda1` would refer to the first partition on your hardrive.

The most straight forward way to make a raw image of your partitions is to use 
dd to dump the entire partition to a single file (remember the OS access the 
partitions `/dev/sda1` through a file interface). 
Make sure you are on a larger partition or on a secondary drive and perform the 
following command:
```
dd if=/dev/hda1 of=./part1.image to backup (repeat for different partitions)
dd if=./part1.image of=/dev/hda1 to restore
```
You can use the exact same command to backup the entire hard disk (replace hda1 with hda). 
You can then use any compression program (gunzip, zip, bzip) to compress the file for 
storage. 

You can use this same technique to make rote copies of entire partitions to make 
clones of your computer.

There is one limitation though, when restoring the backup, the partition needs to 
be the same size (or bigger) as the partition you took the image from, so this 
limits your options in case of a restore. 

However, you can always expand the partition after you've restored the backup using 
gparted or parted. 

The picture gets even muddier when you are trying to restore entire disk copies,
however, if you are restoring the backup to the same exact hardrive you don't need 
to worry about this at all.

## [Second example](https://superuser.com/questions/314480/in-linux-how-do-i-create-restore-an-image-snapshot-of-my-entire-drive/314482#314482)
You can simply do `dd if=/dev/sda of=/path/to/target/backup` if you know you have 
the room where you are trying to put it. 

You could also do `dd if=/dev/sda | bzip2 > /path/to/target/backup` to compress 
on-the-fly. 

This might take some time though.

Or, you could do `tar --preserve-permissions -cjf backup.tar.bz2 /what/to/backup` 
as a user that has all the neccessary read permissions. Take your pick.

Addendum: I recently bought a new laptop, preinstalled with Vista. I figured I 
wanted to preserve vista somewhere, in case I wanted to try it out at some point, 
so the first time I booted the computer (with a linux livecd), I did this:

```dd if=/dev/sda | ssh 10.0.0.1 "bzip2 > ~/vistadrive.bz2```

This was on a fast local network, of course. Otherwise it would have been more 
prudent to compress before transmission:

```dd if=/dev/sda | bzip2 | ssh 10.0.0.1 "cat > ~/vistadrive.bz2```
