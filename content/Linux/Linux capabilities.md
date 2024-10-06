---
publish_folder: Linux
tags:
  - linux
---

Linux capabilities **provide a subset of the available root privileges** to a process. This effectively breaks up root privileges into smaller and distinctive units. Each of these units can then be independently be granted to processes.


```bash
# print capabilities
capsh --print

# examine a file's capabilities
getcap /usr/bin/ping
getcap `which ping`
```




https://man7.org/linux/man-pages/man7/capabilities.7.html
https://book.hacktricks.xyz/linux-hardening/privilege-escalation/linux-capabilities



#linux/capabilities
#quartz 