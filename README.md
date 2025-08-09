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


flowchart TD
    S[Inicio play NFS\nhosts: centos, become: true]
    S --> P1[Instalar paquetes:\n nfs-utils, firewalld]
    P1 --> F1[Iniciar y habilitar firewalld]
    F1 --> FW1[Abrir 2049/tcp en firewall]
    FW1 --> FW2[Abrir 2049/udp en firewall]
    FW2 --> D1[Crear /var/nfs_shared\nowner: nobody:nobody\nmode: 0777]
    D1 --> E1[Agregar export en /etc/exports]
    E1 -->|notify| H1[Handler: exportfs -ra]
    H1 --> H2[Handler: recargar nfs-server]
    E1 --> SVC[Iniciar y habilitar nfs-server]
    SVC --> V[Fin]



Ubuntu:
 $ansible-playbook -i inventories/inventory.ini playbooks/hardening.yml --become --extra-vars "@secret.yml" --ask-vault-pass

flowchart TD
    S[Inicio play Hardening\nhosts: ubuntu, become: true]
    S --> U1[apt dist-upgrade\n(update_cache: yes)]
    U1 -->|notify| HR1[Handler: Reboot si hubo updates]
    U1 --> U2[Instalar ufw]
    U2 --> U3[Obtener estado de ufw\nufw status verbose]
    U3 --> U4[Default deny incoming\n(si no estaba)]
    U4 --> U5[Allow outgoing\n(si no estaba)]
    U5 --> U6[Permitir OpenSSH\n(si no existe regla)]
    U6 --> U7[Habilitar ufw\n(si no estaba activo)]
    U7 --> SSH1[sshd_config:\nPasswordAuthentication no]
    SSH1 -->|notify| HR2[Handler: Restart ssh]
    SSH1 --> SSH2[sshd_config:\nPermitRootLogin no]
    SSH2 -->|notify| HR2
    SSH2 --> F2[Instalar fail2ban]
    F2 --> F3[Crear/actualizar jail.d/sshd.local\n(enabled=true, límites)]
    F3 -->|notify| HR3[Handler: Restart fail2ban]
    F3 --> F4[fail2ban started + enabled]
    F4 --> V[Fin]

    HR1:::handler
    HR2:::handler
    HR3:::handler

    classDef handler fill:#eef,stroke:#55f,stroke-width:1px;







#######################################################################################################################

