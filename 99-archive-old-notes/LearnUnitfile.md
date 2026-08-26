# Day 01 :Services on linux help to configure software to run in background make sure that they run all the time automatically when servers are rebooted as they follow the right order of startup

ex: docker,db,appache server etc 

> systemctl start httpd

# A systemd file usually refers to a systemd unit file.
These files are used by systemd, the init system and service manager on most modern Linux distributions (like Ubuntu, CentOS, RHEL, Fedora, Debian).

# 🔹 What is a systemd unit file?

A configuration file that tells systemd how to manage a resource.

Resource can be a service, mount point, timer, device, or target.

The most common type is a service unit file (.service).

# 🔹 Location of systemd files

System-wide (default services): /lib/systemd/system/ or /usr/lib/systemd/system/

User/system overrides: /etc/systemd/system/

User-specific services: ~/.config/systemd/user/

once system file is configured relaod the command by systemctl daemon-reload

# Day 02 

configure the basic python log file as a service and executed and configured the unit file [unit][services][install] - Ensures service starts at boot in multi-user mode

sudo systemctl daemon-reload 

# Why sudo systemctl daemon-reload is Needed

When you create or modify a new service file (like /etc/systemd/system/myservice.service), systemd (the init system) doesn’t know about your changes yet.

daemon-reload tells systemd:
“Hey, I added/edited a unit file, please reload your configuration files and update your database of services.”
