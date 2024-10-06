---
tags:
  - linux
publish_folder: Linux
---

# Introduction 

Namespaces are a feature of the Linux kernel that partitions kernel resources such that one set of processes sees one set of resources while another set of processes sees a different set of resources.

Namespace kinds : 

- Mount (mnt)
- Process ID (pid)
	- provides processes with an independent set of process IDs
	- PID namespaces are nested
- Network (net)
- Interprocess communication (ipc)
- UTS (uts)
- User ID (user)
- Control group (cgroup)
- Time (time)



# Manipulating namespaces

```bash

# List existing namespaces
lsns

# Run program with some namespaces unshared from parent 
# We could say it creates a new namespace
# - uts namespace
unshare --uts
# - pid namespace
unshare --pid --fork --mount-proc

# Get into a process namespace
nsenter -a -t <pid>



```






# Network namespaces

Usually, an installation of Linux shares a single set of network interfaces and routing table entries shared across the entire OS.

With network namespaces, you can have different and separate instances of network interfaces and routing tables that operate independent of each other.


	# create a new namespace
	ip netns add <namespace_name>
	ip netns list
	






# References

* https://man7.org/linux/man-pages/man7/namespaces.7.html
* https://linuxembedded.fr/2020/11/namespaces-la-brique-de-base-des-conteneurs
* https://lwn.net/Articles/531114/



#veille/linux 
#quartz 