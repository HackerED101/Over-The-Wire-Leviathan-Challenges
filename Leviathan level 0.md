# OverTheWire - Leviathan Level 0 Setup Guide

This guide explains how to connect to the OverTheWire **Leviathan Level 0** challenge and start playing using SSH.

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

## Steps to Connect to Leviathan Level 0

1. **Open a terminal**: If you're on Linux or macOS, open a terminal window. On Windows, you may need an SSH client like `PuTTY` or use the Windows Subsystem for Linux (WSL).

2. **Use `sshpass` to log in**: The username for **Level 0** is `leviathan0`, and the password is `leviathan0`. To log in via SSH using `sshpass`, run the following command in your terminal:

    ```bash
    sshpass -p leviathan0 ssh leviathan0@leviathan.labs.overthewire.org -p 2223
    ```

   - The `-p` option provides the password (`leviathan0`).
   - `sshpass` automatically passes the password during the SSH login.

3. **Confirm the host authenticity**: When connecting for the first time, you might see the following prompt:
   
    ```text
    The authenticity of host '[leviathan.labs.overthewire.org]:2223 ([13.48.119.24]:2223)' can't be established.
    ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.
    Are you sure you want to continue connecting (yes/no/[fingerprint])?
    ```

   Type `yes` to continue and add the host to the list of known hosts.

4. **Enter the password**: After entering the `sshpass` command, you should be logged in to the server. If you are not using `sshpass`, the server will prompt you for the password (`leviathan0`).

5. **You're in!**: Once logged in, you should see a welcome message and the prompt for the `leviathan0` user:
   
    ```bash
    leviathan0@gibson:~$
    ```
6. **Running `whoami`**: After logging in, confirm the username with the `whoami` command.
 **Running `ls -la`**: List the files in the directory to find the `.backup` folder.
 **Accessing `.backup`**: Navigate to the `.backup` directory and use `grep` to find the password in `bookmark.html`.

## Troubleshooting

- If you're unable to connect, ensure the server is up by testing the connection with `telnet`:
  
    ```bash
    telnet leviathan.labs.overthewire.org 2223
    ```

- If you receive an error like `Permission denied, please try again.`, double-check the username and password, and make sure you're using the correct login credentials (`leviathan0` and `leviathan0`).

## Helpful Links

- [OverTheWire Wargames](https://www.overthewire.org/wargames/)
- [Leviathan Game Info](https://www.overthewire.org/wargames/leviathan/)

Enjoy the challenge, and remember—no spoilers!
