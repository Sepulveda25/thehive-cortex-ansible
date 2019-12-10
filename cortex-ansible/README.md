# Ansible para la instalacion de Cortex

## Tabla de contenidos

1. [Pre-requisitos](#pre-requisitos)
2. [Instrucciones para el despliegue de Cortex](#instrucciones-para-el-despliegue-de-cortex)
3. [Post-despligue](#post-despligue)



## Pre-requisitos

1. Contar con un servidor con Ubuntu Server 18.04. Los requisitos del servidor se encuentran en el apartado "Hardware Pre-requisites
" del siguiente repositorio:  [Repositorio con los requisitos de hardware](https://github.com/TheHive-Project/TheHiveDocs)

2. Agregar clave SSH publica del dispositivo desde el cual se realiza el despliegue sobre el servidor objetivo y usuario creado en el paso anterior.
(No agregar claves SSH  sobre el usuario ROOT del servidor donde se realizara el despliegue).

3. [Saltear por ahora] Mantener actualizada la carpeta `roles/cortex_analyzers/files/my_analyzers` con los Analyzers desarollados.

3. Mantener actualizada la carpeta `roles/cortex_responders/files/my_responders` con los Responders desarollados, los mismos se pueden descargar del repositorio:  
[Repositorio con los Responders creados](https://gitlab.unc.edu.ar/csirt/thehive-cortex-responders)



## Instrucciones para el despliegue de Cortex


*  Agregar nombre de usuario del servidor `host` en el grupo `cortex` (Ej. user thehiveuser):

```yaml
    [cortex]
    thehiveuser
```
    
    
* En la carpeta `host_vars` agregar un archivo .yml que tiene la forma del archivo `template_cortex.yml`, renombrar de la forma `nombre_usuario.yml`
(Ej. thehiveuser.yml) y modificar las variables de configuracion para la instalacion de Cortex.


 Dentro del archivo `template_cortex.yml` tenemos las siguientes variables:  
 
  1. `ansible_host` y  `ansible_user` corresponden a la IP y Username del host objetivo:
  2. `path_default_analyzers_and_responders` se corresponde con el path donde se almacenaran los Analyzers y Responder por defecto que se descargan automaticamente del repositorio: 
  [Repositorio con los Analyzers y Responder por defecto](https://github.com/TheHive-Project/Cortex-Analyzers)
  3. `path_my_own_analyzers` es el path donde se copian los Analyzers propios almacenados en la carpeta `roles/cortex_analyzers/files/my_analyzers`
  4. `path_my_own_responders` es el path donde se copian los Responders propios almacenados en la carpeta `roles/cortex_responders/files/my_responders`
  5. Las variables `parallelism_min_analyzers`, `parallelism_factor_analyzers` y `parallelism_max_analyzers` tienen que ver con cuestiones de rendimiento de los Analyzers, 
  recomendamos dejar las mismas en los valores por defecto, en caso de querer modificarlas consultar la documentacion de Cortex. 
  6. Las variables `parallelism_min_responders`, `parallelism_factor_responders` y `parallelism_max_responders` tienen que ver con cuestiones de rendimiento de los Analyzers, 
  recomendamos dejar las mismas en los valores por defecto, en caso de querer modificarlas consultar la documentacion de Cortex. 

```yaml
    ansible_host: '172.16.81.70'
    ansible_user: 'thehive'
    
    path_default_analyzers_and_responders: "/opt/Cortex-Analyzers"

    path_my_own_analyzers: " "
    
    parallelism_min_analyzers: 2 #default 2
    parallelism_factor_analyzers: 2.0  #default 2.0
    parallelism_max_analyzers: 4 #default 4
    
    path_my_own_responders: " "
    
    parallelism_min_responders: 2 #default 2
    parallelism_factor_responders: 2.0  #default 2.0
    parallelism_max_responders: 4 #default 4

```

*   Ejecutar ansible sobre el servidor `"thehiveuser"` (el username se define en la opcion extra_var):

```bash
  ansible-playbook -i hosts -l cortex setup.yml --extra-var "target=thehiveuser" --ask-become-pass
```

## Post-despligue
Despues del despliegue de cortex seguir la siguiente guia:

[Guía de inico rápido](https://gitlab.unc.edu.ar/csirt/csirt-docs/blob/master/gestion-de-incidentes/incidentes-install-guide.md#gu%C3%ADa-de-inicio-r%C3%A1pido)




