# Administración de servicios

Una vez instalado un servicio, debemos configurarlo para que el servicio esté activo cada vez que se reinicia el servidor, además debemos poder reiniciar, detener o iniciar el servicio.

Para esta tarea se usa el comando:
```
systemctl
```

## Activando un servicio (Se inicia el servidor)
```
systemctl enable xxx.service
```

## Deshabilitando un servicio
```
systemctl disable xxx.service
```

## Iniciando un servicios
```
systemctl start xxxx.service
```

## Reiniciando un servicio

```
systemctl restart xxx. service
```

## Obteniendo el estado de un servicio
```
systemctl status xxxx.service
```

donde `xxxxx` es el nombre del servicio.s

### Actividad

Instalar y configurar los siguientes servicios

`postgresql`

`mysql`

Tiempo:15min.

```bash
[root@oromion ~]# postgresql-setup initdb
$ start postgresql.service

```

## Administración de usuarios

La definición de usuarios se realiza agregando una línea a los archivos `/etc/passwd` y `/etc/shadow`. El primer archivo mantiene las propiedades del archivo y el segundo la contraseña.

### Formato del archivo `passwd`

```
usuario:clave:uid:gid:comentarios:directorio hogar: programa de inicio
```
La modificación directa de este archivo no es recomendable, ya que la alteración de su formato haría imposible el ingreso de cualquier usuario al sistema.

La creación de usuarios se realiza con el comando `adduser` o `useradd` (son idénticos en CentOS).

Luego de la creación del usuario se le debe asignar una contraseña con el comando `passwd`.

```
adduser
```

Opciones:


Clave del root, sudoers
