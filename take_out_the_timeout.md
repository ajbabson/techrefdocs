# Introduction
Over aggressive TMOUT settings can be real productivity killers.  Using `tmux` or `screen` can help, and there are other solutions that simulate user input,
but getting those to work consistently can be time consuming and inconsistent.  I recently discovered a new method that has been rock solid up to this point
at keeping me logged in to servers I need to stay logged into to do my work.  Disconnections create breaks in productivity at best and data/work loss at worst.

## How is TMOUT set?
When sys admins want to enforce a TMOUT setting, they generally do it in the system's system wide profile.  Check `/etc/profile` or a shell script in `/etc/profile.d/` for something like this:
```
TMOUT=900
readonly TMOUT
export TMOUT
```
This sets the TMOUT to a paltry 15 minutes for users and makes it read-only so users cannot change it.

## SSH Config
In many environments, a bastion server must be first connected to.  If you need to do this, then you should add entries like these to your `~/.ssh/config` file.
```
# ABC site
Host bastion.abc
 Hostname bastion.abc.example.com
 StrictHostKeyChecking accept-new

Host server01.abc
 Hostname server01.abc.example.com
 ProxyJump bastion.abc
 StrictHostKeyChecking accept-new

# XYZ site
Host bastion.xyz
 Hostname bastion.xyz.example.com
 StrictHostKeyChecking accept-new

Host server01.xyz
 Hostname server01.xyz.example.com
 ProxyJump bastion.xyz
 StrictHostKeyChecking accept-new
```
And so on...

Also, there is sometimes confusion around "Host" and "Hostname" in SSH config files, so I'll try to clear that up here.  The "Host" is just a sort of shorthand alias so you don't have to type
the FQDN each time you SSH to a host.  For example, with the following entry, I can type `ssh foo` and my SSH client will know that I actually want to SSH to `webserver01.example.com` even
though "foo" isn't in the real hostname at all.
```
Host foo
 Hostname webserver01.example.com
```
In your bash aliases and functions you can just put the name you specify as "Host" which helps keep them shorter.  The name that follows "Hostname" is the one that needs to resolve.

## Interlude - SSH Keys

I have also worked in environments where SSH keys can change frequently due to round robin DNS and the sys admins explicitly disallow StrictHostKeyChecking set to 'no'.  This seems pointless
to me in an environment where the keys assocated with a host can change as part of the DNS design.  It's especially pointless when you allow `StrictHostKeyChecking accept-new`, because now all I
have to do is delete a host's SSH keys from `known_hosts` every time I connect to it and then automatically accept the "new" one that is presented.  This is why I have added this directive to my
SSH config.

## Sending the TMOUT to Take a Timeout

I use this function in my `.bashrc`.  It uses the positional parameter so that I can pass the data center location as an argument and saves me a little typing.

`function tssh {ssh -t server01.$1 "bash --noprofile"; }`

Now all I have to do is type:

`tssh abc`

The function will expand this argument to `ssh -t server01.abc "bash --noprofile"`  SSH will then search my SSH config file for `server01.abc` and will find the `Host` entry that matches the
FQDN.  It will also tell it to connect (proxy jump) through `bastion.abc` which it then also looks up in my SSH Config to find the FQDN and other directives for connecting.

After forwarding through the ProxyJump host, the SSH client process will pass the "bash --noprofile" command to the SSH server to be executed as part of the login process.  This prevents the
system wide profile from being read.  Put the following line in either your `~/.bashrc` or `~/.bash_profile` and your custom TMOUT will be set.

`export TMOUT=28800`

You can also just unset it with `unset TMOUT`, but I favor a reasoned approach where the value allows me to do my work over the course of a business day without getting logged out, while at the
same time not totally violating the intention original set by the sys admins.  Having huge numbers of users logged in for indefinite amounts of time is just as bad practiced as setting a TMOUT
that's too short for users to be able to work reasonably without unnecessary interruptions.

## Back to SSH Keys

If you are working in an environment where SSH keys change often as a normal part of the design (this is actually not good practice because it defeats the purpose, but it happens), then you might
want to modify your function to this:

`function tssh { ssh-keygen -f "$HOME/.ssh/known_hosts" -R "bastion.$1.example.com"; ssh -t server01.$1 "bash --noprofile"; }`

This will remove the SSH key for the bastion server from your `known_hosts` file before you connect.  With `StrictHostKeyChecking accept-new` set, this is transparent to you when you connect,
besides a small additional delay as the new key is accepted and saved.  But don't do this if you don't have to.  SSH key checking is there for a reason.


