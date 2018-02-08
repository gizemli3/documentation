# Solución de Problemas

## Verificar Registros

Para detectar el problema, tiene que verificar los archivos de registro de errores.

#### Registro de errores EspoCRM 

Los resgistros de EspoCRM están ubicados en `<ESPOCRM_DIRECTORY>/logs/*.log` y contiene información del error.

#### Registros de error de Apache

Para el servidor Ubuntu hay un registro de error de apache ubicado en `/var/log/apache2/error.log` y contiene toda la información del error. La ubicación de los archivos de registro puede ser diferente en otros sistemas. 

## Habilitar el modo de depuración

Para habilitar el modo de depuración, vaya al directorio EspoCRM instalado, abra el arcivo `data/config.php` y cambie el valor:

```
'logger' => [
    ...
    'level' => 'WARNING',
    ...
]
```
a
```
'logger' => [
    ...
    'level' => 'DEBUG',
    ...
]
```

## Los trabajos programados no funcionan

#### Problema #1: Su crontab no está configurado

1. Ingrese a su servidor a través de SSH.

2. Configure su crontab siguiendo los pasos siguientes: https://www.espocrm.com/documentation/administration/server-configuration/#user-content-setup-a-crontab.

Nota: Crontab debe ser configurado bajo el usuario del servidor web, p.e. `crontab -e -u www-data`.

3. Espere un momento y verifique los Trabajos Programados para si algún trabajo fue ejecutado (ver un panel de registro).

#### Problema #2. Crontab está configurado, pero los Trabajos Programados no están funcionando

Para asegurarse que no hay errores cuando cron está ejecutándose, trate de ejecutar el comando cron en una terminal:

1. Ingrese a su servidor a través de SSH.

2. Vaya al directorio donde EspoCRM está instalado. P.e. para el directorio `/var/www/html/espocrm` el comando es:

```bash
cd /var/www/html/espocrm
```

3. Ejecute el comando crontab:

```bash
php cron.php
```

Nota: Debe ser ejecutado bajo el usuario del servidor web. Si ha iniciado sesión como root, el comando debe ser (p.e para Ubuntu):

```bash
sudo -u www-data php cron.php
```

donde `www-data` es un usuario del servidor web.

4. Si no hay errores, verifique los Trabajos Programados para ver si algún trabajo fue ejecutado (ver un panel de registro).

## EspoCRM no carga tras la actualización

Esto puede suceder a veces en algunos hostings compartidos.

Verificar permisos de los archivos:
/index.php
/api/v1/index.php

Deben ser 644. Si cualquiera de esos archivos tiene permiso 664 necesita cambiarlo a 644. Use el panel de control de su hosting o el comando chmod.

```
chmod 644 /path/to/file
```
Más información sobre permisos de archivos: [here](server-configuration.md#required-permissions-for-unix-based-systems).
