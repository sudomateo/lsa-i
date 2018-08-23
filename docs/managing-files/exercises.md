# Exercises

1. Create a directory for these exercises by using the command `mkdir /tmp/managing-files`.
2. Change into the newly created directory using the command `cd /tmp/managing-files`.
3. Create six empty files using the command `touch file{01..06}`.
4. Run each of the following commands to change the permissions of each file. See if you can guess what the permissions will be before you run each command:
    1. `chmod 764 file01`
    2. `chmod 400 file02`
    3. `chmod 651 file03`
    4. `chmod 4744 file04`
    5. `chmod 4664 file06`
    6. `chmod 1444 file06`
5. Run the command `ls -l`. You should see output similar to the following.
```
$ ls -l
total 0
-rwxrw-r--. 1 vagrant vagrant 0 Aug 23 01:10 file01
-r--------. 1 vagrant vagrant 0 Aug 23 01:10 file02
-rw-r-x--x. 1 vagrant vagrant 0 Aug 23 01:10 file03
-rwsr--r--. 1 vagrant vagrant 0 Aug 23 01:10 file04
-rw-rw-r--. 1 vagrant vagrant 0 Aug 23 01:10 file05
-r--r--r-T. 1 vagrant vagrant 0 Aug 23 01:10 file06
```
6. Run the commmand `tar -zcvf /tmp/managing-files.tgz -C /tmp/managing-files .` to create an archive named `/tmp/managing-files.tgz` of all the files in the `/tmp/managing-files` directory.
7. Run the command `rm -f file0*` to remove all six files that were created earlier. Verify the files were removed using the command `ls -l`.
8. Run the command `tar -zxvf /tmp/managing-files.tgz -C /tmp/managing-files` to extract the contents of your archive back into the `/tmp/managing-files` directory.
9. Verify the files were restored correctly using the command `ls -l`. You should see output similar to the following. **NOTE: `tar` does not restore special permissions (SUID, SGID, sticky bit) so you will only see the read, write, and execute permissions.**
```
$ ls -l
total 0
-rwxrw-r--. 1 vagrant vagrant 0 Aug 23 01:10 file01
-r--------. 1 vagrant vagrant 0 Aug 23 01:10 file02
-rw-r-x--x. 1 vagrant vagrant 0 Aug 23 01:10 file03
-rwxr--r--. 1 vagrant vagrant 0 Aug 23 01:10 file04
-rw-rw-r--. 1 vagrant vagrant 0 Aug 23 01:10 file05
-r--r--r--. 1 vagrant vagrant 0 Aug 23 01:10 file06
```
10.  Practice these and other commands until you feel comfortable with them.
11.  When finished, use the `exit` command to exit the shell and logout.

