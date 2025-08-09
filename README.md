####### Preparación de ambiente #######

En el nuevo Bastión o Controller, crear nuevo usuario en nuestro caso utilizamos "sysadmin" con permisos de sudo.

$sudo useradd -m -s /bin/bash sysadmin
$sudo passwd sysadmin
$sudo usermod -aG wheel sysadmin

#Instalar ANSIBLE#

$sudo dnf install -y ansible-core

#Instalar ANSIBLE-GALAXY, para ejecución de modulos, etc según requisitos#

$ansible-galaxy install -r collections/requirements.yaml

#Generar clave pública y agregarlo al Centro de confianza de GIT#

$ssh-keygen

#Para ver la clave pública y poder pegarla en los settings de Github#

$cat ~/.ssh/id_rsa.pub

#Copiar clave pública y añadirla a Settings > SSH Keys en cuenta Github#

"Copiar la clave pública de tu Bastión hacia los Servidores, en nuestro caso 192.168.1.100 y 192.168.101".

#ssh-copy-id sysadmin@192.168.1.100
#ssh-copy-id sysadmin@192.168.1.101

Instalar GIT:
$sudo dnf install git

Hacer el GIT Clone, del repositorio
$git clone git@github.com:jr334170/ort_obligatorio_tsl2025.git

Chequear que se haya creado correctamente el arbol de directorios y archivos.

$tree

.
├── ansible.cfg
├── collections
│   └── requirements.yaml
├── inventories
│   ├── all.yaml
│   ├── group_vars
│   │   ├── centos.yml
│   │   └── ubuntu.yml
│   └── inventory.ini
├── LICENSE
├── playbooks
│   ├── hardening.yml
│   └── nfs_setup.yml
├── README.md
└── secret.yml

####### Tarea AD-HOC #######

- Listar todos los usuarios en servidor Ubuntu
$ansible ubuntu -m command -a "cut -d: -f1 /etc/passwd"

- Listar todos los usuarios en servidor Ubuntu
$ansible ubuntu -m command -a "cut -d: -f1 /etc/passwd"

- Que el servicio chrony esté instalado y funcionando en servidor Centos
$ansible centos -m shell -a "dnf install -y chrony && systemctl enable --now chronyd" --become --ask-become-pass

#######################################################################################################################

####### Tarea Playbooks #######


#Ejecución de los Playbooks

Centos:
 $ansible-playbook -i inventories/inventory.ini playbooks/nfs_setup.yml --become --extra-vars "@secret.yml" --ask-vault-pass

Ubuntu:
 $ansible-playbook -i inventories/inventory.ini playbooks/hardening.yml --become --extra-vars "@secret.yml" --ask-vault-pass


#######################################################################################################################

