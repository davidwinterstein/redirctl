# REDIRCTL

**[redir](https://github.com/troglobit/redir)** is a tcp connection redirection software that is ahead of **[rinetd](https://github.com/samhocevar/rinetd)** regarding the maximum number of concurrently redirectable connections.  
This becomes relevant when you need to move a lot of similarly configured servers to new IP addresses, for instance.  
Sadly there is no service available for this, so I wrote this simple wrapper script. To use it, simply copy the relevant files to the locations described below.  


---


You can basically keep the folder structure from this repository.  

The wrapper script should be located here:  
`/usr/sbin/redirctl`  
Use it like this:
**[`redirctl`](usr/sbin/redirctl) `<status|start|stop|restart>`**

Config files for the wrapper script should be located here:  
`/etc/redir/ctl.cfg`  
`/etc/redir/ips.cfg`  
`/etc/redir/ports.cfg`  
`/etc/redir/special.cfg`  

By default, for every IP defined in [`ips.cfg`](etc/redir/ips.cfg) a redir process for every port in [`ports.cfg`](etc/redir/ports.cfg) is spawned.  
Additionaly a process for every IP and port quadruplet in [`special.cfg`](etc/redir/special.cfg) is spawned.

Log files are located at:  
`/var/log/redir/redirctl.log`  
`/var/log/redir/redir_output.log`

They are configured in [`ctl.cfg`](etc/redir/ctl.cfg). You don't need to create them manually.


If you want to make this a `systemd` service, you can do so by copying the [`redirctl.service`](etc/systemd/multi-user.target.wants/redirctl.service) file to `/etc/systemd/multi-user.target.wants/redirctl.service` and then running
```sh
systemctl start redirctl.service
systemctl enable redirctl.service
```


**Remember to configure and bring up the network interface for the IP address(es) to be forwarded first.  
Obviously the ports that should be forwarded may not be listened on by any other service.  
Also you need the redir binary, of course.**
