# Create a User on Ubuntu Linux with Ansible

```yaml
layout: runbook
title: "Create User on Ubuntu Linux with Ansible"
date: 2023-06-10 19:00:00 +1000
categories: homelab
tags: homelab linux iac ansible
```

## Runbook Steps:

#### Create a User on Ubuntu Linux with Ansible

::: info
This section of the runbook provides steps to create a user on an Ubuntu Linux or into your localhost.

:::

##### **Prerequisites**

- Ansible is installed on the localhost machine.

##### **Steps**

- Open a terminal or command prompt on the localhost.
- Create a new file called `create_user.yml` and open it in a text editor.
- Copy the following YAML content into the `create_user.yml` file:

```
---
- name: Create User on Ubuntu Linux Machine
  hosts: "{{ target_host | default('localhost') }}"
  gather_facts: false
  vars_prompt:
    - name: username
      prompt: "Enter the username for the new user:"
      private: no

    - name: home_directory
      prompt: "Enter the home directory for the new user (e.g., /home/{{ username }}):"
      private: no

    - name: user_shell
      prompt: "Enter the desired shell for the new user (e.g., /bin/bash):"
      private: no

  tasks:
    - name: Create user
      ansible.builtin.user:
        name: "{{ username }}"
        comment: "Created by Ansible"
        home: "{{ home_directory }}"
        shell: "{{ user_shell }}"
        create_home: yes
        password_lock: yes
```

- Save the playbook as `create_user.yml`.
- Open a terminal or command prompt.
  - If you want to create the user on a remote host, make sure you have SSH connectivity to the target host and ensure it is accessible in your Ansible inventory.
- Run the following command to execute the playbook:

```
$> ansible-playbook create_user.yml --extra-vars "target_host=your_target_host"
```

Replace `your_target_host` with the hostname or IP address of the remote host where you want to create the user. If you want to execute the playbook on the localhost, you can omit the `--extra-vars "target_host=your_target_host"` part.

- When prompted, enter the requested information for the new user, including the username, home directory, and desired shell.
- Wait for the playbook execution to complete. Ansible will create the user with the provided parameters.

The playbook uses the `ansible.builtin.user` module to create the user on the specified host. It sets the username, comment, home directory, shell, and other necessary options.