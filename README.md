systemd Helper Script for WSL2
----
[![ko-fi](https://www.ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/capuccino)

This is a script designed to allow you to use systemd in WSL2 by faking PID1 using namespaces - aka "the poor man's container".

The main motivation behind this is you can run systemctl or your usual systemd stuff in WSL2 - all without waiting for Microsoft to wait for the official integration
for custom inits (for now).


Why Another?
----

Most of the approaches done is more complicated to set up. This was created based on my frustration on the existing approaches:

* Current Existing Approach does not preserve PWD when walking to the namespace. the [Snaps guide](https://forum.snapcraft.io/t/running-snaps-on-wsl2-insiders-only-for-now/13033) is a example of this, while that guide was the basis of this project,
  I took the liberties to improve the script so it works seamlessly with WSL2.

* Almost zero dependency - All you need is daemonize, util-linux, nsenter and a sane POSIX-compatible shell. Approaches like [genie](https://github.com/arkane-systems/genie) requires you to install .NET Core just to do this
  which is rather - bloaty. You're just spawning a shared namespace, you don't need to write it in C#.


Installing
----

Simply download this script and add it on your /usr/bin or wherever you like. 

However, to make sure this script truly works, make sure you have the following dependencies:

* util-linux (comes standard in all linux distros)
* daemonize (its in every debian-based distro out there. If it doesn't exist in your repos, build from source here: https://github.com/bmc/daemonize)
* nsenter (comes standard in all linux distros)

If you have them all, congrats! You're ready to use this.


Usage
----

```
Usage: ./init-systemd -u (USER) -c (command)
This script spawns a namespace to be able to use systemd in a specified user.
This requires unshare (from util-linux) and daemonize (available on debian/ubuntu).
If -c is provided, the command will be executed in the namespace's context non-interactively.
````

Contrbuting
---

There's more laywork to be done so it will be desirable for everyone, but in my own current usage, I say its ready for my own intended needs.

If you think you can make this script better please send patches via PR, or open some issues so I'm aware of the outstanding problems.

The entire script is written to be POSIX as possible. Bash-specific syntax should be prevented **at all costs**.


If you want to support me financially, my [Ko-fi](https://ko-fi.com/capuccino) is available for you to donate to.

Copyright
---

This script is Copyright 2020 &copy; Ayane "Capuccino" Satomi. Licensed under MIT.

This is inspired of this [article](https://forum.snapcraft.io/t/running-snaps-on-wsl2-insiders-only-for-now/13033) from Snapcraft.io.
