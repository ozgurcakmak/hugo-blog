+++
title = "Mounting HFS+ (Mac) filesystem on Linux"
date = "2020-12-19"
description = "How to mount HFS filesystem on Linux (Pop_os)
tags = ["Linux","Mac","Mounting"]
+++

# Introduction
A few months ago I replaced my aging Macbook Pro's harddisk with a SSD. But the problem was I had my audiobook/lecture files in the replaced disk. To switch the files I bought a SATA-to-USB cable and it arrived today. Here's how I did it.

# After action report
## Installing hfsprogs
I used the cable on my Macbook Pro and saw that I could mount it and copy the files with no problems. When I switched to my main tower I saw that it did neither mount it automatically nor copy the files. Some research yielded that I should install the `hfsprogs` package from the repositories:

	sudo apt-get install hfsprogs

## First Tries with mount
The guide says that I should run 

	sudo mount -t hfsplus -o remount,force,rw /dev/sdb2 /home/f4stjack/mac

command to get it mounted but it never worked for me. I restarted my computer, hoping that maybe this will do the trick but alas. I used it with `remount`, without `remount` and other option changes but nothing worked. All I got was a superblock error and nothing else. 

Then a bulb appeared on my mind. What if I repaired the disk - against my judgement.

## Repairing the disk
To repair the disk we use this command:

	sudo fsck.hfsplos -f /dev/sdb2

Lo and behold it found two minor errors and repaired it. Then, with little hope of it working, I opened the `Disks` program and hit the mount button - as far as I see it is better to reach for the low hanging fruit before trying harder.

You know what? It worked. Everything was mounted, I could access the file system and everything was golden.

## Copying the files
When I was doing my research I read that the copied files had to undergo a `chmod` operation. But nowadays it seems it doesn't work like that. When copying a folder - or a group of folders - the system asks for sudo access for every new main folder it creates. So if you have 3 main folders consisting other folders, you'll get 3 prompts. 

A `ls -alh` showed that those copied files were indeed mine.

And that is how I solved this problem. Thank you for reading.
