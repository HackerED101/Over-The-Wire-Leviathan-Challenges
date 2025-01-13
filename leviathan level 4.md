# OverTheWire - Leviathan Level 4 Setup Guide

This guide explains how to complete **Leviathan Level 4** and retrieve the password for **Level 5**.

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

## Steps to Connect to Leviathan Level 4

1. **Open a terminal**: If you're on Linux or macOS, open a terminal window. On Windows, you may need an SSH client like `PuTTY` or use the Windows Subsystem for Linux (WSL).

2. **Use `sshpass` to log in**: The username for **Level 4** is `leviathan4`, and the password is the one you retrieved from **Level 3**. Use the following command to log in via SSH:

    ```bash
    sshpass -p <password_from_level_3> ssh leviathan4@leviathan.labs.overthewire.org -p 2223
    ```

   Replace `<password_from_level_3>` with the password you found in Level 3.

3. **Confirm the host authenticity**: When connecting for the first time, you might see the following prompt:
   
    ```text
    The authenticity of host '[leviathan.labs.overthewire.org]:2223 ([13.48.119.24]:2223)' can't be established.
    ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.
    Are you sure you want to continue connecting (yes/no/[fingerprint])?
    ```

   Type `yes` to continue and add the host to the list of known hosts.

4. **Enter the password**: After entering the `sshpass` command, you should be logged in to the server. If you're not using `sshpass`, the server will prompt you for the password you retrieved from Level 3.

5. **You're in!**: Once logged in, you should see a welcome message and the prompt for the `leviathan4` user:
   
    ```bash
    leviathan4@gibson:~$
    ```

6. **Check who you are**: To verify your current user, run the following command:
   
    ```bash
    whoami
    ```

## Initial Directory Listing

```sh
leviathan4@melinda:~$ ls -la
total 24
drwxr-xr-x   3 root root       4096 Nov 14  2014 .
drwxr-xr-x 172 root root       4096 Jul 10 14:12 ..
-rw-r--r--   1 root root        220 Apr  9  2014 .bash_logout
-rw-r--r--   1 root root       3637 Apr  9  2014 .bashrc
-rw-r--r--   1 root root        675 Apr  9  2014 .profile
dr-xr-x---   2 root leviathan4 4096 Nov 14  2014 .trash
```

## Exploring .trash Directory

```sh
leviathan4@melinda:~$ cd .trash
leviathan4@melinda:~/.trash$ ls -la
total 16
dr-xr-x--- 2 root       leviathan4 4096 Nov 14  2014 .
drwxr-xr-x 3 root       root       4096 Nov 14  2014 ..
-r-sr-x--- 1 leviathan5 leviathan4 7425 Nov 14  2014 bin
```

## Running the Binary File

```sh
leviathan4@melinda:~/.trash$ ./bin
01010100 01101001 01110100 01101000 00110100 01100011 01101111 01101011 01100101 01101001 00001010
```
## Converting Binary to ASCII

The binary output translates to the password Tith4cokei using an online Binary to ASCII converter.

And there you have it! The password for Leviathan Level 5 is Tith4cokei. On to the next challenge!
