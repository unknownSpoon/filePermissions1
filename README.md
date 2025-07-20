# filePermissions1

. ls -l Permission Output

Example:

drwxr-x--- 2 user group 4096 Feb 18 03:27 logs
-rw-r--r-- 1 user group 4578 Oct 30 11:37 log.txt

    1st column (10 chars): permissions

    Then: link count, owner, group, size, timestamp, name

4. Permission String Breakdown

    1st char: file type

        - file, d dir, l symlink, b block, c char dev, s socket, p pipe

    Next 9 chars: 3 groups (user, group, other)

        r read, w write, x execute

5. Directory Permissions

    r: list files

    w: create/delete/rename/modify files

    x: enter directory & access contents

    Directories need x to be usable

6. Numeric Permissions

Each permission has a value: r=4, w=2, x=1

    rw-r--r-- = 644

    rwx------ = 700

    rwxrw-r-- = 764

    rwxrwxrwx = 777

7. Permission Examples

    -rw-r--r--: User can read/write, others read only

    drwx------: Dir only usable by user

    -rwxr-----: User full access, group read, others none

8. Special Permissions: SUID, GUID, Sticky Bit

    SUID (chmod u+s): Run as file owner

    GUID (chmod g+s): Run as file group

    Sticky Bit (chmod +t on dirs): Only owner/root can delete

    Example: /usr/bin/passwd runs as root

9. Sticky Bit (More Detail)

    Only applies to directories

    Group bit: files inherit directory's group

    Other bit: restrict delete to file owner or root

10. chmod – Change Mode

    chmod 777 file: all perms to everyone

    chmod ugo+rwx folder: add full perms to all

    chmod +r,u+wx file: add read to all, write/exec to user

11. chown – Change Owner

    chown user file: change owner

    chown user:group folder: change owner & group

    chown :group folder: change group only

    chown user:: change owner, keep primary group

12. Default Permissions

    Vary by distro

    Debian:

        Files: rw-r--r--

        Folders: rwxr-xr-x

    Can be modified with umask

13. umask – Set Default Subtracted Permissions

    Default permissions (e.g., rw-rw-rw-) – umask removes bits

    Example:

        To remove write from others: umask 002

        Result: rw-rw-r--

14. umask Usage

    umask: display current

    umask 022: removes write from group/others

    umask 077: only owner has full perms

15. Setting umask Persistently

    Per user: add to ~/.bashrc

    Globally:

        /etc/profile (login shells)

        /etc/bash.bashrc (interactive shells)

        /etc/profile.d/set-umask.sh (custom scripts)

        /etc/pam.d/common-session using pam_umask
