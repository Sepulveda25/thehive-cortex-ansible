# Ansible para la instalacion de nodos FORWARD y MASTER para Security Onion.

## Tabla de contenidos

1. [Pre-requisitos](#pre-requisitos)
2. [Instrucciones para el despliegue de un nodo Master](#instrucciones-para-el-despliegue-de-un-nodo-master)
3. [Instrucciones para el despliegue de un nodo Forward](#instrucciones-para-el-despliegue-de-un-nodo-forward)
4. [Referencias](#referencias)




ansible-playbook -i hosts -l thehive setup.yml --extra-var "target=thehiveuser" --ask-become-pass





