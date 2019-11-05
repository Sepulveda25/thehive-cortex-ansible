# Ansible para la instalacion de nodos FORWARD y MASTER para Security Onion.

## Tabla de contenidos

1. [Pre-requisitos](#pre-requisitos)
2. [Instrucciones para el despliegue de Cortex](#instrucciones-para-el-despliegue-de-cortex)
4. [Referencias](#referencias)


## Pre-requisitos

1. Contar con un servidor con Ubuntu/Debian con TheHive previamente instalado
    link al repo: https://gitlab.unc.edu.ar/csirt/thehive-cortex-ansible/tree/master/thehive-ansible

#2. Agregar clave SSH publica del dispositivo desde el cual se realiza el despliegue de TheHive

2. Contar con un servidor con InfluxDB y Grafana. El servidor desplegado con Ansible sera integrado con Grafana. 
   Comprobar configuracion de archivo: `roles/telegraf_install/files/telegraf.conf` (AGREGAR!!!!!)


## [Instrucciones para el despliegue de Cortex]


*  Agregar nombre de usuario del servidor `host` en el grupo `thehive` (Ej. user thehiveuser):

    ```
    
      [thehive]
      thehiveuser

    ```
    
    
*  En la carpeta `host_vars` agregar un archivo yml (`thehiveuser.yml`) en la que se especifiquen las variables
   del archivo template_thehive.yml (Ej. thehiveuser.yml):

    ```
    
      ansible_host: '172.16.81.111'
      ansible_user: 'thehive'

      path_default_analyzers: "/opt/Cortex-Analyzers/analyzers"
      path_my_own_analyzers: " "

      path_default_responders: "/opt/Cortex-Analyzers/responders"
      path_my_own_responders: " "

    ```

*  En el mismo archivo, colocar la API-KEY que generamos en la opcion `Users` (Barra superior derecha en la lista deplegable "ADMIN").
*  Para ello, hacemos click en la opcion REVEAL y la copiamos
*  La pegamos en el archivo que estabamos modificando (`thehiveuser.yml`). 
*  Por ejemplo, si la clave fuera `X0YDSBCTOPtT1jYGoAG8deupsBJPFeJo`

    ```
    api_admin_the_hive: X0YDSBCTOPtT1jYGoAG8deupsBJPFeJo
    
    ```

ansible-playbook -i hosts -l thehive setup.yml --extra-var "target=thehiveuser" --ask-become-pass





