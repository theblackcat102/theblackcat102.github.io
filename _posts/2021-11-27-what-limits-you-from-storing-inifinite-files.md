---
keywords:
  - OS
comments: true
title: Limits of files you can store in a directory
---

```
04/03/2022 Update: Instead of using ext4, you should simply consider other file format such as xfs, zfs, btrfs for high file counts storage
```

Its normal for a typical research projects to store each data as an individual file under a directory. Although this is not idea, no one seems to question what are the limits of such method.

### Ext4

Ext4 is the most commonly used format in linux environment nowadays so we will focus in finding the limit of files under a directory.

According to this [stackoverflow answer](https://stackoverflow.com/questions/466521/how-many-files-can-i-put-in-a-directory/466596#466596), ext4 limits is 2^32-1 (inode table maximum size) likely due to compatibility with 32-bit filesystem. 

> So the answer is 2^32 -1 or 4 billions right?

![](https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/file_size_limit_meme.png#center)


### Introducing Index node aka Inode

However under linux things doesn't work this way. In order to efficiently access each files, they are stored as index node or we typically call **inodes**. With this unique index number, we can do [symbolic link](https://linuxize.com/post/how-to-create-symbolic-links-in-linux-using-the-ln-command/) which points different files to the same inode id. Inode is also where you store the permissions, owner, group settings. 

Now the bad news is inodes are limited, but they usually comes with in a very large number. This default value grows proportionally with disk size. For example here's a list of inodes number I get in my machine using ``df -i``.

| Disk  | Storage Size  | Inodes Limit  | Inodes in used  | Storage Usage |
|---|---|---|---|---|
| Samsung 860  |  512G | 30,531,584  | 4,069,444  |  97% |
| WD Blue SSD  |  512G | 30,498,816  | 1,029,493  |  93% |
| WD Blue SSD | 1T  | 61,054,976  | 9,918,907  | 92% |
| WD Blue HDD | 6T  | 183,144,448  | 4,392,142  | 10% |

As you can see filling both of my SSDs almost full with hundreds of millions of files doesn't even come close to reaching the inode limit.

Unless you are storing billions of very small files ( ~ 1kB) inodes won't be a problem. If you are the 1% who have such problems, I would recommend you take a look into this [thread](https://unix.stackexchange.com/questions/26598/how-can-i-increase-the-number-of-inodes-in-an-ext4-filesystem) to create filesystem with larger inode size.


> So everything is fine right?

### Say hello to hash collision

This is practically CS data structure 101, so I would dwell into what hash collision is. 

Since a single directory can potentially hold up to 2^32 files, ext4 also maintains a hash table of size 2^32 to speed up filename search.


> This translate to subdirectory limits as well right?

### dir_nlink

As mentioned in [manpage about ext4](https://man7.org/linux/man-pages/man5/ext4.5.html) 

> Normally, ext4 allows an inode to have no more than 65,000
> hard links.  This applies to regular files as well as
> directories, which means that there can be no more than
> 64,998 subdirectories in a directory

So no, it doesn't

### Issues with ext4 high inode setup

Although setting to the upper limits of ext4 inode count seems to solve most of other stackoverflow problems, this doesn't solve mine.

Out of space errors still occur after reaching 15 millions of unique files in the filesystem. Using ``df -i`` shows inode counts using only 4% of total inodes. Hence I believe something is still missing which I failed to considered. 

I decided to use [XFS](https://en.wikipedia.org/wiki/XFS) instead for solving the problem once and for all, since it has built in dynamic inodes structure by sacrificing more storage space ( empty xfs filesystem uses about 15G space in a 8T hard disk ). So far I was able to store all 30M files without hurdles at all.

## Reading materials


1. [Ext4 high level design documentation](https://www.kernel.org/doc/html/latest/filesystems/ext4/overview.html)

2. [Simple filesystem introduction if you don't have time to read 1](https://teaching.idallen.com/cst8207/13w/notes/450_file_system.html)

3. [ext4: Mysterious “No space left on device”-errors](https://blog.merovius.de/2013/10/20/ext4-mysterious-no-space-left-on.html)