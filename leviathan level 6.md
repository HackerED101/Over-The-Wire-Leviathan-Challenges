# OverTheWire - Leviathan Level 6 Setup Guide

This guide explains how to complete **Leviathan Level 6** and retrieve the password for **Level 7**.

## Prerequisites

Before you begin, ensure you have the following:

1. **An active internet connection**.
2. **SSH client** installed (typically available on most Linux distributions and macOS by default).
3. **sshpass** installed (for automating SSH logins with a password).
   - To install `sshpass` on Kali Linux, use the following:
     ```bash
     sudo apt-get install sshpass
     ```
   - On macOS, use `brew`:
     ```bash
     brew install sshpass
     ```

## Steps to Connect to Leviathan Level 6

1. **Open a terminal**: If you're on Linux or macOS, open a terminal window. On Windows, you may need an SSH client like `PuTTY` or use the Windows Subsystem for Linux (WSL).

2. **Use `sshpass` to log in**: The username for **Level 6** is `leviathan6`, and the password is the one you retrieved from **Level 5**. Use the following command to log in via SSH:

    ```bash
    sshpass -p <password_from_level_5> ssh leviathan6@leviathan.labs.overthewire.org -p 2223
    ```

   Replace `<password_from_level_5>` with the password you found in Level 5.

3. **Confirm the host authenticity**: When connecting for the first time, you might see the following prompt:
   
    ```text
    The authenticity of host '[leviathan.labs.overthewire.org]:2223 ([13.48.119.24]:2223)' can't be established.
    ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.
    Are you sure you want to continue connecting (yes/no/[fingerprint])?
    ```

   Type `yes` to continue and add the host to the list of known hosts.

4. **Enter the password**: After entering the `sshpass` command, you should be logged in to the server. If you're not using `sshpass`, the server will prompt you for the password you retrieved from Level 5.

5. **You're in!**: Once logged in, you should see a welcome message and the prompt for the `leviathan6` user:
   
    ```bash
    leviathan6@gibson:~$
    ```

6. **Check who you are**: To verify your current user, run the following command:
   
    ```bash
    whoami
    ```

## Initial Directory Listing

```sh
leviathan6@melinda:~$ ls -la
total 28
drwxr-xr-x   2 root       root       4096 Nov 14  2014 .
drwxr-xr-x 172 root       root       4096 Jul 10 14:12 ..
-rw-r--r--   1 root       root        220 Apr  9  2014 .bash_logout
-rw-r--r--   1 root       root       3637 Apr  9  2014 .bashrc
-rw-r--r--   1 root       root        675 Apr  9  2014 .profile
-r-sr-x---   1 leviathan7 leviathan6 7484 Nov 14  2014 leviathan6
```

## Running the Executable

```sh
leviathan6@melinda:~$ ./leviathan6
usage: ./leviathan6 <4 digit code>
```

## Writing a Brute Force Script

```sh
leviathan6@melinda:~$ mkdir /tmp/jhalon
leviathan6@melinda:~$ nano /tmp/jhalon/brute.sh
```
Our shell script will look something like this:

```sh
#!/bin/bash

for a in {0000..9999}
do
~/leviathan6 $a
done
```
Save the script as brute.sh or any name you prefer, and then make it executable:

```sh
leviathan6@melinda:/tmp/jhalon$ chmod +x brute.sh
leviathan6@melinda:/tmp/jhalon$ ./brute.sh
```

## Running the Script

Give the script ~20 seconds to run, and you should see a blank command line with $ appear...

```sh
$ whoami 
leviathan7
$ cat /etc/leviathan_pass/leviathan7
ahy7MaeBo9
```

Done! We got the password for Leviathan Level 7. Technically this is the last level, but let’s SSH into Leviathan7 to see what’s in there.
