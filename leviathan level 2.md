Level 2 -> 3 Walkthrough

This document details how to exploit a vulnerability in the printfile program to gain access to the /etc/leviathan_pass/leviathan3 file.

Disclaimer: This walkthrough is for educational purposes only. Exploiting vulnerabilities without permission can have legal ramifications.
Understanding the Program

The printfile program appears to function similarly to the cat command,  reading and displaying the contents of a specified file. However, the program exhibits a security weakness in how it utilizes file paths.
Vulnerability Analysis

    The program relies on the access() function to verify file permissions. This function employs the process's real user ID rather than the effective user ID.
    The printfile program calls /bin/cat to display the file's contents. Notably, /bin/cat interprets only the initial portion of the filename provided within quotation marks.

Exploitation Strategy

    Create a symbolic link named "pass" that points to the target file /etc/leviathan_pass/leviathan3.
    Construct a filename with a space, such as "pass file.txt".
    Execute printfile with the crafted filename as an argument.

When printfile encounters the space, it treats "pass" and "file.txt" as separate files. Since "pass" is a symbolic link to the desired file,  /bin/cat will attempt to read the contents of /etc/leviathan_pass/leviathan3, granting us access to the password.
Walkthrough Steps

    Establish a Temporary Directory and Text File

Bash

mkdir /tmp/jhalon && touch /tmp/jhalon/test.txt

    Analyze printfile with ltrace

Bash

ltrace ~/printfile test.txt

This command will provide a detailed log of system calls made by printfile during execution.

    Craft a Space-Separated Filename

Bash

touch pass\ file.txt

    Verify the Vulnerability

Bash

ltrace ~/printfile "pass file.txt"

The output should confirm that /bin/cat attempts to read "pass" and "file.txt" as individual files.

    Create a Symbolic Link

Bash

ln -s /etc/leviathan_pass/leviathan3 /tmp/jhalon/pass

This command creates a symbolic link named "pass" within the temporary directory, referencing the target file.

    Exploit the Vulnerability

Bash

~/printfile "pass file.txt"

If successful, this command should output the contents of the /etc/leviathan_pass/leviathan3 file, revealing the password.
