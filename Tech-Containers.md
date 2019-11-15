## Jamie's Rules for Container Usage

* If it interacts with kernelspace, such as NFS or VPN, use a virtual machine.
* If it's multiple processes or a daemon, use a virtual machine or an [LXD container](https://linuxcontainers.org/lxd/) (as an LXD container starts a init system)
* If it's a single userspace-only process which YOU write the commandline arguments for, then consider containers

----

I have not had good experience with container technologies such as [Docker](https://www.docker.com/).

Definitely [Linux kernel namespaces](https://lwn.net/Articles/531114/) have their usage, but so far, the management tools which bring these together into an execution environment have left me disappointed and frustrated (to put it politely).

So I formulated this set of rules to help prevent my own future frustration.

It turns out pretty much everything I want to do is in 1 and 2, which explains my dissatisfaction.