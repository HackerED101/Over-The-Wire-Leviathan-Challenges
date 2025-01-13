# OverTheWire - Leviathan Level 1 Setup Guide

This guide explains how to complete **Leviathan Level 1** and retrieve the password for **Level 2**.

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

## Steps to Connect to Leviathan Level 1

1. **Open a terminal**: If you're on Linux or macOS, open a terminal window. On Windows, you may need an SSH client like `PuTTY` or use the Windows Subsystem for Linux (WSL).

2. **Use `sshpass` to log in**: The username for **Level 1** is `leviathan1`, and the password is the one you retrieved from **Level 0**. Use the following command to log in via SSH:

    ```bash
    sshpass -p <password_from_level_0> ssh leviathan1@leviathan.labs.overthewire.org -p 2223
    ```

   Replace `<password_from_level_0>` with the password you found in Level 0.

3. **Confirm the host authenticity**: When connecting for the first time, you might see the following prompt:
   
    ```text
    The authenticity of host '[leviathan.labs.overthewire.org]:2223 ([13.48.119.24]:2223)' can't be established.
    ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.
    Are you sure you want to continue connecting (yes/no/[fingerprint])?
    ```

   Type `yes` to continue and add the host to the list of known hosts.

4. **Enter the password**: After entering the `sshpass` command, you should be logged in to the server. If you're not using `sshpass`, the server will prompt you for the password you retrieved from Level 0.

5. **You're in!**: Once logged in, you should see a welcome message and the prompt for the `leviathan1` user:
   
    ```bash
    leviathan1@gibson:~$
    ```

6. **Check who you are**: To verify your current user, run the following command:
   
    ```bash
    whoami
    ```

   This should return `leviathan1`, confirming you're logged in as the correct user.

7. **List all files**: Now list all files and directories in the current directory by running:

    ```bash
    ls -la
    ```

   In the output, look for a directory named **`checkup`**. The directory may be marked in red, indicating it is protected.

8. **Investigate the `checkup` directory**: Since the directory is protected, we will need to use `ltrace` to observe the password comparison process. To do this, run the following:

    ```bash
    ltrace -e "open,read" <command_to_open_checkup_directory> 
    ```

    Replace `<command_to_open_checkup_directory>` with the actual command you would use to open or access the directory. 

    The `ltrace` tool will allow us to see how the password is being processed.

9. **Bypass the password protection**: You can enter `null` as a password during this process. This will allow the system to compare the input password and you will eventually see that the password for the directory is **`sex`**.

10. **Access the `checkup` directory**: With the password **`sex`**, you can now access the protected directory.

11. **Retrieve the password for Level 2**: Now that you have accessed the `checkup` directory, run the following command to get the password for **Level 2**:

    ```bash
    cat /etc/leviathan_pass/leviathan2
    ```

    This will display the password for **Level 2**.

12. **Log in to Level 2**: Use the password you retrieved to log in to **Level 2**.

## Troubleshooting

- If you're unable to connect, ensure the server is up by testing the connection with `telnet`:
  
    ```bash
    telnet leviathan.labs.overthewire.org 2223
    ```

- If you receive an error like `Permission denied, please try again.`, double-check the username and password, and make sure you're using the correct login credentials (`leviathan1` and the password you found in Level 0).

## Helpful Links

- [OverTheWire Wargames](https://www.overthewire.org/wargames/)
- [Leviathan Game Info](https://www.overthewire.org/wargames/leviathan/)

Enjoy the challenge, and remember—no spoilers!
