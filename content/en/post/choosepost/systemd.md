---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Systemd"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2022-06-04T14:02:06+03:00
lastmod: 2022-06-04T14:02:06+03:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---
# systemd


Systemd is a set of basic building blocks for a Linux system. He
provides a system and service manager that runs as PID 1 and
starts the rest of the system. Systemd provides: \* Aggressive
parallelization possibilities

- Uses socket activation and D-Bus to start services.

- Offers to start daemons on demand, monitors processes with
    Linux control groups.

- Supports snapshots and system state restore

- Supports mount points and automounts

- Implements complex service management logic based on
    transactional dependencies.

systemd provides a system of dependencies between various
entities called "units" (modules/tasks) that systemd
can manage. Modules encapsulate various objects needed for
system loading and maintenance. Most units are configured in
unit configuration files, syntax and basic set of parameters
which are described in systemd.unit(5) , however some are created
automatically from other configuration files, dynamically from
system state or programmatically at run time. Devices can
be "active" (meaning running, connected, connected, ...,
depending on the type of device, see below) or “inactive” (which
means stopped, unlinked, disconnected, ...) and also in
the process of activation or deactivation, i.e. between two states (these
states are called "activation", "deactivation"). Also available
a special "failed" state, which is very similar to "inactive" and
is entered when the service somehow failed (the process returned a code
exit errors or failed, operation timed out
or after too many restarts). ). If this
state entered, the reason will be logged for further
use. The following types of units are available:

- service - Service in the system, including start instructions,
    restart and stop the service.

- socket - The network socket associated with the service.

- device - A device specifically managed by systemd.

- mount - Mount point managed by systemd.

- automount - The mount point is automatically mounted when
    loading.

- swap - Swap in the system.

- target - Synchronization point for other units. Commonly used
    to start enabled services on boot.

- path - Path to activate based on path. For example, you can
    start services based on the state of a particular path, e.g.
    whether it exists or not.

- timer - Timer for scheduling the activation of another device.

- snapshot - A "snapshot" of the current state of systemd. Usually
    used to rollback after making temporary changes to systemd

- slice - Resource limitation via Linux Control Group nodes
    (cgroups).

- scope - Information from systemd bus interfaces. Commonly used
    to manage external system processes.

- And here is the location of systemd modules files (Screenshot 1)

![Screenshot_1](/Screenshots/Screenshot_1.png) ( Screenshot 1 )

# A little about the structure of Units

![Screenshot_2](/Screenshots/Screenshot_2.png) ( Screenshot 2 )

In screenshot 1, we can observe some structure of the nginx unit file:

1. \[Unit\] --- This usually describes the metadata of the service and its
    interaction with other services.

- Description --- a brief description of the daemon

- Documentation --- man page, which describes how to work with the service, in
    In this case, Nginx

- After --- Literally means "After". The field indicates after which
    daemons or events, this unit will be started. In our example,
    the Nginx unit will be started after the network
    interfaces.

2. \[Service\] --- Describes the configuration. Applies only to
    service units.

Type --- An important parameter. Describes how the daemon will be started.
In our version, this is forking, but you may encounter others:

- forking --- after starting, the daemon forks (fork), completing
    parent process;

- simple --- at startup, the daemon goes into standby mode, in its
    original form;

- one-shot --- one-time execution. This type is used for
    scripts that should run and finish after
    execution.

- PIDFile --- points to the main process that monitors
    systemd

- ExecStartPre --- main path and arguments to be
    command started BEFORE starting the main process

- ExecStart --- main path and arguments to be launched with
    Nginx

- ExecReload --- specifies the command to restart the service

- ExecStop --- command to stop the service

- TimeoutStopSec --- Indicates that the system will wait 5 seconds
    stopping a service before forcibly stopping it

3. \[Install\] --- describes the behavior of the unit.

- WantedBy --- describes exactly how the device will be turned on.
    multi-user.target means that on startup, in a directory
    /etc/systemd/system directory multi-user.target.wants will be created, in
    which will create a symbolic link to the service. This is the parameter
    dependencies with the current block, when you stop the service this link
    will be deleted.

# systemctl


You can perform various management tasks to manage services
systemd using the `systemctl` command. Below is a set of examples
commands demonstrating how to use systemctl to control
systemd services ( Screenshots 3 - 4 ).

![Screenshot_3](/Screenshots/Screenshot_3.png) ( Screenshot 3 )

![Screenshot_4](/Screenshots/Screenshot_4.png) ( Screenshot 4 )

For a complete list of options for the `systemctl` command, see
using the `man systemctl` command.

# Other systemd commands from the system \*ctl

Along with the main systemctl tool for managing target and
service units systemd provides a bunch of other useful utilities:

1. The `timedatecl` command. This command provides a user-friendly interface
    to change the date and time zone information for the system.
2. Command `hostnamectl`. This command allows us to permanently change
    hostname of the system without having to edit any files.
3. The `localectl` command. Allows you to change the system locale settings.
4. The `loginctl` command. `loginctl` can be used for introspection
    and state management systemd login manager
    systemd-logind.service.
5. The `journalctl` command. Used to query the contents of the journal
    systemd(1).

# Sources


1.  <https://freehost.com.ua/faq/articles/ispolzovanie-systemd/>
2.  <https://mirivlad.ru/vvedenie-v-systemd/>
3.  <https://man7.org/linux/man-pages/man1/systemctl.1.html>
4.  <https://docs.fedoraproject.org/en-US/packaging-guidelines/Systemd/#definitions>
5.  <https://man7.org/linux/man-pages/man1/systemd.1.html>
6.  <https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system_administrators_guide/chap-managing_services_with_systemd>
7.  <https://docs.fedoraproject.org/en-US/quick-docs/understanding-and-administering-systemd/>