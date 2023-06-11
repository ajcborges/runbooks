# Create SSH Key in Linux

```yaml
layout: runbook
title: "SSH Key Generation"
date: 2023-06-10 19:00:00 +1000
categories: homelab
tags: homelab linux sshkeys
```

## Runbook Steps:

#### Create SSH Key in Linux

::: info
This section of the runbook provides steps to create an SSH key pair on a Linux machine.  
It's important to emphasize the significance of keeping the private key secure and not sharing it with unauthorized individuals. 

:::

- Open the terminal on your Linux machine.
- Run the following command to generate an SSH key pair:

```

$> ssh-keygen -o -a 100 -t ed25519 -f ~/.ssh/rsa_<name> -C <email address>
```

Remember to adapt the command and file paths to your specific needs and preferences. 

Explanation:

`-o`: This flag specifies the use of the OpenSSH format for the key file.

`-a 100`: This flag sets the number of KDF (Key Derivation Function) rounds used to decrypt the private key. A higher value increases the resistance to brute-force attacks.

`-t ed25519`: This flag specifies the type of key to generate, in this case, an Ed25519 key. Ed25519 is a newer algorithm that provides security and performance benefits.

`-f ~/.ssh/rsa_<name>`: This flag specifies the file path and name for the private and public key files. In this example, the private key will be saved as `rsa_<name>` in the `~/.ssh/` directory.

`-C <email address>`: This flag adds a comment to the public key file, which can be useful for identifying the key owner or providing additional information.

- You will be prompted to enter the file path where you want to save the key. The default location is usually `~/.ssh/id_rsa`, which is fine for most cases. Press Enter to proceed with the default location, or specify a different path if desired.

  ```
  Enter file in which to save the key (/home/user/.ssh/id_rsa):
  ```

  If you want to use the default location, simply press Enter without typing anything. The SSH key pair will be saved in `~/.ssh/id_rsa`.

  However, if you prefer to save the key pair in a different location or under a different name, you can specify a custom file path. For example, you can enter `/path/to/my_ssh_key` to save the key pair in a directory called `my_ssh_key` located at the specified path.

  Keep in mind that if you choose a custom file path, you will need to remember and use that path when referencing the SSH key pair in subsequent steps or when configuring SSH on remote servers or systems.
- Next, you will be asked to enter a passphrase. The passphrase adds an extra layer of security to your SSH key. It's optional but highly recommended. If you choose to use a passphrase, enter it and remember it. Press Enter to continue without a passphrase if you prefer.

  ```
  Enter passphrase (empty for no passphrase):
  ```

  Confirm passphrase:

  ```
  Enter same passphrase again:
  ```

  If you choose to use a passphrase, it's highly recommended to use a strong and unique passphrase that combines a mix of uppercase and lowercase letters, numbers, and special characters. The passphrase should be something memorable to you but difficult for others to guess.

  To enter a passphrase, type it and press Enter. You'll be prompted to re-enter the passphrase to ensure accuracy.

  If you prefer not to use a passphrase and have your private key unprotected by an additional password, simply press Enter without typing anything. Keep in mind that choosing not to use a passphrase makes it easier for someone with unauthorized access to your private key to use it.

  Deciding whether to use a passphrase depends on your security requirements and the level of protection you want for your SSH key. It's generally recommended to use a passphrase to enhance the security of your private key, especially if the key provides access to sensitive systems or data.
- The SSH key pair (a public key and a private key) will be generated and saved in the specified location. The private key will be saved as `id_rsa` (or as you specified), and the public key will have the same name with `.pub` extension.

  The private key is the file that contains sensitive information and should be kept secure. It is typically saved as `id_rsa` in the `.ssh` directory. This private key should not be shared with anyone.

  The public key is the file that can be shared with remote servers or systems for authentication purposes. It has the same name as the private key, but with a `.pub` extension. For example, if the private key is `id_rsa`, the public key will be `id_rsa.pub`. The public key is safe to share and can be provided to the administrators of the remote servers or systems you want to access.

  Both the private and public keys are necessary for SSH key-based authentication. The private key resides on your local machine, while the public key is placed on the remote servers or systems you want to connect to.
- Congratulations! You have successfully generated your SSH key pair. The private key (`id_rsa`) should be kept secure and not shared with anyone, while the public key (`id_rsa.pub`) can be shared with the remote servers or systems you want to connect to.