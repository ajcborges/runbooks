# Create User on Ubuntu Linux Machine

```yaml
layout: runbook
title: "Create User on Ubuntu Linux Machine"
date: 2023-06-10 19:00:00 +1000
categories: homelab
tags: homelab linux sshkeys
```

## Runbook Steps:

#### Create User on Ubuntu Linux Machine

::: info
This section of the runbook provides steps to create a user on an Ubuntu Linux machine.

:::

- Connect to the Ubuntu Linux machine using SSH or log in to the machine directly.
  1. Switch to the root user or a user with sudo privileges, if you didn't log in as `root`:

     ```
     $> sudo su -
     ```
  2. Create a new user with the desired username. Replace `{username}` with the desired username for the new user:

     ```
     $> adduser --home /home/{username} --shell /bin/bash {username}
     ```

     Explanation:
     - The `adduser` command is used to create a new user on the Ubuntu Linux machine.
     - The `--home /home/{username}` flag sets the home directory path for the new user to `/home/{username}`. Replace `{username}` with the desired username for the new user. By default, Ubuntu creates the user's home directory within the `/home` directory with the same name as the username.
     - The `--shell /bin/bash` flag sets the default shell for the new user to `/bin/bash`. This ensures that the user has the Bash shell as the default interactive shell. Bash is the most commonly used shell in Linux.

     After running this command, the system will prompt you to set a password for the new user. Follow the password policy requirements and provide a strong, secure password for the user. Confirm the password when prompted.
  3. Set a password for the new user when prompted. Follow the password policy requirements and provide a strong, secure password. Confirm the password when prompted.
  4. Optional: If you want to grant administrative privileges to the new user, add the user to the `sudo` group:

     ```
     $> usermod -aG sudo {username}
     ```
  5. The new user account is now created. You can switch to the new user and start using it:

     ```
     $> su - {username}
     ```
  6. Test the new user account by running some basic commands or performing tasks specific to your needs.
  7. Remember to log out of the new user account and switch back to the root user or your original user account when finished:

     ```
     $> exit
     ```

  ---