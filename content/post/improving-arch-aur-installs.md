+++
author = "JMN"
categories = ["Tech"]
date = "2017-06-11T14:26:52-07:00"
description = "In which I attempt to make my aur installations more efficient"
featured = ""
featuredalt = ""
featuredpath = ""
linktitle = ""
title = "improving arch aur installs"

+++

I use Arch Linux on my poor seven year old laptop. My experience has been overwhelmingly positive... buuuuuuuuuuut, there have been a few times that my computers performance has driven me to the edge. Most of those experiences have been in attempting to install packages from the Arch User Repository or the AUR for short. 

Let's step back. Quick intro to Arch and a link to the projects home on the web: [Arch](https://www.archlinux.org/)
is a 'lightweight and flexible  Linux® distribution that tries to Keep It Simple.'

Arch has official package repositories and a community operated package repository(the AUR). To install official packages you can use pacman, a super simple package manager that will also manage package dependencies. It's great. 

To install packages from the AUR you first have to download the package source, compile it with makepkg, and then install it with pacman. I have no data for this but I'm going to guess that this process is one of the most significant barriers to entry for potential Arch users. It's really a question of patience and determination though; I have found that Arch has great documentation and a very active community. Take a look at the docs for the [Arch user Repository](https://wiki.archlinux.org/index.php/Arch_User_Repository). 

Anyhow, since many people are ~~not big fans of this manual compile and install process~~ stricken with sloth, there are a bunch of '[AUR helpers](https://wiki.archlinux.org/index.php/Arch_User_Repository#Build_and_install_the_package)' made to facilate/automate the installation of AUR packages. Anyhow, people love to argue over their AUR helpers. I use [packer](https://aur.archlinux.org/packages/packer/) because I saw it on a forum somewhere. Turns out it has been flagged 'out-of-date' since April 2017. Whoops.

All this to say that sometimes the installation process can be frustrating. Yesterday, I realized that a package I was installing was taking forever to compress. The compiled package will be archived and the makepkg script compress the compiled package so that it doesn't eat up space in its archived form. That's also the step that seems to take the longest in the installation of all my AUR packages. The [makepkg documentation page](https://wiki.archlinux.org/index.php/makepkg) has several suggestions for improving compile times that you should check out. In my case I adjusted [the number of cores being used for compression](https://wiki.archlinux.org/index.php/makepkg#Utilizing_multiple_cores_on_compression). 

I actually stumbled my way across the root root issue and this optimization. My installation of the python conda library was taking forever and the only feedback my package manager was giving me was a line informing me that compression was taking place. I checked htop to see why this took so long and found only a single core at 100% use. A short Google trip later led me to this makepkg documentation page and a couple [good](https://bbs.archlinux.org/viewtopic.php?id=215764) AUR issues discussion [pages](https://bbs.archlinux.org/viewtopic.php?id=127894). 

I'm seeing more cpu usage after my change and quicker compression times although I don't have data to show you. This whole post is just a reminder that I need to reach out to documentation more often. 
