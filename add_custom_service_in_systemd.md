# Introduction
Systemd is the service and daemon manager. I have explained about systemd in previous blog [systemd "the service manager"](https://juhelblog.hashnode.dev/systemd-the-service-manager). Now, after knowing about systemd, it's function you may be wondering can we add our custom made service or daemon. And yes we can add our custom made services similarly to how package manager adds services tho package manager automatically adds services for us.

# Adding service
For adding services you need to make a file .service inside the /etc/systemd/system. And that's it boom you added your custom service. Obviously, you need to edit .service file you added. That's pretty easy too. You need to know somethings. Let me explain.
Unit file i.e. services file looks like following:
```
[Unit]
Description=<description about service>
After=<unit files>
Requires=<unit files>
Wants=<unit files>
Conflicts=<unit files>
Documentation=<url>

[Service]
Type=<simple, forking, oneshot, notify, dbus>
ExecStart=<path to executable file>
ExecReload=<path to executable file>
ExecStop=<path to executable file>
User=<user>
Restart=<condition>

[Install]
WantedBy=multi-user.target
Alias=<alias>
```

### Unit section
In the unit section, we have some option which are
1. Description: Here we can add some description regarding the service which gets output while checking status.
2. After: It consists of list of units. The unit starts only after units specified here are active.
3. Requires: It consists of list of dependencies units. If any units listed here fails to start, the unit is not activated.
3. Wants: It consists of list of weak dependencies units. If any units listed here fails it doesn't affect the unit on activation but it's better the units listed are active
4. Conflicts: It is opposite to Requires i.e. any units listed here shouldn't be active

### Service section
In the service section, we have some option which are
1. Type: Here we specify the type of service. Simple, forking, oneshot, notify, dbus are types of service.
2. ExecStart: Here we specify the path of script which runs while starting.
3. ExecReload: Here we specify the path of script which runs while reloading.
4. ExecStop: Here we specify the path of script which runs while stopping.
5. User: Here we specify user who can start, stop, control this service.
6. Restart: Condition when to restart like in failure.

### Install section
In install section, we have following option:
1. WantedBy: Consists a list of units that weakly depend on the unit. Tells when to start service and create symlinks between targets and its dependent unit. When you don't know the which target to use, just use multi-user.target.
2. Alias: We specify the alias of the unit

# Demonstration
Now, for the demonstration, I have created a daemon that simply saves the date every 3 second.
```
#! /usr/bin/bash
while true 
do
	date >> /home/juhel/tmp/test;
	sleep 3;
done
```

Then, I have added the savedate.service file inside /etc/systemd/system.
```
[Unit]
Description=Save date in every three second
After=network.target

[Service]
Type=simple
ExecStart=/usr/bin/env bash /home/juhel/Documents/automation/savedate.sh
Restart=on-failure
User=juhel

[Install]
WantedBy=multi-user.target
```

Now, you just need to reload systemctl daemon which can be done by following command
And, that's it I have added my custom created daemon in systemd
To enable the service:
```
sudo systemctl daemon-reload
```

The work done by the service:

![Screenshot from 2022-02-15 16-23-06.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1644921549156/jgGIYS-Ds.png)

# Conclusion
Now, I assume you know how to add custom service to the systemd. This comes very handy for the system administrator. Also, you can implement in your desktop.