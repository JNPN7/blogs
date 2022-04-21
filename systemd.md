# Introduction
Systemd is service and daemons manager of linux. It's very important part of Linux. You need to understand about systemd, if you are using Linux as an operating system windows. Systemd provides functions like startup of services at boot time which will make our life easier (we don't need to startup services and daemons always we login to our system), enabling, disabling, stopping, restarting services and daemons. systemd is default init system for maximum Linux distros.

# File system for systemd
You can find systemd directory inside /etc/ and also inside /usr/lib/ . You may be wonder why there are two systemd, it was my first question. There is small difference between /etc/systemd and /usr/lib/systemd. /usr/lib/systemd contains systemd unit files which is saved by the package manager. When a software is installed then their service file is written inside /usr/lib/systemd. /etc/systemd is directory where the admin writes needed daemon and services. So when you need to add some services then you ought to keep it in /etc/systemd/system.

In systemd, a single servies is refered as an "unit". We call them systemd unit. We define those unit in a file called unit file. There are diffent kind of  unit files which can be distinguised by the extension of file such as:
1. .service => system servies
2. .device => device file recognized by kernel
3. .mount => mount file
4. .socket => inter process communication socket
5. .timer => systemd timer
5. .target => group of systemd units
and so on more on that later.

You can find systemd unit files inside directory /etc/systemd/system. 

![Screenshot from 2022-02-14 19-31-25.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1644846655730/HBbi42dWC.png)


# Controlling services
To start, stop, restart, reload services, you can use systemctl command.
### Start service
```
sudo systemctl start servicename.service
``` 
or
```
sudo systemctl start servicename
``` 
The systemctl will recognize all servicename so no need to add .service post-fix.

### Stop service
Similar to start, you just need to replace start by stop.
```
sudo systemctl stop servicename
``` 

### Restart service
```
sudo systemctl restart servicename
``` 

### Reload service
```
sudo systemctl reload servicename
``` 

### Status
To know the status of services i.e. is service running or not and other information about status.
```
sudo systemctl status servicename
``` 

## Enabling disabling services in boot
As I told before, one of the function of systemd is to startup service in boot. So to enable the service startup in boot you can use following command:
```
sudo systemctl enable servicename
``` 
Similary if you want remove service from start up you can disable it by following:
```
sudo systemctl disable servicename
``` 

## Listing all the units
If you forget the services you have, you can simply navigate to systemd/system and check all the services but there is a better way. You can just check all services form systemctl command:
```
systemctl list-units
``` 
For unit files:
```
systemctl list-unit-files
``` 
If you want only services then you can use option called type:
```
systemctl list-units --type=service
``` 
Similarly for active services only:
```
systemctl list-units --state=active
``` 

## Masking and unmasking units
If you want to mask unit i.e. prevent systemd unit from being started, automatically or manually you can use following command:
```
sudo systemctl mask servicename.service
``` 
And to unmask
```
sudo systemctl unmask servicename.service
``` 

# Conclusion
Systemd, service manager manages the service. Using systemctl you can control these systemd units. Now you are able to start, stop, enable, disable services.