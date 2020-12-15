+++
title = "Installing VMWare & Kali on Linux (Pop_os! specifically)"
date = "2020-12-15"
description = "How to download, install VMWare and Kali on top of that"
tags = [linux, kali, vmware]
+++

# Introduction
I'm sure you have this problem whenever you install your favourite linux distribution: "How do I run Kali on top of this hunk-a-junk?" if you are me. Then again, if you are me, we are in deep six friemd. 

'nyhow. To do that we have two options. Either grab an iso, burn it to an usb (because CD/DVD's are so blase now) and do whole partitioning shenanigans. I don't like this option for many reasons, primarily it doesn't make sense. Sure as a pentester I don't have anything to hide, anywhere I don't have permission to test; I don't - but if I am putting myself in the shoes of a redteamer this means that I need to dump my whole machine if compromised/traced/sniffed etc. Also there is the risk of hardware incompatibilities and so on. 

Second option is running kali as a virtual machine on top of some abstraction layer. In this case we have two options, VMWare and VirtualBox. As far as I saw, VMWare offers a near-hassle free experience but Virtualbox has this snapshotting ability that is juuust sexy. With that we can save a *state* of a machine before doing something interesting. 

I personally do VMWare setup and launch a Kali Virtual Machine. In this article I want to show you how to do it. 

# Grabbing VMWare Player
To run our Kali Virtual Machine we only need VMWare Player. It is free to download from [VMWare](https://www.vmware.com/)'s own site. It makes us download a file ending in `.bundle`. To install this we first turn it into an executable and run it as system administrator. Else it yells at us and doesn't install:

	chmod +x VMWARE-DOWNLOADED.bundle
	sudo ./VMWARE-DOWNLOADED.bundle

We see a progress bar and when it's done, we finish the installation step. Then we run it and accept the licences and other stuff. Then, and only then, we finally are able to run our Vmware Player.

# Grabbing Kali Virtual Machine
To download this I use `qbittorrent` and Kali's torrent file. We download this file from [Offensive Security](https://www.offensive-security.com)'s own page. I prefer this over HTTP download because my previous experience shows that sometimes HTTP download can bork and give you an incomplete file which causes problems. 

To install qbittorrent I use the good ole `apt-get`

	sudo apt-get install qbittorrent

Post installation I open the file from qbittorrent and wait until it's done. The file itself is in 7z format. Most distributions have built-in support for 7zip extraction. But bear in mind that this 2gb file (at the time of this writing at least) will take some time to extract. 

I move the folder to `Documents/VMs/Kali` location - because unlike in real life I am tidy in my folder management in my computers. 

# Running the Virtual Machine
So let's chip in. To link our extracted file with our VMWare Player:

- Run the VMWare Player
- Select *Open a Virtual Machine*
- Move the file browser to the location we moved our files
- Click the machine file
- Select *I copied it*

We are golden! Bear in mind that the default uname:pass is `kali:kali` and the keyboard layout is set to US. Also some update won't hurt. 

See ya in the flip side m8s!
