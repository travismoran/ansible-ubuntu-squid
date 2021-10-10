### Ansible playbooks 
- fail2ban on Ubuntu
- fail2ban config for dockerized squid proxy(datadog/squid)
- docker-compose.yml to start squid proxy


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

## Squid Proxy docker-compose

# get docker
```
sudo curl -fsSL get.docker.com | sh
```

# get docker-compose
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

### Default Squid Proxy User & Pass included in repo
```
user:
71258b13fab16f2141ff9d91af6c16a7

password:
kTuHD8fQ9ILSCcj6q690WXlt-m2sRjWX

```


## I strongly recommend you follow the next steps to create your own user/password file.

### How to generate strong credentials for squid proxy

#### generate strong random username using bash
```
head -c16 /dev/urandom | md5sum
```

#### generate strong random password on bash line using urandom
```
< /dev/urandom tr -dc _A-Z-a-z-0-9 | head -c${1:-32};echo;
```

#### generate password file username must be only letters and numbers
```
# install apache2-utils
apt install apache2-utils

#generate encrypted password file

htpasswd -c squid/etc/squid/passwords <yourstrongusername>
```




## Start docker-compose stack
```
docker-compose up -d
```

### Configure your browser to connect to the squid proxy using your credentials.

![](.readme/img/ff_proxy1.jpg?raw=true)

![](.readme/img/ff_proxy2.jpg?raw=true)

### Congratulations you have setup a squid proxy with ddos and intrusion protection!

