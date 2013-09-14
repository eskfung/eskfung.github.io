---
layout: post
title: Hijack This
categories: twiki
---

HiJack this is a handy tool to view startup entries in the registry, non-MS services, BHO's, and more. It works by listing various files that modify browser welcome pages, run on startup, and hijack your internet among other things. It is typically the first program I will run because of its all-encompassing prowess in identifying trouble. This is an advanced tool that **PERMANENTLY DELETES** the offending file, so please use caution when modifying anything in it.

There are numbers listed on the left side of all of the listings, and these relate to their function. Below will be a brief intro to some of the more important codes to remember. Don't worry if you don't have examples of all of the codes listed. We'll go through and determine the malicious ones afterwards.

## Function by Code:

* `R0, R1, R2, R3` - IE Start URLs
* `N1, N2, N3, N4` - Mozilla Start URLs
* `01` - Hosts file redirection
* `02` - Browser Helper Object
* `03` - Internet Explorer toolbars
* `04` - Startups
* `010` - Winsock Hijacker
* `013` - IE Default Prefix hijack
* `014` - "Reset Web Settings" hijack
* `015` - Unwanted site in Trusted Zone
* `017, 018, 019` are also all hijackers

We're now going to collect bad files, so just click on the ones you want to remove, and click on the "fix checked" button at the very end.

![HiJackThis Screenshot][hijack-ss]

## The Results

* First off, in the `R0-R3` or `N1-N4`, do you see any websites that don't belong? It should only show files that you load when you first open your browser. It's okay to have the same site listed multiple times.
* `01`'s are bad. A hijacked host file means that when you type in a certain website, you're going to get redirected to another site. Select these.
* In the `02` section, click on anything that says "no name" AND "no file".
* If you use toolbars, then you'll see something in `03`. If you don't recognize it or you don't want it, click on it here.
* `04`'s are files that start up with your computer. You're better off modifying in msconfig, but if you don't even want the listing to show up in msconfig, then you can click on it here. You're not deleting the program, but you're deleting the part where it starts up whenever you turn on the computer.
* `010, 013, 014, 015, 017, 018, 019` just click on them unless you recognize the file.

Click on "fix checked", and you're done!

[hijack-ss]: /images/hijackthis_results.png
