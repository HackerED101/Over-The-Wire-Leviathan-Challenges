# Leviathan Level 7 - OverTheWire Wargame

Congratulations! You have reached **Level 7** of the **Leviathan** wargame on OverTheWire. Here's how you can complete this level.

## Objective

In **Level 7**, you are required to read the **CONGRATULATIONS** file. This file will provide a message confirming that you've successfully completed the **Leviathan** wargame.

## Steps

1. **Log in** to the system using the provided credentials for **leviathan7**:

ssh leviathan7@leviathan.labs.overthewire.org -p 2223


2. **List the contents** of the directory:

ls -la


3. You should see a file named `CONGRATULATIONS` in the output, with restricted read permissions.

4. **Read the contents** of the `CONGRATULATIONS` file by running the `cat` command:

cat CON*


This will display the congratulatory message, confirming you have completed the Leviathan wargame:

Well Done, you seem to have used a *nix system before, now try something more serious.

Congratulations! You have conquered Leviathan!


## Conclusion

That's it! You've successfully completed the **Leviathan** wargame. Congratulations on your hard work and persistence in solving all the levels!

---

Happy hacking! 🖥️🔐
