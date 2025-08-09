# ort_obligatorio_tsl2025
Repositorio Taller servidores Linux ORT 2025.



Instalar ansible-core a nivel de la VM Bastion.

#Sudo dnf install -y ansible-core

Instalar Ansible-Galaxy para manejar roles y colecciones reutilizables.

$ansible-galaxy install -r collections/requirements.yaml


Comandos adhoc ejecutados.

- Listar todos los usuarios en servidor Ubuntu

$ansible ubuntu -m command -a "cut -d: -f1 /etc/passwd"

- Listar todos los usuarios en servidor Ubuntu

$ansible ubuntu -m command -a "cut -d: -f1 /etc/passwd"

- Que el servicio chrony esté instalado y funcionando en servidor Centos

$ansible centos -m shell -a "dnf install -y chrony && systemctl enable --now chronyd" --become --ask-become-pass



