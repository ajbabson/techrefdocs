
# Linux: Commands and Configuration

This is a collection of various useful Linux things for reference.

#### Get current
Don't just upgrade your packages, upgrade your release.<br>
`sudo do-release-upgrade`

#### Fix your prompt
This document explains just about all you need to know.<br>
[Bash prompt how-to](https://tldp.org/HOWTO/Bash-Prompt-HOWTO/x329.html)

#### Enjoy the silence (turn off that annoying bell!)
By all means, always uncomment this line in `/etc/inputrc`:<br>
`set bell-style none`

and add this to  your `.vimrc`:<br>
`set visualbell`

while you've got your `.vimrc` open, might as well add:
```
syntax enable
set nohls
set background=dark
"convert tabs to four spaces
set tabstop=8 softtabstop=0 expandtab shiftwidth=4 smarttab
```

#### Know your terminal
```
tty
stty
stty -a
```
If it's too cluttered<br>
`clear` or `Ctrl-L`<br>
and if it misbehaves and gets all wonky:<br>
`reset`<br>

Set your terminal history.
```
grep saveLines /etc/X11/app-defaults/XTerm
*saveLines: 1024
```

#### Get to know your CPU
```
cat /etc/cpuinfo
lscpu
```

#### Know your hardware
`sudo lshw`<br>

#### Know your hardware with less work
```
inxi -D
inxi -G
inxi -F
```

#### Find the serial number of a system and whether it's a VM or physical.
```
dmidecode -t system | grep Serial
dmidecode -s system-manufacturer
```
#### What's on the bus, Gus?
```
busctl
```

#### Set some limits on users
```
man pam_limits
vim /etc/security/limits.conf
ulimit -a
```

#### Set limits on things you run to keep them from breaking things
```
man prlimit
```

#### Control your keyboard, pointer, and monitor
Show current settings:<br>
`xset q`<br>
Disable autorepeat on your keyboard:<br>
`xset r off`

#### APT stuff
Which repos do you trust?<br>
`apt-key list`<br>

Looking for something in a package but don't know which?<br>
`apt-cache search <keyword>`<br>

Package info:<br>
`apt-cache show <package>`

What are a package's reverse dependencies?<br>
```
apt-cache rdepends <package>
<package>
Reverse Depends:
  <package-that-needs-me>
```

What other packages are installed as part of this package?<br>
```
apt depends <package>
<package>
  Depends: <package1>
  Depends: <package2>
  Depends: <package...>
```

#### Know your kernel
`uname -r`<br>
`uname -a`

#### Know your release
`cat /etc/os-release`<br>
`lsb_release -a`

#### Know what your kernel is up to
`dmesg`<br>
and<br>
`tail -f /var/log/dmesg`

#### Dynamic motd
Files live here<br>
`/etc/update-mot.d/`<br>
For more info<br>
`man update-motd`

#### Informational motd
`screenfetch`

#### Setting root's editor
change this symlink to point to your editor of choice when using visudo<br>
```
file /etc/alternatives/editor
/etc/alternatives/editor: symbolic link to /usr/bin/vim
```

#### Autostart
If you find things starting on boot that you would rather not, look in these directories:<br>
```
~/.config/autostart/
/etc/xdg/autostart/
```

#### System V services
Distributions that use System V use the `service` command.<br>
```
service --status-all
service ssh status
service ssh start
service ssh stop
service ssh restart
```

#### Systemd services
Some systemd distributions support the `service` command, but you should use `systemctl` instead.<br>
```
systemctl list-unit-files --type=service
systemctl -a
sudo systemctl enable ssh
sudo systemctl disable ssh
sudo systemctl start ssh
sudo systemctl stop ssh
sudo systemctl restart ssh
```

#### Status of services
See `systemctl` man page for explanations.<br>
```
$ sudo systemctl is-enabled virtlogd
indirect
$ sudo systemctl is-enabled whoopsie
enabled
$ sudo systemctl is-enabled saned
masked
```

#### List installed packages
Ubuntu
```
dpkg --list
```
CentOS
```
sudo yum list installed
```

#### Search installed packages for filename
This will tell you which package the file came from.<br>
Ubuntu
```
dpkg-query -S <filename>
```
CentOS
```
rpm -qf <filename>
````

#### List all files from a package
Ubuntu
```
dpkg -L
```
CentOS
```
rpm -ql <package>
```

#### Verify the integrity of a package
```
dpkg -V <package>
```
#### Learn about time
`ntpq -p`

#### Change your MAC address
```
ifconfig <intf> ether d4:33:a3:ed:f2:12
```

#### Check your visitor logs
Shows all logins since file was created (by default it gets logrotate'd)
```
last
```
Shows all **failed** login attempts
```
lastb
```
#### Know your disk use<br>
`du -s -h -x <dir>`<br>

Show disk use for top 20 directories ordered by size<br>
`du -s * | sort -rn | head -20`

#### Know your processes
```
ps -A
ps -A -o pid,pcpu,rss,args
pstree
```
#### Get to know procfs<br>
`man procfs`<br>

Show all the values stored in `/proc/sys/`.<br>
`sysctl -a`

Show values that include the icmp token.<br>
`sysctl -ar icmp`

Turn on IP forwarding. (not persistent)<br>
`sudo sysctl net.ipv4.ip_forward=1`<br>

Makes changes persistent by adding them to:<br>
`/etc/sysctl.conf`

Tell the kernel to reread changes made to `/etc/sysctl.conf`.<br>
`sysctl -p`

/bin/ls*

#### Where do syscalls live?
```
/usr/include/asm-generic/unistd.h
/usr/src/linux-headers-$(uname -r)/include/uapi/asm-generic/unistd.h
```

#### What's the kernel logging?
`journalctl -t kernel`<br>
`journalctl -t kernel -f`

#### Know which files are in use
```
# by a process
lsof -p <pid>`
# by your current shell
`lsof -p $$`
# or you can use
fuser
# What's using your home directory?
fuser -c ~
# kills all processes accessing the file system /home in any way.
fuser -km /home
# shows all processes at the (local) TELNET port
fuser telnet/tcp           
```

#### kill background job 2
`kill %2`

#### kernel modules
```
man modules.dep
lsmod
depmod
modinfo
```

#### use modprobe, not insmod and rmmod
`modprobe`

#### find files and do something with them
```
find . -iname "*.vbs" -exec /bin/mv '{}' /var/dodgy/ \;
find . -name .DSstore -delete
```

#### find files
```
# anywhere on the system that are not owned by any user
find / -nouser -ls
find
 -newer <thanfile>
 -maxdepth -<n> (directories)
 -mtime
 -type d -exec chmod o+x {} \;
```
 
#### use a null character separator when filenames have spaces
```
aric@sasquatch:~$ find . -maxdepth 1 -name "*.txt"
./a.txt
./my file.txt
./foo.txt
./b.txt
 ```
By default, a space is a separator, so "my" and "file.txt" get piped to xargs.
```
aric@sasquatch:~$ find . -maxdepth 1 -name "*.txt" | xargs grep "foo"
grep: ./my: No such file or directory
grep: file.txt: No such file or directory
```
Use the print0 option to separate matched files with a null character and then tell xargs that input items are separated by a null character.
```
aric@sasquatch:~$ find . -maxdepth 1 -name "*.txt" -print0 | xargs -0 grep foo
./my file.txt:foobar
aric@sasquatch:~$ 
```

#### Name Service Switch (NSS)
`man nsswitch.conf`

#### Systemd-analyze
```
$ systemd-analyze 
Startup finished in 6.398s (firmware) + 4.326s (loader) + 7.425s (kernel) + 23.308s (userspace) = 41.457s
$ systemd-analyze critical-chain
$ systemd-analyze blame
$ systemd-analyze plot
```

#### Network socket statistics
````
ss -latn
ss -latr
ss -tiepm
ls /proc/sys/net/ipv4/
ls /proc/sys/net/ipv6/
````

#### Get link statistics (including errors)
```
ip -s link
```
 
#### Get network statistics
```
nstat -s
nicstat 1
```

#### Ethtool
```
# statistics
ethtool -S eth0
# driver info
ethtool -i eth0
# interface tunables
ethtool -k eth0
```

#### Use SAR
```
sar
  -n DEV: Network interface statistics
  -n EDEV: Network interface errors
  -n IP,IP6: IPv4 and IPv6 datagram statistics
  -n EIP,EIP6: IPv4 and IPv6 error statistics
  -n ICMP,ICMP6: ICMP IPv4 and IPv6 statistics
  -n EICMP,EICMP6: ICMP IPv4 and IPv6 error statistics
  -n TCP: TCP statistics
  -n ETCP: TCP error statistics
  -n SOCK,SOCK6: IPv4 and IPv6 socket usage
sar -n SOCK,TCP,ETCP,DEV 1
```

#### Unicode
Use `Ctrl-Shift-U` then enter the unicode code, and press the spacebar.<br>
Find everything you could want [here](https://unicode.org/charts/).<br>
`20ac` = €<br>
`00a5` = ¥<br>
