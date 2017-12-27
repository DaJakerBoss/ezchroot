# ezchroot || EasyChroot
## A simple script to ensure proper chroot-ing

I thought I might try my hand in bash scripting since I had made a script like this before.
So Keyboard hit the `nano` and off I went.

This script ensures the proper chroot environment for any one with chroot.
This script currently has extra support for Debian and SUSE based systems, but should work with any `bash`.

The easychroot_changelog.txt should have everything you need for changes I have made, and version history. Eventually I will split this up into a stable and beta branch but for now who cares as long as it works.

Enjoy!

###Usage
EasyChroot must be run as root. Simply running `sudo ./ezchroot` in its directory should do the trick.

For everywhere I have forgotten to give you an option for Yes/No, "y" always means Yes, and "n" always means No

If you are running EasyChroot on WSL, you must have mounted the ext4 partition of your target beforehand. If you are unable to do that, you can simply use Ext2Fsd and mount it beforehand.

If you are running EasyChroot on Linux, the command `parted` must be installed. You can do this with the script, so no worries if you haven't.

To continue, when you enter your partition to mount it must be in the form of 'sdXY'

As a rule of thumb, X will always be a lowercase letter, and Y will always be a number. These characters will follow "/dev/sd..." in your parted list.

Take this output for instance:

Disk geometry for /dev/sda: 0MB - 122942MB  
Disk label type: msdos  
Number  Start   End     Size    Type      File system  Flags  
1       0MB     1078MB  1077MB  primary   reiserfs     boot  
2       1078MB  2155MB  1078MB  primary   linux-swap  
3       2155MB  122935MB 120780MB extended  
5       2155MB  7452MB  5297MB  logical   reiserfs  

Say I wanted to chroot into the 3rd partition. To set this as my target partition I can take the letter from the device ("a" from /dev/sda) and the number of the partition from the column on the left (3) to type in "sda3"

Now onto the actual chroot. If you get an error such as `chroot: failed to run command ‘/bin/bash’: No such file or directory` this means one of two things:

A. You are using a different architecture on each system (like using an x64 chroot on an x32 system)  
B. You chose the wrong partition  

I will add a catch for both instances but for now this is a general rule.

You cannot use two different system architectures when chrooting. If you have a 64-bit system, only a 64-bit chroot will work. If you are using an arm64 system, you cannot use a regular 64-bit chroot. Cross-arch is impossible.

If you choose the wrong partition, don't worry about it. Just restart the script. It's not fun, but hey. So is bash.

That's it! If you have an issue drop it in the issues.

Be sure to give credit if you decide to use this script. I spent time on it so you don't have to.
