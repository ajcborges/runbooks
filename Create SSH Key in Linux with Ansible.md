# Create SSH Key in Linux with Ansible

```yaml
layout: runbook
title: "SSH Key Generation with Ansible"
date: 2023-06-10 19:00:00 +1000
categories: homelab
tags: homelab linux sshkeys iac ansible
```

## Runbook Steps:

#### Create SSH Key in Linux with Ansible

::: info
This section of the runbook provides step-by-step instructions on using an Ansible playbook to generate an SSH key with a customizable key name and comment on the localhost.

:::

##### **Prerequisites**

- Ansible is installed on the localhost machine.

##### **Steps**

1. Open a terminal or command prompt on the localhost.
2. Create a new file called `create_ssh_key.yml` and open it in a text editor.
3. Copy the following YAML content into the `create_ssh_key.yml` file:

```
---
- name: Create SSH Key in Linux
  hosts: localhost
  gather_facts: false
  vars_prompt:
    - name: ssh_key_name
      prompt: "Enter the SSH key name (e.g., rsa_hostname):"
      private: no

    - name: ssh_key_comment
      prompt: "Enter the SSH key comment (e.g., your_email_address):"
      private: no

  tasks:
    - name: Generate SSH key
      ansible.builtin.shell: ssh-keygen -o -a 100 -t ed25519 -f ~/.ssh/{{ ssh_key_name }} -C {{ ssh_key_comment }}
      args:
        creates: "~/.ssh/{{ ssh_key_name }}"

    - name: Display public key
      ansible.builtin.debug:
        msg: "Public key content:\n{{ lookup('file', '~/.ssh/{{ ssh_key_name }}.pub') }}"
```

1. Save the `create_ssh_key.yml` file.
2. Open a terminal or command prompt and navigate to the directory where the `create_ssh_key.yml` file is located.
3. Run the following command to execute the Ansible playbook:

```
ansible-playbook create_ssh_key.yml
```

1. When prompted, enter the desired SSH key name and comment as requested.
2. Wait for the playbook execution to complete. Ansible will generate the SSH key using the provided parameters.
3. Once the playbook execution is finished, the public key content will be displayed in the terminal or command prompt.
4. The generated SSH key pair will be stored in the `~/.ssh/` directory on the localhost. The private key will be named `{{ ssh_key_name }}`, and the corresponding public key will be named `{{ ssh_key_name }}.pub`.

With this runbook, you can easily create an SSH key pair with a customized key name and comment on your localhost machine using Ansible. Remember to replace the placeholders `{{ ssh_key_name }}` and `{{ ssh_key_comment }}` with the desired values when prompted.