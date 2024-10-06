---
tags:
  - linux
publish_folder: Linux
---

- basic file permissions
- setuid and setguid
- sticky bits
- umask
- file attributes


#### File permissions

Every file has three types of ownership (owner, group, and other/world) and three basic permission modes : read, write, executable.

`chown` is used to update the ownership
`chmod` is used to update the permissions

#### setuid and setguid

`setuid` was designed to solve a very basic problem : user not having enough permissions to run certain programs. Adding the `setuid` flag allows the run the program with the owner's permissions, not the user executing it. 

`setguid` is the same concept but applied to groups.

#### sticky bits

When the sticky bit is set on a directory, it restricts the deletion or renaming of files within that directory to the file's owner, the directory's owner, or the superuser (root). 
Other users, even if they have write permissions to the directory, cannot delete or rename files that they do not own.

- **Shared directories**: In shared directories where multiple users have write permissions, setting the sticky bit ensures that users can only delete or rename their own files. This prevents accidental or malicious deletion of other users' files.
- **Temporary directories**: Sticky bits are often used on temporary directories, such as `/tmp`, to prevent users from deleting or modifying files created by other users. This helps maintain the integrity of temporary files and ensures that they are not accidentally removed while still in use.


#### umask

`umask` is a command and a concept in Unix and Unix-like operating systems, including Linux. It stands for "user file creation mask" and determines the default file permissions for newly created files and directories.

The umask value is typically set in the user's shell configuration files (e.g., ~/.bashrc, ~/.profile) to ensure that it applies consistently to new shell sessions.

```bash
# see current value
umask
# set a new value
umask 022
# umask 077 ensures that files are created with permissions that only allow the owner full access, with no access granted to the group or others
umask 077
```

#### File attributes


**Attributes**

Apart from the file mode bits that control user and group read, write and execute permissions, several file systems support file attributes that enable further customization of allowable file operations. 

The `e2fsprogs` package contains the programs `lsattr`(1) and `chattr`(1) that list and change a file's attributes, respectively. 

    a - append only: File can only be opened for appending.
    c - compressed: Enable filesystem-level compression for the file.
    i - immutable: Cannot be modified, deleted, renamed, linked to. Can only be set by root.
    j - data journaling: Use the journal for file data writes as well as metadata.
    m - no compression: Disable filesystem-level compression for the file.
    A - no atime update: The file's atime will not be modified.
    C - no copy on write: Disable copy-on-write, for filesystems that support it.


**Extended attributes**

Extended attributes are name:value pairs associated permanently with files and directories.
Extended attributes are also used to set Capabilities. 

By default, extended attributes are not preserved by `cp`, `rsync`, and other similar programs.




# Annexes

https://wiki.archlinux.org/title/File_permissions_and_attributes

#quartz 