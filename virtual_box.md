
## Virtual Box Tips

### 9.8.6. Using the Host's Resolver as a DNS Proxy in NAT Mode

When connecting my laptop to a VPN, my VM could no longer resolve until I restarted `systemd-resolved`.  This fixed that.
https://www.virtualbox.org/manual/ch09.html#nat_host_resolver_proxy

```
9.8.6. Using the Host's Resolver as a DNS Proxy in NAT Mode

For resolving network names, the DHCP server of the NAT engine offers a list of registered DNS servers of the host. If for some reason you need to hide this DNS server list and use the host's resolver settings, thereby forcing the Oracle VM VirtualBox NAT engine to intercept DNS requests and forward them to host's resolver, use the following command:

$ VBoxManage modifyvm VM-name --natdnshostresolver1 on

Note that this setting is similar to the DNS proxy mode, however whereas the proxy mode just forwards DNS requests to the appropriate servers, the resolver mode will interpret the DNS requests and use the host's DNS API to query the information and return it to the guest. 
```
