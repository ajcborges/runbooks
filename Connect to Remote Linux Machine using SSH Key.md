
```yaml
layout: runbook
title: "Connect to Remote Linux Machine using SSH Key"
date: 2023-06-10 19:00:00 +1000
categories: homelab
tags: homelab linux sshkeys
```

## Runbook Steps:

#### Connect to Remote Linux Machine using SSH Key

::: info
This section of the runbook provides steps to use an SSH key to connect to a remote Linux machine.

:::

- Copy the public key to the remote Linux machine:
  - If the public key is not already on the remote machine, use the `ssh-copy-id` command to copy the public key to the remote machine's `~/.ssh/authorized_keys` file:

    ```
    $> ssh-copy-id -i ~/.ssh/id_rsa.pub {username}@{remote-host}
    ```
  - If `ssh-copy-id` is not available, manually append the contents of the public key file (`~/.ssh/id_rsa.pub`) to the `~/.ssh/authorized_keys` file on the remote machine:

    ```
    $> cat ~/.ssh/id_rsa.pub | ssh {username}@{remote-host} "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
    ```
- Set appropriate permissions on the remote machine:
  - Log in to the remote machine using SSH:

    ```
    $> ssh {username}@{remote-host}
    ```
  - Set the correct permissions for the `~/.ssh/` directory:

    ```
    $> chmod 700 ~/.ssh
    ```
  - Set the correct permissions for the `~/.ssh/authorized_keys` file:

    ```
    $> chmod 600 ~/.ssh/authorized_keys
    ```
  - Exit the SSH session:

    ```
    $> exit
    ```
- Open the SSH configuration file on your local machine:

  ```
  $> nano ~/.ssh/config
  ```

  If the file doesn't exist, create it.
- Add an entry in the SSH configuration file for the remote Linux machine:

  ```
  Host {alias}
      HostName {remote-host}
      User {username}
      IdentityFile {/path/to/ssh_key}
  ```

  Replace `{alias}` with an alias of your choice for the remote machine, `{remote-host}` with the IP address or hostname of the remote machine, `{username}` with your username on the remote machine and the {`/path/to/ssh_key}`
- Save and close the SSH configuration file.
- Set appropriate permissions on the SSH configuration file:

  ```
  $> chmod 600 ~/.ssh/config
  ```
- Connect to the remote machine using the configured SSH alias:

  ```
  $> ssh {alias}
  ```
- You should now be connected to the remote Linux machine using the SSH configuration file and the specified alias. Ensure that the private key (`id_rsa`) is securely stored on your local machine and not shared with others.
- To avoid being prompted for the passphrase every time you SSH into the remote host, you can use SSH agent to securely store and manage your SSH keys. Here's how you can configure SSH agent to automatically handle your SSH key's passphrase:
  - Start the SSH agent:

    ```
    $> eval "$(ssh-agent -s)"
    ```
  - Add your SSH private key to the SSH agent:

    ```
    $> ssh-add {/path/to/ssh_key}
    ```

    If your private key is stored in a different location or has a different filename, adjust the command accordingly.
  - Enter the passphrase for your SSH key when prompted. The passphrase will be securely stored in the SSH agent for the current session.
  - Now, when you use the SSH command with the specified alias, you should not be prompted for the passphrase anymore. The SSH agent will automatically provide the passphrase from its cache.
- By configuring SSH agent and adding your SSH key, you enable automatic passphrase handling, eliminating the need to enter it every time you connect to the remote host. The SSH agent securely manages your private key's passphrase, enhancing convenience while maintaining security.

  ::: info
  Remember to keep your private key file (`id_rsa`) secure and protected on your local machine. Additionally, ensure that you have appropriate permissions set for the private key file (`chmod 600 ~/.ssh/id_rsa`).

  :::