---
layout: post
title: Linux Basic how to clear understand free command
---

{{ page.title }}
================

<p class="meta">23 March 2016 - Beijing</p>
Free is a comman tool to  Display amount of free and used memory in the system.

free displays the total amount of free and used physical and swap memory in the system, as well as the buffers used by the kernel.  
The shared memory  column  represents  the  ’Shmem’  value.   The available memory column represents the ’MemAvailable’ value.

When I type 'free -m', 

free -m
=============================================================================
             total       used       free     shared    buffers     cached
Mem:         64104      52579      11525          1        103      32907
-/+ buffers/cache:      19568      44536
Swap:        16383      14256       2127
==============================================================================

total 64104 --> The system totally have 64G memory,total(52579) = used(52579) + free(11523) 
used   --> memory in use by the OS.(52579)
free   --> memory not in use by the OS.(11525)
buffers--> buffers counts pending file/network writes and cached counts recently read/written blocks held in RAM to save future physical reads (103)
cached --> something that has been "read" from the disk and stored for later use or tmpfs filesytems,or uesd by virtual machines

-/+ buffers/cache 
 used -->  It gives the original value for used minus the sum buffers+cached  used（52579）-(buffers（103）+cached(32907))
 free -->   the original value for free plus the sum buffers+cached,          free(44536) + (buffers（103）+cached(32907))
 Thess values are more meaningful than above values
 
 
 ==================================================================================
 Swap 
 Swap space in Linux is used when the amount of physical memory (RAM) is full. 
 If the system needs more memory resources and the RAM is full, inactive pages in memory are moved to the swap space. 
 While swap space can help machines with a small amount of RAM, it should not be considered a replacement for more RAM.
 Swap space is located on hard drives, which have a slower access time than physical memory.
 
 
 /proc/sys/vm/swappiness default 60， vary  from 0 -100， the OS will use swap sapce more  aggressivly  if the value is more larger
   used --> swap used 14256
   free -->  swap free 2127
   
[Discuss this post on StackOverflow](http://stackoverflow.com)
