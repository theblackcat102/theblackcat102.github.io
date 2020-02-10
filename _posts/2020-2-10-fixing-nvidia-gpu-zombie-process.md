---
keywords:
  - GPU
  - memory
  - zombie process
  - debug
comments: true
title: Kill zombie process using GPU memory 
cover_image: https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/nvtop_snapshot.png
---

I was repeating my experiments and I notice there'a a dead process hoarding GPU memory.

![](https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/nvtop_snapshot.png)

Using nvtop I was able to see the process using memory but when I try to kill the PID I get "No such process" error. Which isn't surprising since the parent process was already dead.

In order to access the child process you have to execute:

```
sudo fuser -v /dev/nvidia*
```

And find for /dev/nvidia[GPU ID] and you should get something like this:

```
/dev/nvidia0:        root       1587 F...m Xorg
                     gdm        1636 F...m gnome-shell
                     yourusername   9459 F.... nvtop
                     yourusername  14763 F...m python
                     yourusername  14764 F...m python
                     yourusername  25181 F...m python
                     yourusername  25929 F...m python
                     yourusername  25930 F...m python
                     yourusername  25931 F...m python
                     yourusername  25933 F...m python
                     yourusername  25934 F...m python
                     yourusername  25935 F...m python
```

There you have it, all the children PID are listed and should be able to kill them easily using kill command.

