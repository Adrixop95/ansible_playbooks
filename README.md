# Ansible playbooks

Zbiór różnych playbooków do Ansible.
Zostały one napisane aby przypomnieć sobie jak używa się Ansible oraz aby zautomatyzować trochę pracę serwerów i stanowisk z Ubuntu GNU/Linux.

### Instalacja 

Instalacja Ansible na hoście:
```
sudo apt-add-repository -y ppa:ansible/ansible
sudo apt-get update
sudo apt-get install ansible -y
```

Wymagane pliki do wykonania Ansible playbooks na maszynach:
```
sudo apt-get install python2.7 python-pip aptitude -y
sudo pip install virtualenv -U
```

Do działania Ansible wymagany jest plik hosts posiadający w sobie zbiór adresów IP urządzeń do których maja zostać wysłane polecenia. Przykład pliku:
```
# This is the default ansible 'hosts' file.
#
# It should live in /etc/ansible/hosts
#
#   - Comments begin with the '#' character
#   - Blank lines are ignored
#   - Groups of hosts are delimited by [header] elements
#   - You can enter hostnames or ip addresses
#   - A hostname/ip can be a member of multiple groups

[web]
192.168.56.101
192.168.56.102

[local]
192.168.1.64

```

### Przydane komendy Ansible

Ping urządzeń w pliku host:

ansible -i hosts (lokalizacja pliku hosts) web (dany zbiór adresów) -m ping --ask-password
```
adrox@MSI-Adrox:/mnt/c/Users/Adrox/GitHub/ansible_playbooks/ubuntu_books$ ansible -i hosts web -m ping --ask-pass

SSH password:
192.168.56.102 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

Wywołanie pliku .yml (ansible playbook):
ansible-playbook -i hosts (lokalizacja pliku hosts) plik.yml (playbook jaki chcemy wykonać) (dodatkowe paramentry, np. --ask-sudo-pass aby podać hasło superusers)

```
adrox@MSI-Adrox:/mnt/c/Users/Adrox/GitHub/ansible_playbooks/ubuntu_books$ ansible-playbook -i hosts update_ubuntu.yml --ask-sudo-pass
[DEPRECATION WARNING]: The sudo command line option has been deprecated in favor of the "become" command line
arguments. This feature will be removed in version 2.6. Deprecation warnings can be disabled by setting
deprecation_warnings=False in ansible.cfg.
SUDO password:

PLAY [web] *************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************
ok: [192.168.56.102]

TASK [Install OS update] ***********************************************************************************************
ok: [192.168.56.102]

PLAY RECAP *************************************************************************************************************
192.168.56.102             : ok=2    changed=0    unreachable=0    failed=0
```