---
layout: post
title: "A nice, gentle tutorial to synchronize files and directories across OSX and Linux"
---

# A nice, gentle tutorial to syncronize files and directories across OSX and Linux

If you want to go straight to the point [click here](#sofast)

Wassup piiiiiiiiiiiiiips

It's ya boi c to the mf p : cqncpdp (yeah that's my haxker ninjass killer name)
.

This article is really useful, you should read it. It's the best one out there.
Well, it's probably the only one (haha got em).

So today we are going to tackle a pretty specific problem : files synchronization
across OSX and Linux.

> **A problem ?** Is this 2006 again ? Have you ever heard of
> dropbox ? or google drive ? or mediafire ? or ...

### ShhhuTFU

no it's not 2006, but who wants to pay so a company can have access to your
secret special files ? to your top secret ideas worth billions of dollars  ?

> What about git and github or gitlab or ..., it's free ?

Git is cool, but when you are working on several computers you don't want to
commit and push every time you press the save button.

## it's time to stop the bullshit and to start the real shit

toolbox :

* computer
* bash
* usb flashdrive/external hard drive
* rsync

I could just make a tutorial on how to use rsync, because it's the tool we are
going to use to sync our files. The problem is if we want to make it works, we
need to put a little extra work, which is the point of this article.

warning use at your own risks

##mounting your external device on linux

## change your user ID (UID)

- type id on your mac, remember the uid we will call him JEFF
- boot linux, hold shift, enter the recovery mode
- select enable networking, yes
- then root to access a root console
- type id and remember your uid call him ananass
- change the userid and set it to jeff:  `usermod -u 2005 JEFF`
- now you've changed the uid, you need to change your current file uid to your
new one with : `find / -user ANANASS -exec chown -h JEFF {} \;`
- Any UID values below 1000 are treated as system type users. These are hidden from the Login-screen.
- open /etc/login.defs and search for `UID_MIN` in the text file. Change that value from 1000 to 501
- add your username as a sudoer : `usermod -aG sudo username`
- once it's done, type exit and boot
- now linux only seems to be able the guest session ?
- Press Ctrl+Alt+F3 and login into the shell.
- Now run `ls -lA`. If you see the line
`-rw-------  1 root root   53 Nov 29 10:19 .Xauthority`
then you need to do `sudo chown username:username .Xauthority` and try logging in.

## create a bash script

how to use rsync
create a small alias, and hope it's done

sources :
* https://askubuntu.com/a/92558
* https://askubuntu.com/a/106937
* https://askubuntu.com/a/223634
* https://www.cyberciti.biz/faq/linux-change-user-group-uid-gid-for-all-owned-files/
* https://www.digitalocean.com/community/tutorials/how-to-create-a-sudo-user-on-ubuntu-quickstart





















