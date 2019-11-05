# Ansible para la instalacion de TheHive

## Tabla de contenidos

1. [Pre-requisitos](#pre-requisitos)
2. [Instrucciones para el despliegue de TheHive](#instrucciones-para-el-despliegue-de-thehive)
3. [Post-despligue](#post-despligue)


## Pre-requisitos

1. Contar con un servidor con Ubuntu/Debian.

2. Agregar clave SSH publica del dispositivo desde el cual se realiza el despliegue de TheHive

3. Contar con un servidor con InfluxDB y Grafana. El servidor desplegado con Ansible sera integrado con Grafana. 
   Comprobar configuracion de archivo: `roles/telegraf_install/files/telegraf.conf` (AGREGAR!!!!!)

## Instrucciones para el despliegue de TheHive


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
    

    ```
    
*  Ejecutar ansible sobre el servidor `"thehiveuser"` (el username se define en la opcion extra_var):

    ```
    ansible-playbook -i hosts -l thehive setup.yml --extra-var "target=thehiveuser" --ask-become-pass
    ```

## Post-despligue

1.  Ingresar desde el navegador a: `ipserverthehive:9000`
2.  Activar opcion `"Actualizar base de datos"`.
3.  Crear usuario `ADMIN`.
4.  Crear `API-KEY` en `Users` (Barra superior derecha en la lista deplegable "ADMIN").
5.  Activar la opcion `"Reveal"` sobre la `API-KEY`, la misma sera usada para el despliegue de Cortex.















