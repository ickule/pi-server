# Autoconfig WSL

This repository will hold my personal configs for my pi secondary server using Ansible.
It can be used on any RaspberrypiOS based system.

It mainly install security, email notifications, unattended-upgrades and wifi access point.

## 1. Requirements

### 1.1 General requirements

This setup assumes that you have key based ssh access to your server.
To setup a new key, you can use the following.

* Generate a new ssh key

    ```sh
    ssh-keygen -t ed25516 -a 128 -f ~/.ssh/enter_your_custom_name
    ```

*Note: You can use the ```-t rsa -b 4096``` option instead of ```-t ed25519``` to generate a key with comparable security and better compatibility at the price of creation and login performance*

* Register your ssh key with your agent

    ```sh
    eval $(ssh-agent -s)  # This starts your agent and gives you its PID
    ssh-add /path/to/your/private/key/file
    ```

* Copy the ssh key to your server

    ```sh
    ssh-copy-id -i /path/to/your/private/key/file username@ip_address
    ```

### 1.2 Install ansible-galaxy requirements

```sh
ansible-galaxy install -r requirements.yml
```

### 1.3 Creating a secret vault

Create a new secret vault with ansible:

```bash
ansible-vault create /secret/folder/path/secret.yml
```

### 1.4 Extra variables

You needs the following variables defined manually.
It would be well suited for a vault ;)

* email
* email_smtp_host
* email_smtp_port_startls
* email_password
* samba_private_password
* wireless:
    wpa:
        ssid
        passphrase

## 2. Using the ansible playbook

With a system featuring the previous requirements, we can run the playbooks.

```bash
ansible-playbook setup.yml
```

## Credits/Sources
