# Ansible para la instalacion de TheHive

[Ir a documento raiz](https://gitlab.unc.edu.ar/csirt/csirt-docs/tree/master#csirt-docs)

[Ir a Ansible para la instalacion de Cortex](https://gitlab.unc.edu.ar/csirt/thehive-cortex-ansible/tree/master/cortex-ansible#ansible-para-la-instalacion-de-cortex)

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


 Dentro del archivo `template_thehive.yml` tenemos las siguientes variables:  `ansible_host` y `ansible_user` corresponden a la IP y Username del host objetivo (el Master Node):
 
```yaml
ansible_host: '172.16.81.70'
ansible_user: 'thehive'
```

*   Ejecutar ansible sobre el servidor `"thehiveuser"` (el username se define en la opcion extra_var):

```bash
ansible-playbook -i hosts -l thehive setup.yml --extra-var "target=thehiveuser" --ask-become-pass
```

`[IMPORTANTE]` Cuando se ejecute el comando anterior se va a pedir una contraseña de usuario contra el que se realiza el despliegue (ansible_user). En caso de ser root solo presionar enter.

## Post-despligue

1.  Ingresar desde el navegador a: `ipserverthehive:9000`
2.  Activar opcion `"Actualizar base de datos"`.
3.  Crear usuario `ADMIN`.
4.  Una vez creado el usuario administrador, crear una cuenta nueva para usuarios no administradores.
5.  Luego crear una `API-KEY` para el usuario no administrador en `Users` (Barra superior derecha en la lista deplegable "ADMIN").
6.  Activar la opcion `Reveal` sobre la `API-KEY`, la misma sera usada para el despliegue de Cortex.















