---
layout: post
title: Linux Kernel Build
date: 2021-12-18 05:19:42.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
tags:
- build
- c
- compile
- kernel
- linux
- make
- virtual machine
author:
  display_name: deparkes
permalink: "/2021/12/18/linux-kernel-build/"
---
<h2>Build Custom Linux Kernel</h2>
I was interested to see how to do a Linux Kernel Build from the source code. I followed <a href="https://kernelnewbies.org/FirstKernelPatch">this guide</a> and while it mostly made sense there were a few areas that I found less clear or had unexpected errors.
<h2>Initial Set up</h2>
I used <a href="https://deparkes.co.uk/2015/10/15/linux-virtual-machine/">VirtualBox</a> rather than VMWare suggested in the guide, but don't think didn't encounter many differences. Some of the later steps are quite resource intensive, so set your virtual machine <a href="https://superuser.com/questions/926339/how-to-change-the-ram-allocated-to-an-os-in-virtualbox">memory</a> , <a href="https://superuser.com/questions/823109/how-to-allocate-more-processor-power-to-my-ubuntu-based-virtualbox-system-in-w">CPU</a> and <a href="https://www.howtogeek.com/124622/how-to-enlarge-a-virtual-machines-disk-in-virtualbox-or-vmware/">Virtual Disk</a> relatively high if you can spare it on your host machine.
I used a <a href="https://lubuntu.me/">lubuntu</a> install with 10GB virtual hard disk initially, but upped that to 20GB when I ran out of space cloning the repo.
The guide I followed is actually for submitting patches. This might be something I build up to, but realistically I didn't think I would be submitting patches any time soon, so I skipped the email setup.

<h2>Cloning the Kernel Repo</h2>

<h3>Performance Issues</h3>

The guide recommends cloning the repository on a fast, stable, unlimited connection. They weren't joking when they said it took over 5GB!
I didn't follow the <a href="https://kernelnewbies.org/OutreachyfirstpatchAlt?action=show&amp;redirect=OPWfirstpatchAlt">guidance</a> on sensible virtual disk space and ran out of space on my first attempt.
<a href="https://superuser.com/questions/130381/compiling-the-linux-kernel-how-much-size-is-needed">Read more about how much space the kernel requires for building</a>.
As I was running a virtual machine, i think I may have had the issue that it<a href="https://jlemke.com/virtualbox-guest-machine-freezes/"> goes into pause mode</a> when it it struggling with memory. This was fixed by upping the amount of memory I gave it.

<h3>Name Resolution Error</h3>

On doing

```bash
git fetch origin
```

I got an error:

```
fatal: unable to look up git.kernel.org (port 9418) (Temporary failure in name resolution)
```

I checked the origin with

```bash
git remote -v
```

And also tried to change to https version of origin (rather than 'git:' in the guide):

```bash
git remote set-url origin https://git.kernel.org/pub/scm/linux/kernel/git/gregkh/staging.git
```

This still was not working, so tried pinging <a href="https://git.kernel.org" target="_blank" rel="nofollow noopener noreferrer">git.kernel.org</a> in the virtual machine and got the error 'Temporary failure in name resolution'. Pinging the IP address of git.kernel.org (via <a href="https://isc.sans.edu/ipinfo.html?ip=git.kernel.org">this website</a>) gave the same error.
This still didn't work and after mucking about with pinging and checking IP addresses I found <a href="https://askubuntu.com/questions/1012641/dns-set-to-systemds-127-0-0-53-how-to-change-permanently">this solution</a> to temporarily change the <a href="https://www.cloudflare.com/learning/dns/what-is-a-dns-server/">nameserver</a> to 8.8.8.8.
Finally, I came across <a href="https://linuxconfig.org/in-depth-howto-on-linux-kernel-configuration">this page</a> which mentions there had been issues with kernel.org, which could be related to the same problem
If you keep having problems, you could use the <a href="https://github.com/torvalds/linux">GitHub mirror</a> if you just want to be able to build recent-ish kernel code.
<h2>Updating the build configuration</h2>
As per the guide, I found a kernel config file in /boot/and copied it to .config in the cloned folder:

```
git/kernels/staging/staging/
```

working directory with

```bash
cp /boot/config-uname -r* .config
```

It is also <a href="https://kernelnewbies.org/OutreachyfirstpatchSetup">a good idea</a> to update <a href="https://cateee.net/lkddb/web-lkddb/LOCALVERSION.html">CONFIG_LOCALVERSION</a> in the new config. This appends an extra label to the name of any kernel built which helps avoid name clashes.
<h2>Building The Kernel</h2>
<h3>Setting the Config</h3>
If you run 'make' without a .config file, it will complain that there isn't one there.
I think the config file I used (from lubuntu 20.04) was quite out of date compared to the kernel as there were many questions not configured and appeared as 'NEW'.
Having no idea what I was doing, I just accepted the defaults for each question until the build got started.
Lots of them seemed to be about including compatibility with various hardware.
<a href="https://kernelnewbies.org/OutreachyfirstpatchSetup">This page</a> actually suggests some other ways of setting up your config including automatically accepting defaults on new configuration options or only building a minimal version to speed up build time.
In my case I initially copied the configuration from an Ubuntu build, which is likely to be fairly generalised and include more than a more bespoke option might need.
(In retrospect, I may have been better starting from the same kernel version as my distro (lubuntu 20.04) so I wouldn't see so many 'NEW' config options.)
<h3>Fixing Certs Issues</h3>
After building for a while, I got an error:

```
No rule to make target 'debian/canonical-certs.pem', needed by 'certs/x509_certificate_list'
```

From <a href="https://askubuntu.com/questions/1329538/compiling-the-kernel-5-11-11">this link</a> it looks like I need to update the config to set
This seemed to do the trick, although I also needed to update the config for

```
debian/canonical-revoked-certs.pem
```

<h3>Pahole is not available</h3>
This failed with an error that 'pahole is not available'. Thankfully there was a <a href="https://stackoverflow.com/questions/61657707/btf-tmp-vmlinux-btf-pahole-pahole-is-not-available">stackoverflow question</a> with an answer - install the '<a href="https://ubuntu.pkgs.org/21.04/ubuntu-universe-arm64/dwarves_1.20-1_arm64.deb.html">dwarves</a>' package.
Installing dwarves did the trick and the rest of the build went ok.
<h3>Build Time</h3>
To get a feel for how long the build time might be, check out these <a href="https://ubuntuforums.org/showthread.php?t=650461">here</a> and <a href="https://unix.stackexchange.com/questions/125790/do-i-have-to-compile-the-kernel-every-time-even-for-a-small-change">here</a> . It really depends on the computer/resources you are using and how much you are compiling.
In my case the Linux kernel build took several hours and then ran out of space on my virtual machine. I tried again with a VM with more resources (8GB RAM, 4 cpu cores) and it was done within about 30 minutes.
<h2>Modifying a Driver</h2>
As I was running on a virtual machine I followed the guide to change the e1000 driver, which worked without issues.
<h2>Reverting to your original kernel</h2>
To get back to your original kernel, you can usually hit 'Escape' during boot to <a href="https://forums.linuxmint.com/viewtopic.php?t=90752">bring up the grub menu</a>.
If you set a CONFIG_LOCALVERSION when setting your configuration, this will have been appended to the kernel name.
Once booted into your old/original kernel you can remove the one you build.
For kernels installed with your package manager (e.g. during an upgrade) this can be done via <a href="https://www.cyberciti.biz/faq/debian-redhat-linux-delete-kernel-command/">these instructions</a>.
However, in our case we need to do something a little different and <a href="https://askubuntu.com/questions/594443/how-can-i-remove-compiled-kernel">manually remove the kernel</a> and references to it.
The suggested method on stackoverflow is to

```bash
locate -b -e 4.4.6-my-kernel | xargs -p sudo rm -r
```

and enter 'y' to accept the deletions. To play it safe you may want to just run

```bash
locate -b -e 4.4.6-my-kernel
```

first to confirm what it finds.
This uses the 'locate' package which you may need to <a href="https://askubuntu.com/questions/215503/how-to-install-the-locate-command">install as the 'mlocate' package</a>.
<h2>Cleaning build folder</h2>
To clean the build folder, use

```bash
make clean
```

This<a href="https://www.gnu.org/software/automake/manual/automake.html#Clean"> should remove</a> the build artifacts and leave just the source code.
Read more about '<a href="https://www.kernel.org/doc/html/latest/kbuild/makefiles.html#kbuild-clean-infrastructure">kmake</a>'
<h2>Further reading</h2>
<h3>Building your Own Kernel</h3>
<a href="https://opensource.com/article/19/8/linux-kernel-21st-century" target="_blank" rel="nofollow noopener noreferrer">https://opensource.com/article/19/8/linux-kernel-21st-century</a>
<a href="https://wiki.ubuntu.com/Kernel/BuildYourOwnKernel" target="_blank" rel="nofollow noopener noreferrer">https://wiki.ubuntu.com/Kernel/BuildYourOwnKernel</a>
<h3>Speeding up the build time</h3>
<a href="https://stackoverflow.com/questions/24321336/most-lightweight-linux-kernel-os" target="_blank" rel="nofollow noopener noreferrer">https://stackoverflow.com/questions/24321336/most-lightweight-linux-kernel-os</a>
<h3>More on configuration</h3>
<a href="https://linuxconfig.org/in-depth-howto-on-linux-kernel-configuration" target="_blank" rel="nofollow noopener noreferrer">https://linuxconfig.org/in-depth-howto-on-linux-kernel-configuration</a>
<a href="https://linuxconfig.org/custom-kernels-in-ubuntu-debian-how-when-and-why" target="_blank" rel="nofollow noopener noreferrer">https://linuxconfig.org/custom-kernels-in-ubuntu-debian-how-when-and-why</a>
</div>
