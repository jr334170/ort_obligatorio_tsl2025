# ort_obligatorio_tsl2025
Repositorio Taller servidores Linux ORT 2025.

#Instalar ansible-core a nivel de la VM Bastion.

Sudo dnf install -y ansible-core

Instalar Ansible-Galaxy para manejar roles y colecciones reutilizables.

$ansible-galaxy install -r collections/requirements.yaml


####### Tarea comandos adhoc: #######

- Listar todos los usuarios en servidor Ubuntu

$ansible ubuntu -m command -a "cut -d: -f1 /etc/passwd"

- Listar todos los usuarios en servidor Ubuntu

$ansible ubuntu -m command -a "cut -d: -f1 /etc/passwd"

- Que el servicio chrony esté instalado y funcionando en servidor Centos

$ansible centos -m shell -a "dnf install -y chrony && systemctl enable --now chronyd" --become --ask-become-pass

######## Tareas Playbooks: #########

##Crear directorios y archivos con lo necesario:

##Modificar los host dependiendo de la config de red elegida

touch ansible.cfg
echo "[defaults]
inventory = ./inventories/inventory.ini" >> ansible.cfg

mkdir -p inventories
touch inventories/inventory.ini
echo "[centos]
centos01        ansible_host=192.168.1.101

[ubuntu]
ubuntu01        ansible_host=192.168.1.100

[linux:children]
centos
ubuntu

[fileserver]
centos01" >> inventories/inventory.ini
 
 
mkdir -p collections
touch collections/requirements.yaml
echo "---
collections:
  - ansible.posix" >> collections/requirements.yaml
 
mkdir -p playbooks
mkdir -p inventories/group_vars
touch inventories/group_vars/ubuntu.yml
echo "ansible_user: sysadmin" >> inventories/group_vars/ubuntu.yml
touch inventories/group_vars/centos.yml
echo "ansible_user: sysadmin" >> inventories/group_vars/centos.yml

#Chequear que haya este arbol de directorios creado:

├── ansible.cfg
├── collections
│   └── requirements.yaml
├── inventories
│   ├── all.yaml
│   ├── group_vars
│   │   ├── centos.yml
│   │   └── ubuntu.yml
│   └── inventory.ini
├── LICENSE
├── playbooks
│   ├── hardening.yml
│   └── nfs_setup.yml
├── README.md
└── secret.yml



#Ejecución de los Playbooks

Centos:
$ansible-playbook -i inventories/inventory.ini playbooks/nfs_setup.yml --become --extra-vars "@secret.yml" --ask-vault-pass


Ubuntu:
$ansible-playbook -i inventories/inventory.ini playbooks/hardening.yml   --become --extra-vars "@secret.yml" --ask-vault-pass





