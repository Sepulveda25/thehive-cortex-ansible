# Ansible para la instalacion de TheHive

## Tabla de contenidos

1. [Pre-requisitos](#pre-requisitos)
2. [Instrucciones para el despliegue de TheHive](#instrucciones-para-el-despliegue-de-thehive)
3. [Post-despligue](#post-despligue)


## Pre-requisitos

1. Contar con un servidor con Ubuntu Server 18.04. Los requisitos del servidor se encuentran en el apartado "Hardware Pre-requisites
" del siguiente repositorio: 
   [Repositorio con los requisitos de hardware](https://github.com/TheHive-Project/TheHiveDocs)

2. Agregar clave SSH publica del dispositivo desde el cual se realiza el despliegue sobre el servidor objetivo y usuario creado en el paso anterior.
(No agregar claves SSH  sobre el usuario ROOT del servidor donde se realizara el despliegue).


## Instrucciones para el despliegue de TheHive


*  Agregar nombre de usuario del servidor `host` en el grupo `thehive` (Ej. user thehiveuser):

    ```
        [thehive]
        thehiveuser
    ```
    
* En la carpeta `host_vars` agregar un archivo .yml que tiene la forma del archivo `template_thehive.yml`, renombrar de la forma `nombre_usuario.yml`
(Ej. thehiveuser.yml) y modificar las variables de configuracion para la instalacion de TheHive.


Dentro del archivo `template_thehive.yml` tenemos las siguientes variables:


- `ansible_host` y `ansible_user` corresponden a la IP y Username del host objetivo (el Master Node).

    ```yaml
    ansible_host: '172.16.81.70'
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
5.  Activar la opcion `Reveal` sobre la `API-KEY`, la misma sera usada para el despliegue de Cortex.















