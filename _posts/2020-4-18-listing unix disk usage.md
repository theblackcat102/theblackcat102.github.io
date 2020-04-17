---
keywords:
  - Linux
  - Unix
  - Ubuntu
  - space usage
  - disk usage
comments: true
title: Listing disk usage under UNIX system
---

TLDR; **du -xa / | sort -n -r | head -n 30** list the top 30 disk hogger files under your system disk.

Sometimes is kinda painful when you need to do disk space management in a remote server. Since **ls -alh** commands shows little information about a folder size. 

## du ( disk usage )

I think a lot of people are quite comfortable with using **du** command. 

A simple list of current directory disk usage can be **du -sh ./**

Which list a summary ( -s ) of disk usage under human readable form ( -h )

If you wish to list all the files size including directory size, you can remove the summary flag (**s**) and you should be greeted with a large list of files with their repective disk size.

But what if your system disk and full and you wish to find out hidden logs that was taking a few hundreds Gigs of size?

Well this works right?

```
du -a / | sort -n -r | head -n 30
```

Yes, but when you have muliple disk mounted around the system, large files from these system will be shown as well. Hence you need an extra **-x** flag to only traverse files under the current system disk. 







