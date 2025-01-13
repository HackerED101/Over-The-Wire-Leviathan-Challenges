# OverTheWire - Leviathan level 3 Setup Guide

This guide explains how to complete **Leviathan level 3** and retrieve the password for **Level 4**.

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

2. **Use `sshpass` to log in**: The username for **level 3** is `leviath2`, and the password is the one you retrieved from **Level 1**. Use the following command to log in via SSH:

    ```bash
    sshpass -p <password_from_level_1> ssh leviathan3@leviathan.labs.overthewire.org -p 2223
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

5. **You're in!**: Once logged in, you should see a welcome message and the prompt for the `leviathan3` user:
   
    ```bash
    leviathan3@gibson:~$
    ```

6. **Check who you are**: To verify your current user, run the following command:
   
    ```bash
    whoami
    ```

## Steps

1. **Initial Directory Listing**

    ```sh
    leviathan3@melinda:~$ ls -la
    total 32
    drwxr-xr-x   2 root       root       4096 Mar 21  2015 .
    drwxr-xr-x 172 root       root       4096 Jul 10 14:12 ..
    -rw-r--r--   1 root       root        220 Apr  9  2014 .bash_logout
    -rw-r--r--   1 root       root       3637 Apr  9  2014 .bashrc
    -rw-r--r--   1 root       root        675 Apr  9  2014 .profile
    -r-sr-x---   1 leviathan4 leviathan3 9962 Mar 21  2015 level3
    ```

2. **Running the Executable**

    ```sh
    leviathan3@melinda:~$ ./level3
    Enter the password> 1234
    bzzzzzzzzap. WRONG
    ```

3. **Tracing the Program Execution**

    ```sh
    leviathan3@melinda:~$ ltrace ./level3
    __libc_start_main(0x80485fe, 1, 0xffffd794, 0x80486d0 <unfinished ...>
    strcmp("h0no33", "kakaka")                       = -1
    printf("Enter the password> ")                   = 20
    fgets(Enter the password> 1234
    "1234\n", 256, 0xf7fc9c20)                 = 0xffffd58c
    strcmp("1234\n", "snlprintf\n")                  = -1
    puts("bzzzzzzzzap. WRONG"bzzzzzzzzap. WRONG
    )                       = 19
    +++ exited (status 0) +++
    ```

4. **Using the Correct Password**

    ```sh
    leviathan3@melinda:~$ ./level3
    Enter the password> snlprintf
    [You've got shell]!
    $ whoami
    leviathan4
    $ cat /etc/leviathan_pass/leviathan4
    vuH0coox6m
    ```

And there you have it! You got the password for leviathan4. On to the next challenge!
