# KSPIDS
PoC code for a simple user-based intrusion detection system for the Linux kernel. I wrote this code as an undergraduate student in 2008. It was designed for Linux 2.6. I hope it is still of use.


KSPIDS stands for *Kernel Service Profile Intrusion Detection System*. It is a kernel code patch for Linux systems that monitors the programs a service user (e.g. `www-data`) uses. It alerts you if - for example - your `www-data` user now executes something like `/bin/sh`. Please note that KSPIDS is based on my other project [FUPIDS](https://github.com/cdpxe/OpenBSDhacks).

# Features

Here is a list of KSPIDS' features:

- KSPIDS calculates an attacker level for every user (with uid 1...999) on your system. It will alert you via `syslog` if the attacker levels becomes high.
- KSPIDS has a profile of used executables for service accounts. If such a user uses too many new programms within a short time, the attacker level will raise. This is done because an attacker could overtake the account of a user and then uses some new compiled exploits or an editor the normal user never starts.
- If a user who never did anything before (for example `uucp`) is now active on your system, KSPIDS will notice and report it.
- An attacker cannot kill the KSPIDS system because it is kernel code. The attacker can also not unload an LKM because the code is directly implemented in the Linux kernel.
- KSPIDS is transparent for users, i.e. no user will notice the presence of KSPIDS.

# Installation
 
Patch your kernel with the KSPIDS patch, activate the option "Security / KSPIDS" in your kernel configuration, recompile the kernel, and boot it (but make sure to backup your previous kernel and make sure you can boot the other kernel, too (in the case something went wrong!).

# Results
 
You need to calibrate KSPIDS via *kspids.c*. If you skip this part, you will maybe see too many attack warnings or even not a single one.

# Demo output

See my [website](http://steffen-wendzel.blogspot.com/p/security-hacks.html#kspids) for some screenshots.
