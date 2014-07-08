# Vagrant dev box
Create a local vm as a dev box with Vagrant, provisioned with Ansible.

##Instructions
Create a vagrant inventory file in /etc/ansible/hosts with format:
```ini
devbox ansible_ssh_port=2222 ansible_ssh_host=localhost
```

Remember on first login to set a passphrase for your user ``passwd <user>`` and for the created ssh key in ~/.ssh/id_rsa
