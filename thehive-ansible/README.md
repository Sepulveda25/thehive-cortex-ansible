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

2. Agregar clave SSH publica del host desde el cual se realiza el despliegue en el servidor donde se pretende instalar TheHive, para hacer esto se puede copiar manualmente la public key del host en el archivo autorized_keys de la carpeta /home/THEHIVEUSER/.ssh o con el comando: ssh-copy-id THEHIVEUSER@THEHIVEIP (tambien ejecutado desde el host).


## Instrucciones para el despliegue de TheHive


    
`[IMPORTANTE]` Cuando se ejecute el comando para el despliegue del Ansible se le solicitara el pass de SUDO (BECOME_PASSWORD o SUDO_PASSWORD) para el usuario del servidor donde se pretende instalar TheHive, en este caso tenemos tres alternativas:
1. Ingresar el password en caso de conocerlo.
2. Si el usuario es root presionar enter y no ingresar nada (presionar enter).
3. O en caso de no cumplirse ninguna de las opciones anteriores se le debe permitir ejecutar sudo sin solicitar la contraseña, esto se hace agregando una entrada al archivo sudoers (sudo visudo), la entrada es: THEHIVEUSER ALL=(ALL) NOPASSWD: ALL (lo mismo se puede realizar creando un archivo temporal en /etc/sudoers.d/temporal_THEHIVEUSER y agregando la misma linea). En este caso no se debe ingresar contraseña (presionar enter). 

*  Agregar nombre de usuario del servidor `host` en el grupo `thehive` (Ej. user thehiveuser):

```
[thehive]
thehiveuser
```
    
* En la carpeta `host_vars` agregar un archivo .yml que tiene la forma del archivo `template_thehive.yml`, renombrar de la forma `nombre_usuario.yml`
(Ej. thehiveuser.yml) y modificar las variables de configuracion para la instalacion de TheHive.


 Dentro del archivo `template_thehive.yml` tenemos las siguientes variables:  `ansible_host` y `ansible_user` corresponden a la IP y Username del host objetivo (el User del host donde se pretende instalar TheHive):
 
```yaml
ansible_host: '172.16.81.70'
ansible_user: 'thehive'
```

*   Ejecutar ansible sobre el servidor `"thehiveuser"` (el username se define en la opcion extra_var):

```bash
ansible-playbook -i hosts -l thehive setup.yml --extra-var "target=thehiveuser" --ask-become-pass
```

## Post-despligue

1.  Ingresar desde el navegador a: `ipserverthehive:9000`
2.  Activar opcion `"Actualizar base de datos"`.
3.  Crear usuario `ADMIN`.
4.  Una vez creado el usuario administrador, crear una cuenta nueva para usuarios no administradores.
5.  Luego crear una `API-KEY` para el usuario no administrador en `Users` (Barra superior derecha en la lista deplegable "ADMIN").
6.  Activar la opcion `Reveal` sobre la `API-KEY`, la misma sera usada para el despliegue de Cortex.















