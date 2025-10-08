okay, follow these steps:

first, give `find` SUID bit. You give this by: `sudo chmod 4755 /usr/bin/find` OR `sudo chmod u+s /usr/bin/find`, check by `ls -l /usr/bin/find`. 
Second, run this `find . -exec /bin/sh -p \; -quit`
Third, you will see #, yeah, now you have root access.


We exploit binaries for this. Binaries usually have a SUID bit. SUID bit is given to files that do root level things. So when users access it, they don't get the 'oh this can't be performed by you! this is sudo stuff', it just goes 'hm, this is root, but you can get a pass... though, this is still a root.'

so we set `find` SUID.

Now, find has a -exec flag. This flag executes the command on each file found.

now, what we do is, we use this bit inside -exec: /bin/sh -p \;
This command just launches a damn shell. The p flag? It reflects the access of the SUID of the command that triggered this command- which is, yeah, find with SUID- so superuser access, boom, we open a shell with superuser access.

a few important notes:
1. `which find` to get the binary location
2. `find / -perm -u=s -type f 2>/dev/null` this searches the entire file system for permissions with SUID, which type as file, and if there are errors, send them to /dev/null to avoid clutter

