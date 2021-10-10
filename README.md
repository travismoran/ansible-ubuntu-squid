# Ansible playbooks to install fail2ban on Ubuntu for sshd & configure a docker squid proxy(datadog/squid)


## install latest version of Ansible
```
# remove older version
sudo apt remove ansible && sudo apt --purge autoremove

# refresh apt
sudo apt update

# install software-properties-common & add ppa:ansible/ansible
sudo apt install software-properties-common
sudo apt-add-repository ppa:ansible/ansible

# pull ppa:ansible/ansible updates
sudo apt update

# install latest version of ansible
sudo apt install ansible

# show version
ansible --version
```

## clone playbooks repo
```
sudo apt -y install git
git clone https://github.com/travismoran/ansible-ubuntu-squid.git
cd ansible-ubuntu-squid
```


## Default fail2ban sshd config with aggressive & pubkey mode enabled

```
ansible-playbook ubuntu-fail2ban-sshd.yml
```
 
## Squid Proxy fail2ban config including Default ssh config

```
ansible-playbook ubuntu-f2b-squid.yml
```


