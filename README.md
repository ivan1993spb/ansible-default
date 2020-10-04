
# Ansible-Default

Ansible playbooks for default server settings. The playbooks works only with CentOS.

## Presettings

1. Check whether you have python 2.7 and pip
2. Clone the repository
3. `git submodules init`
4. Initialize virtual environment and install dependencies:
    ```bash
    virtualenv -p python2 .venv
    source .venv/bin/activate
    pip install -r requirements.txt
    ```
5. Create `inventories` file:
    ```
    [all]
    host1
    host2
    hostN
    ```
6. Setup variables in `group_vars/all.yml`:
    ```bash
    cp group_vars/all.yml.sample group_vars/all.yml
    ```

## Run the playbooks

```
# Run disabling of selinux
ansible-playbook -i inventories selinux.yml
# Wait for reboot...

# Run setting up of packages, tools, iptables, user and ssh
ansible-playbook -i inventories \
    roles.yml \
    iptables.yml \
    common.yml \
    python.yml \
    user.yml \
    docker.yml \
    ssh.yml

# Run the playbook without inventories file
ansible-playbook -u root -k  -i '192.168.61.1,' selinux.yml
```

Use flags `-K`, `-k`, `-u` to control access.

## License

See [LICENSE](LICENSE).
