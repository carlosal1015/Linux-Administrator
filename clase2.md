# Sesión 2 #

## El Sistema de Archivos de Linux FHS. Editores de texto ##

Fecha: Sábado 3 de febrero del 2018.
Profesor: Luis Carrera

### Sistema de archivos ###

> Es la parte del sistema operativo encargada del almacenamiento y recuperación de los datos de un medio físico (cintas, discos duros, discos portátiles, cds, etc).

#### Archivo ####

> Secuencia de bits o cadena de bits.

La definición de archivo en Unix no contempla análisis ni reconocimiento del contenido, es por eso, que en **UNIX** no existe el concepto de extensión en el nombre del archivo.


#### Nombre del archivo ####

> Secuencia de caracteres alfanuméricos que sirve como identificador del archivo para el usuario.

#### i - nodo ####

Estructura de datos que almacena las propiedades del archivo, esta estructura se identifica con un `#` proporcionado por el sistema y es la única forma como el SA reconoce el archivo.

#### Propiedades almacenadas en el `i-nodo` ####

	tipo de archivo
	Al usar el comando
	permisos del archivo
	uid del dueño del archivo
	gid del grupo principal del dueño
	tamaño en bytes
	fecha y hora de última actualización
	fecha y hora de última modificación
	fecha y hora de creación
	lista de blocks

#### Enlace ####

Relación entre el i-nodo y el nombre del archivo.

#### Tipos de archivos ####

#### Archivo regular (-) #####

Archivo que contiene cualquier flujo de bits.

#### Directorio (d) ####

Archivo que contiene enlaces, al crear un directorio, este ya tiene dos enlaces almacenados, el enlace `.` y el enlace `..` que identifican los i-nodos del directorio actual y el directorio padre respectivamente.
El comando que crea directorios es el comando `mkdir` (make directory)

#### Enlace (l) ####

Enlace simbólico, es un tipo de archivo que almacena un "puntero" hacia otro archivo, es útil para poder crear referencias a directorios y a archivos que se encuentran en otra partición. El comando que crea enlaces simbólicos es el comando `ln`.

### Archivos de dispositivos ###

##### Dispositivo de bloques (b) ####

Utiliza un área de memoria intermedia (buffer) para comunicarse con el SO, la comunicación se realiza en unidades de buffer.

#### Dispositivo de caracteres ####

Se comunica con el SO enviando serie de caracteres (caracter por caracter).

### Archivos de comunicación entre procesos ####

### Tubería con nombre (p) ###

Permite la comunicación entre procesos de manera asíncrona, no se ejecutan en simultáneo. El primer proceso almacena la información en la tubería, esta información se mantiene en la tubería hasta que el segundo proceso la extrae, quedando entonces la tubería vacía.

#### Sockets (s) ####

Permite la comunicación entre procesos de manera asíncrona, los sockets se crean utilizando librerías de programación.

* Enlaces:

nombreArchivo --> #i-nodo
					 ^
nombreArchivo2------>|

Salida del comando ls

	-rw-rw-r--, 2 lcarrera lcarrera 1153 feb 3 10:59 enero
	|	  |		|		|		|	  |		 |			|
tipo de   |		|		|	  grupo	  |		 |			--nombre
archivo   |		#		dueño		  |		última
	cadena de  enlaces 				  |		modificación
	permisos						enlaces


## Comandos del sistema de archivos ##

- ls (list)

> Lista el contenido del directorio
Opciones:

- -l Lista propiedades
- -i Lista i-nodos
- -a Muestra los archivos ocultos (su nombre inicia con .)
- -R Inicia un listado recursuivo

- mkdir (make directory)

> Crea un directorio
Opciones

- -p Crea los subdirectorios faltantes

rmdir (remove directory)

Elimina un directorio, siempre y cuando esté vacío.

Opciones
-r Elimina el directorio y los subdirectorios, aún si no están vacíos.

rm (remove)

Elimina un archivo
Opciones:
-r Ejecuta un borrado recursivo (si dentro de la lista de archivos a borrar hay un directorio) Ingresa al directorio y borra los archivos.

cp (copy)

Sintaxis:
cp origen destino
Copia el archivo de origen como el archivo destino.
Opciones
-r Inicia una copia recursiva

mv (move)

Sintáxis:
mv origen destino
Mueve un archivo de una ubicación a otra

pwd (print work directory)

Indica la ruta actual

cd (change directory)

Cambia de directorio



Árbol de directorios

El sistema de archivo está organizado en una estructura de árbol invertido, siendo la raíz el directorio padre identificado por el símbolo / debajo del cual existe un conjunto de directorios con un uso específico.

					/ raíz (root)
					|
					|
-----------------------------------------------------------------------
|		|	|	|		|		|		|		|		|
|		|	|	|		|		|		|		|		|
|		|	|	|		|		|		|		|		|
|		|	|	|		|		|		|		|		|
/boot/etc/dev/bin/sbin/home/tmp/usr/var/proc/opt

Usos:

	boot
		Contiene los archivos necesarios para iniciar el SO.
	etc
		Contiene los archivos de configuración del sistema y los servicios.
	dev
		Contiene la representación como archivos de los dispositivos.
	bin
		Contiene los ejecutables básicos del usuario. (aplicaciones)
	sbin
		Contiene los ejecutables básicos de administración
	home
		Contiene los directorios hogar de los usuarios. Cada vez se crea el usuario, el sistema le crea un directorio.
	tmp
		Contiene los directorios temporales del sistema
	usr
		Contiene la estructura de archivos para las aplicaciones y servicios del sistema
	var
		Contiene los archivos de registro y de ejecución de los servicios.
	proc
		Imagen del contenido de la memoria.
	opt
		Paracido a usr muy común en distribuciones como SuSe.

Esta es lo típico en sistema CentOS.

Ruta o Path

Es la secuencia de directorios que se deben recorrer desde la raíz hasta llegar al archivo.

Ruta absoluta

/directorio1/directorio2/directorio3/directorio4/...

Ruta relativa

Parte del `pwd`.

Abreviatura

		Los programas en /usr y la base de datos en /var.


		usr bin usr var
		los ejecutables
```bash
$ ls -i
$ ls -l
```

El modem puede recibir y transmitir, terminal también, disco duro.

Solo en Windows existe el reconocimiento por extensión, en Linux no existe esa diferenciación.

El sistema operativo no reconoce el archivo por nombre.

Para el sistema operativo el archivo reconoce por el nombre del  i-nodo, su nombre está en un archivo llamado directorio.

En Windows el contenido tiene significado para el usuario, en Linux el contenido del archivo no le importa al sistema operativo, no le da ninguna característica especial, solamente tiene significado cuando el sistema operativo los usa. Por ejemplo, los archivos

El enlace es el i-nodo.

Un archivo contiene los enlaces.

Cuando se cra un directorio se crean 2 enlaces . y .. (representa el directorio actual y directorio padre)

Es una lista doblemente enlazada.

Unix fue creado por programadores.

Cada partición tienen su número de i-nodos.

Enlace simbólico.

Enlace es la relación entre el i-nodo y el nombre del archivo.


```bash
[user2@luiscarrera ~]$ man ln
[user2@luiscarrera ~]$ cat enero
    enero de 2018
lu ma mi ju vi sá do
 1  2  3  4  5  6  7
 8  9 10 11 12 13 14
15 16 17 18 19 20 21
22 23 24 25 26 27 28
29 30 31
[user2@luiscarrera ~]$ ln enero mes1
[user2@luiscarrera ~]$ ls
2  ejercicios  enero  errores  github  mes1
[user2@luiscarrera ~]$ ls -i
149910 2  149897 ejercicios  149477 enero  149890 errores  274137 github  149477 mes1
[user2@luiscarrera ~]$
```
Estoy agregando un nombre más a mes1, no estoy creando otro archivo.

En Linux reconocemos el archivo no por su nombre sino con i-nodo.

La segunda columna indica el número de enlaces que tiene.


Con rm solo borro el i-nodo, no se borra el archivo.

```bash
[user2@luiscarrera ~]$ ls -l
total 20
-rw-rw-r--. 1 user2 user2    0 ene 27 20:27 2
drwxrwxr-x. 2 user2 user2 4096 ene 27 19:42 ejercicios
-rw-rw-r--. 2 user2 user2 1123 feb  3 10:59 enero
-rw-rw-r--. 1 user2 user2   72 ene 27 18:50 errores
drwxrwxr-x. 3 user2 user2 4096 ene 27 17:59 github
-rw-rw-r--. 2 user2 user2 1123 feb  3 10:59 mes1
[user2@luiscarrera ~]$ ls
2  ejercicios  enero  errores  github  mes1
[user2@luiscarrera ~]$ rm enero
[user2@luiscarrera ~]$ ls
2  ejercicios  errores  github  mes1
[user2@luiscarrera ~]$ cat mes1
    enero de 2018
lu ma mi ju vi sá do
 1  2  3  4  5  6  7
 8  9 10 11 12 13 14
15 16 17 18 19 20 21
22 23 24 25 26 27 28
29 30 31

 10:59:11 up  1:20, 12 users,  load average: 1,70, 1,00, 0,46
USER     TTY      FROM              LOGIN@   IDLE   JCPU   PCPU WHAT
root     tty1     :0               09:41    1:20m  3:15   3:15  /usr/bin/Xorg :
root     pts/0    :0.0             09:41    1:09m  2:38   2:38  /usr/bin/python
root     pts/1    :0.0             09:49   58:21   0.06s  0.06s bash
root     pts/2    :0.0             10:01    4.00s  0.20s  0.04s -bash
user4    pts/3    172.17.3.252     10:04   17.00s  0.07s  0.07s -bash
user2    pts/4    172.17.2.219     10:14    0.00s  0.07s  0.01s w
user1    pts/5    172.17.2.217     10:14    3.00s  0.04s  0.04s -bash
user11   pts/6    172.17.2.216     10:16    3:22   0.03s  0.03s -bash
user3    pts/7    172.17.3.220     10:29   24.00s  0.03s  0.03s -bash
user5    pts/8    172.17.2.223     10:34    2:06   0.04s  0.04s -bash
user8    pts/9    172.17.2.227     10:57    1:40   0.00s  0.00s -bash
user11   pts/10   172.17.2.216     10:57    1:21   0.02s  0.02s -bash

[user2@luiscarrera ~]$ which httpd
/usr/sbin/httpd
[user2@luiscarrera ~]$ which postfix
/usr/sbin/postfix
[user2@luiscarrera ~]$ which tomcat
/usr/bin/which: no tomcat in (/usr/lib64/qt-3.3/bin:/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/sbin:/home/user2/bin)
[user2@luiscarrera ~]$ which glasfish
/usr/bin/which: no glasfish in (/usr/lib64/qt-3.3/bin:/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/sbin:/home/user2/bin)
[user2@luiscarrera ~]$ which java
/usr/bin/java
[user2@luiscarrera ~]$ which javac
/usr/bin/javac
[user2@luiscarrera ~]$ cat /etc/r
cat: /etc/r: No existe el fichero o el directorio
[user2@luiscarrera ~]$ cat /etc/redhat-release
CentOS release 6.9 (Final)
[user2@luiscarrera ~]$ pwd
/home/user2
[user2@luiscarrera ~]$ cat /etc//passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
uucp:x:10:14:uucp:/var/spool/uucp:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
games:x:12:100:games:/usr/games:/sbin/nologin
gopher:x:13:30:gopher:/var/gopher:/sbin/nologin
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
nobody:x:99:99:Nobody:/:/sbin/nologin
dbus:x:81:81:System message bus:/:/sbin/nologin
rpc:x:32:32:Rpcbind Daemon:/var/cache/rpcbind:/sbin/nologin
usbmuxd:x:113:113:usbmuxd user:/:/sbin/nologin
abrt:x:173:173::/etc/abrt:/sbin/nologin
pegasus:x:66:65:tog-pegasus OpenPegasus WBEM/CIM services:/var/lib/Pegasus:/sbin/nologin
cimsrvr:x:134:134:tog-pegasus OpenPegasus WBEM/CIM services:/var/lib/Pegasus:/sbin/nologin
hsqldb:x:96:96::/var/lib/hsqldb:/sbin/nologin
oprofile:x:16:16:Special user account to be used by OProfile:/home/oprofile:/sbin/nologin
vcsa:x:69:69:virtual console memory owner:/dev:/sbin/nologin
rtkit:x:499:497:RealtimeKit:/proc:/sbin/nologin
avahi-autoipd:x:170:170:Avahi IPv4LL Stack:/var/lib/avahi-autoipd:/sbin/nologin
apache:x:48:48:Apache:/var/www:/sbin/nologin
saslauth:x:498:76:"Saslauthd user":/var/empty/saslauth:/sbin/nologin
postfix:x:89:89::/var/spool/postfix:/sbin/nologin
rpcuser:x:29:29:RPC Service User:/var/lib/nfs:/sbin/nologin
nfsnobody:x:65534:65534:Anonymous NFS User:/var/lib/nfs:/sbin/nologin
haldaemon:x:68:68:HAL daemon:/:/sbin/nologin
gdm:x:42:42::/var/lib/gdm:/sbin/nologin
tomcat:x:91:91:Apache Tomcat:/usr/share/tomcat6:/sbin/nologin
mysql:x:27:27:MySQL Server:/var/lib/mysql:/bin/bash
ntp:x:38:38::/etc/ntp:/sbin/nologin
amandabackup:x:33:6:Amanda user:/var/lib/amanda:/bin/bash
memcached:x:497:495:Memcached daemon:/var/run/memcached:/sbin/nologin
pulse:x:496:494:PulseAudio System Daemon:/var/run/pulse:/sbin/nologin
webalizer:x:67:67:Webalizer:/var/www/usage:/sbin/nologin
sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
postgres:x:26:26:PostgreSQL Server:/var/lib/pgsql:/bin/bash
dovecot:x:97:97:Dovecot IMAP server:/usr/libexec/dovecot:/sbin/nologin
dovenull:x:495:491:Dovecot's unauthorized user:/usr/libexec/dovecot:/sbin/nologin
tcpdump:x:72:72::/:/sbin/nologin
Alumno:x:500:500::/home/Alumno:/bin/bash
lcarrera:x:501:501::/home/lcarrera:/bin/bash
user1:x:502:502::/home/user1:/bin/bash
user2:x:503:503::/home/user2:/bin/bash
user3:x:504:504::/home/user3:/bin/bash
user4:x:505:505::/home/user4:/bin/bash
user5:x:506:506::/home/user5:/bin/bash
user6:x:507:507::/home/user6:/bin/bash
user7:x:508:508::/home/user7:/bin/bash
user8:x:509:509::/home/user8:/bin/bash
user9:x:510:510::/home/user9:/bin/bash
user10:x:511:511::/home/user10:/bin/bash
user11:x:512:512::/home/user11:/bin/bash
unbound:x:494:489:Unbound DNS resolver:/etc/unbound:/sbin/nologin
[user2@luiscarrera ~]$ cat /etc/sys
cat: /etc/sys: No existe el fichero o el directorio
[user2@luiscarrera ~]$ cat /etc/sysconfig/
cat: /etc/sysconfig/: Es un directorio
[user2@luiscarrera ~]$ cat /etc/sysconfig/
acpid                       crond                       ip6tables                   keyboard                    nspluginwrapper             rsyslog                     sysstat
atd                         dirsrv                      ip6tables-config            krb5kdc                     ntpd                        samba                       sysstat.ioconf
auditd                      dovecot                     ip6tables.old               libvirt-guests              ntpdate                     sandbox                     system-config-firewall
authconfig                  firstboot                   ipa_memcached               mcelogd                     pgsql/                      saslauthd                   system-config-firewall.old
autofs                      grub                        iptables                    memcached                   pluto                       sa-update                   system-config-users
cbq/                        hostapd                     iptables-config             modules/                    prelink                     selinux                     tgtd
cgconfig                    hsqldb                      iptables.old                netconsole                  quota_nld                   smartmontools               tomcat6
cgred.conf                  htcacheclean                irqbalance                  network                     raid-check                  snmpd                       udev
clock                       httpd                       kadmin                      networking/                 readahead                   snmptrapd                   wpa_supplicant
console/                    i18n                        kdump                       network-scripts/            readonly-root               spamassassin                xinetd
cpuspeed                    init                        kernel                      nfs                         rngd                        sshd
[user2@luiscarrera ~]$ cat /etc/sysconfig/
[user2@luiscarrera ~]$ cat /etc/sysconfig/cd
cat: /etc/sysconfig/cd: No existe el fichero o el directorio
[user2@luiscarrera ~]$
[user2@luiscarrera ~]$ mkdir Linux
[user2@luiscarrera ~]$ ls -l
total 20
-rw-rw-r--. 1 user2 user2    0 ene 27 20:27 2
drwxrwxr-x. 2 user2 user2 4096 ene 27 19:42 ejercicios
-rw-rw-r--. 1 user2 user2   72 ene 27 18:50 errores
drwxrwxr-x. 3 user2 user2 4096 ene 27 17:59 github
drwxrwxr-x. 2 user2 user2 4096 feb  3 11:36 Linux
-rw-rw-r--. 1 user2 user2 1123 feb  3 10:59 mes1
[user2@luiscarrera ~]$ rmdir Linux/
[user2@luiscarrera ~]$ ls
2  ejercicios  errores  github  mes1
[user2@luiscarrera ~]$ mkdir -p Linux/CentOS/clase1
[user2@luiscarrera ~]$ ls -l
total 20
-rw-rw-r--. 1 user2 user2    0 ene 27 20:27 2
drwxrwxr-x. 2 user2 user2 4096 ene 27 19:42 ejercicios
-rw-rw-r--. 1 user2 user2   72 ene 27 18:50 errores
drwxrwxr-x. 3 user2 user2 4096 ene 27 17:59 github
drwxrwxr-x. 3 user2 user2 4096 feb  3 11:36 Linux
-rw-rw-r--. 1 user2 user2 1123 feb  3 10:59 mes1
[user2@luiscarrera ~]$ ls -l Linux/
total 4
drwxrwxr-x. 3 user2 user2 4096 feb  3 11:36 CentOS
[user2@luiscarrera ~]$ ls -l Linux/CentOS/
total 4
drwxrwxr-x. 2 user2 user2 4096 feb  3 11:36 clase1
[user2@luiscarrera ~]$
[user2@luiscarrera ~]$ ls
2  ejercicios  errores  github  Linux  mes1
[user2@luiscarrera ~]$ ls -l Linux/
total 4
drwxrwxr-x. 3 user2 user2 4096 feb  3 11:36 CentOS
[user2@luiscarrera ~]$ ls -l /home/user2/Linux/
total 4
drwxrwxr-x. 3 user2 user2 4096 feb  3 11:36 CentOS
[user2@luiscarrera ~]$
[user2@luiscarrera ~]$ ls -l ./Linux/
total 4
drwxrwxr-x. 3 user2 user2 4096 feb  3 11:36 CentOS
[user2@luiscarrera ~]$
[user2@luiscarrera ~]$ cp ../../etc/passwd .
[user2@luiscarrera ~]$ ls
2  ejercicios  errores  github  Linux  mes1  passwd
[user2@luiscarrera ~]$ cp /etc/passwd .
[user2@luiscarrera ~]$ ñs
-bash: ñs: no se encontró la orden
[user2@luiscarrera ~]$ ls
2  ejercicios  errores  github  Linux  mes1  passwd
[user2@luiscarrera ~]$
[user2@luiscarrera ~]$ pwd
/home/user2
[user2@luiscarrera ~]$ ls
2  CLASE1.txt  ejercicios  errores  github  Linux  mes1  passwd
[user2@luiscarrera ~]$ cd Linux/CentOS/
[user2@luiscarrera CentOS]$ pwd
/home/user2/Linux/CentOS
[user2@luiscarrera CentOS]$ ls -l
total 4
drwxrwxr-x. 2 user2 user2 4096 feb  3 11:36 clase1
[user2@luiscarrera CentOS]$ mkdir clase[2]
[user2@luiscarrera CentOS]$ rmdir class\{2\}/
rmdir: failed to remove «class{2}/»: No existe el fichero o el directorio
[user2@luiscarrera CentOS]$ ls
clase1  clase[2]
[user2@luiscarrera CentOS]$ rmdir clase\{2\}/
rmdir: failed to remove «clase{2}/»: No existe el fichero o el directorio
[user2@luiscarrera CentOS]$ ls
clase1  clase[2]
[user2@luiscarrera CentOS]$ mkdir clase2
[user2@luiscarrera CentOS]$ mkdir clase3
[user2@luiscarrera CentOS]$ mkdir clase4
[user2@luiscarrera CentOS]$
[user2@luiscarrera CentOS]$ ls
clase1  clase2  clase[2]  clase3  clase4
[user2@luiscarrera CentOS]$ mkdir /home/user2/Examenes
[user2@luiscarrera CentOS]$ pwd
/home/user2/Linux/CentOS
[user2@luiscarrera CentOS]$ cd
[user2@luiscarrera ~]$ pwd
/home/user2
[user2@luiscarrera ~]$ yum install tree
Complementos cargados:fastestmirror, refresh-packagekit, security
Necesita ser usuario root para poder ejecutar este comando.
[user2@luiscarrera ~]$ tree
.
├── 2
├── CLASE1.txt
├── ejercicios
├── errores
├── Examenes
├── github
│   └── hola.tex
├── Linux
│   └── CentOS
│       ├── clase1
│       ├── clase2
│       ├── clase[2]
│       ├── clase3
│       └── clase4
├── mes1
└── passwd

10 directories, 6 files
[user2@luiscarrera ~]$ tree Linux/
Linux/
└── CentOS
    ├── clase1
    ├── clase2
    ├── clase[2]
    ├── clase3
    └── clase4

6 directories, 0 files
[user2@luiscarrera ~]$ man mkdir
[user2@luiscarrera ~]$ mkdir Cursos
[user2@luiscarrera ~]$ mv Linux/ C
CLASE1.txt  Cursos/
[user2@luiscarrera ~]$ mv Linux/ Cursos/
[user2@luiscarrera ~]$ tree C
CLASE1.txt  Cursos/
[user2@luiscarrera ~]$ tree Cursos/
Cursos/
└── Linux
    └── CentOS
        ├── clase1
        ├── clase2
        ├── clase[2]
        ├── clase3
        └── clase4

7 directories, 0 files

```

El enlace tiene el mismo i-nodo, el enlace simbólico es un enlace directo como en Windows.

```sh
 ln -s Cursos Clases
[user2@luiscarrera ~]$ ls -l
total 44
-rw-rw-r--. 1 user2    user2        0 ene 27 20:27 2
-rw-r--r--. 9 lcarrera lcarrera 14232 feb  3 12:03 CLASE1.txt
lrwxrwxrwx. 1 user2    user2        6 feb  3 12:16 Clases -> Cursos
drwxrwxr-x. 3 user2    user2     4096 feb  3 12:09 Cursos
drwxrwxr-x. 2 user2    user2     4096 ene 27 19:42 ejercicios
-rw-rw-r--. 1 user2    user2       72 ene 27 18:50 errores
-rw-rw-r--. 1 user2    user2        0 feb  3 12:14 examen
drwxrwxr-x. 2 user2    user2     4096 feb  3 12:06 Examenes
drwxrwxr-x. 3 user2    user2     4096 ene 27 17:59 github
-rw-rw-r--. 1 user2    user2     1123 feb  3 10:59 mes1
-rw-r--r--. 1 user2    user2     2991 feb  3 11:42 passwd
[user2@luiscarrera ~]$ ls Clases/
Linux
[user2@luiscarrera ~]$ tree Clases/
Clases/
└── Linux

1 directory, 0 files
[user2@luiscarrera ~]$
```

Con cat tuberia se extrae el contenido.

Sistemas de archivos 2

Los dispositivos de almacenamiento se nombran de la siguiente forma:

IDE
	hda Primer dispositivo, primer bus.
	hdb Segundo dispositivo, segundo bus.
	hdc Primer dispositivo, segundo bus.
	hdd Segundo dispostivo, segundo bus.

Seriales scsci, sata
	sda Primer dispositivo
	sdb Segundo dispositivo
	sdc Tercer dispositivo
	sdd Cuarto dispositivo
	sde Quinto dispositivo
	sdf Sexto dispositivo

Las particiones se nombran numerándolas desde 1 en adelante, generalmente de 1 a 4 son particiones principales, de allí en adelante son particiones secundarias.

En Windows la primera partición es C, D y más. EN UNIX no existe el concepto de partición.

Para poder almacenar el árbol de directorios en las particiones se realiza el proceso de "montaje", en el cual un directorio del árbol es montado en una partición del disco duro. El directorio se conoce como punto de montaje.

Comandos relacionados:

mount
	Visualiza los montajes realizados.
	Realiza nuevos montajes
umount
	Desmonta los directorios de la partición.
fdisk
	Permite ver las particiones del disco duro.
df (disk free)
	Muestra los puntos de montaje, la partición y el uso de espacio.

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
Hay que particionar, darle formato y enlazar. Primero se crea un punto de montaje.

Instalar ntfs, mkdir win1 crear montaje
mount /dev/sda5 win1/
recibe la partición y el punto de montaje.

Solo lo puede realizar el superusuario.

Se prefiere que para cada partición exista otro punto de montaje.
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

Cadena de Permisos (Sistema de Seguridad del sistema de archivos)

La seguridad del sistema de archivos identifica tres usuarios:

	Owner Dueño Usuario que creó el archivo.
	Group Grupo Usuario que pertenece al grupo del archivo
	Other Otro Usuario que no es el dueño y no pertenece al grupo del archivo.

Cada archivo establece tres permisos por cada tipo de usuario:
	read lectura r
	write escritura w
	Execution Ejecución x
Se define entonces la cadena de permisos como la secuencia de caracteres que expresa los permisos de cada usuario sobre el archivo de la siguiente forma:

			rwxrwxrwx
		 	|	|  |
		 	|	|  |
Dueño-------|	|  |----- Otros
			  grupo

La aparición de la letra que identifica el permiso en la cadena de permisos indica que el usuario tiene el permiso indica si aparece un guion, el usuario no tiene dicho permiso.

Cada vez que un usuario intenta acceder a un archivo se realiza la siguiente comprobación:

1. El usuario que accede tiene el uid=0?
	Si -> Obtiene todos los permisos
	No ->
2. El uid del archivo es igual al uid del usuario?
	Si -> Obtiene los permisos del dueño
3. El gid del archivo es igual al unos de los gid del usuario?
	Si -> Obtiene los permisos del grupo
4. Obtiene los permisos de otros

Al obtener una equivalencia se detienen las comprobaciones.

Equivalente numérico de la cadena de permisos

	r w x #
	0 0 0 0
	0 0 1 1
	0 1 0 2
	0 1 1 3
	1 0 0 4
	1 0 1 5
	1 1 0 6
	1 1 1 7

Umask (Máscara del usuario)

La máscara del usuario es el mecanismo mediante el cual se asignan los permisos a los elementos del sistema de archivos recién creados.

Todos los permisos 			r w x r w x r w x 										7 7 7
Máscara del usuarios 		- - - r w x r w x 										0 7 7
--------------------------------------------- 										-----
							r w x - - - - - -	Permisos de Directorios 			7 0 0
							- - x - - - - - -	Se elimina el permiso de ejecución 	1 0 0
--------------------------------------------- 										-----
							r w - - - - - - -	Permisos de archivos 				6 0 0


Solo de a los de orden impar se les resta 1.


El sistema asumen que el usuario nunca va a crear archivos ejecutables.

Un usuario puede pertenecer a varios grupos, pero el archivo tiene un solo grupo.


Comandos relacionados

chmod (change mode)
	Cambia la cadena de permisos
chgrp (change group)
	Cambia el grupo del archivo
chown (change owner)
	Cambia el dueño del archivo
umask (user mask)
	Establece los permisos de los archivos nuevos.

chmod
	Numérico
		chmod permisos archivo
	Simbólico
		chmod usuariooperacionpermiso archivos

	Usuarios 	Operación 	Permisos
	u dueño 	= Asignar 	r lectura
	g grupo 	+ agregar 	w escritura
	o otro 		- quitar 	x ejecución
	a todos

	Ejemplos:
				chmod u+x errores
				chmod u+rw errores
				chmod ugo=r errores
				chmod u=rwx,g+w,o-wx errores

No debe haber espacio.


```sh
[user2@luiscarrera ~]$ ls -l
total 48
-rw-rw-r--. 1 user2    user2        0 ene 27 20:27 2
-rw-r--r--. 9 lcarrera lcarrera 18155 feb  3 13:24 CLASE1.txt
lrwxrwxrwx. 1 user2    user2        6 feb  3 12:16 Clases -> Cursos
drwxrwxr-x. 3 user2    user2     4096 feb  3 12:09 Cursos
drwxrwxr-x. 2 user2    user2     4096 ene 27 19:42 ejercicios
-rw-rwxrw-. 1 user2    user2       72 ene 27 18:50 errores
-rw-rw-r--. 1 user2    user2        0 feb  3 12:14 examen
drwxrwxr-x. 2 user2    user2     4096 feb  3 12:06 Examenes
drwxrwxr-x. 3 user2    user2     4096 ene 27 17:59 github
-rw-rw-r--. 1 user2    user2     1123 feb  3 10:59 mes1
-rw-r--r--. 1 user2    user2     2991 feb  3 11:42 passwd
prw-rw-r--. 1 user2    user2        0 feb  3 12:19 tuberia
[user2@luiscarrera ~]$ chmod a-rwx errores
[user2@luiscarrera ~]$ ls -l
total 48
-rw-rw-r--. 1 user2    user2        0 ene 27 20:27 2
-rw-r--r--. 9 lcarrera lcarrera 18155 feb  3 13:24 CLASE1.txt
lrwxrwxrwx. 1 user2    user2        6 feb  3 12:16 Clases -> Cursos
drwxrwxr-x. 3 user2    user2     4096 feb  3 12:09 Cursos
drwxrwxr-x. 2 user2    user2     4096 ene 27 19:42 ejercicios
----------. 1 user2    user2       72 ene 27 18:50 errores
-rw-rw-r--. 1 user2    user2        0 feb  3 12:14 examen
drwxrwxr-x. 2 user2    user2     4096 feb  3 12:06 Examenes
drwxrwxr-x. 3 user2    user2     4096 ene 27 17:59 github
-rw-rw-r--. 1 user2    user2     1123 feb  3 10:59 mes1
-rw-r--r--. 1 user2    user2     2991 feb  3 11:42 passwd
prw-rw-r--. 1 user2    user2        0 feb  3 12:19 tuberia
[user2@luiscarrera ~]$ umask
0002
[user2@luiscarrera ~]$
```

en umask solo ver 002

El permiso x se pierde al crear un archivo.

```sh
[user2@luiscarrera ~]$ mkdir directorio1
[user2@luiscarrera ~]$ ls -ld directorio1/
drwxrwxr-x. 2 user2 user2 4096 feb  3 13:31 directorio1/
[user2@luiscarrera ~]$ umask 077
[user2@luiscarrera ~]$ mkdir directorio2
[user2@luiscarrera ~]$ touch archivo2
[user2@luiscarrera ~]$ ls -ld directorio2 archivo2
-rw-------. 1 user2 user2    0 feb  3 13:32 archivo2
drwx------. 2 user2 user2 4096 feb  3 13:32 directorio2
[user2@luiscarrera ~]$
[user2@luiscarrera ~]$ ls -l directorio2 archivo2
-rw-------. 1 user2 user2    0 feb  3 13:32 archivo2

directorio2:
total 0
[user2@luiscarrera ~]$
```



```
[user2@luiscarrera ~]$ ls
2  CLASE1.txt  Clases  Cursos  ejercicios  errores  examen  Examenes  github  mes1  passwd  tuberia
[user2@luiscarrera ~]$ ls -l
total 48
-rw-rw-r--. 1 user2    user2        0 ene 27 20:27 2
-rw-r--r--. 9 lcarrera lcarrera 17799 feb  3 13:11 CLASE1.txt
lrwxrwxrwx. 1 user2    user2        6 feb  3 12:16 Clases -> Cursos
drwxrwxr-x. 3 user2    user2     4096 feb  3 12:09 Cursos
drwxrwxr-x. 2 user2    user2     4096 ene 27 19:42 ejercicios
-rw-rw-r--. 1 user2    user2       72 ene 27 18:50 errores
-rw-rw-r--. 1 user2    user2        0 feb  3 12:14 examen
drwxrwxr-x. 2 user2    user2     4096 feb  3 12:06 Examenes
drwxrwxr-x. 3 user2    user2     4096 ene 27 17:59 github
-rw-rw-r--. 1 user2    user2     1123 feb  3 10:59 mes1
-rw-r--r--. 1 user2    user2     2991 feb  3 11:42 passwd
prw-rw-r--. 1 user2    user2        0 feb  3 12:19 tuberia
[user2@luiscarrera ~]$ chmod 660 errores
[user2@luiscarrera ~]$ ls -l
total 48
-rw-rw-r--. 1 user2    user2        0 ene 27 20:27 2
-rw-r--r--. 9 lcarrera lcarrera 17799 feb  3 13:11 CLASE1.txt
lrwxrwxrwx. 1 user2    user2        6 feb  3 12:16 Clases -> Cursos
drwxrwxr-x. 3 user2    user2     4096 feb  3 12:09 Cursos
drwxrwxr-x. 2 user2    user2     4096 ene 27 19:42 ejercicios
-rw-rw----. 1 user2    user2       72 ene 27 18:50 errores
-rw-rw-r--. 1 user2    user2        0 feb  3 12:14 examen
drwxrwxr-x. 2 user2    user2     4096 feb  3 12:06 Examenes
drwxrwxr-x. 3 user2    user2     4096 ene 27 17:59 github
-rw-rw-r--. 1 user2    user2     1123 feb  3 10:59 mes1
-rw-r--r--. 1 user2    user2     2991 feb  3 11:42 passwd
prw-rw-r--. 1 user2    user2        0 feb  3 12:19 tuberia
[user2@luiscarrera ~]$ ls -l errores
-rw-rw----. 1 user2 user2 72 ene 27 18:50 errores
[user2@luiscarrera ~]$ chmod 600 errores
[user2@luiscarrera ~]$ ls -l errores
-rw-------. 1 user2 user2 72 ene 27 18:50 errores
[user2@luiscarrera ~]$ ^C
[user2@luiscarrera ~]$ chmod 444 errores
[user2@luiscarrera ~]$ ls -l
total 48
-rw-rw-r--. 1 user2    user2        0 ene 27 20:27 2
-rw-r--r--. 9 lcarrera lcarrera 17799 feb  3 13:11 CLASE1.txt
lrwxrwxrwx. 1 user2    user2        6 feb  3 12:16 Clases -> Cursos
drwxrwxr-x. 3 user2    user2     4096 feb  3 12:09 Cursos
drwxrwxr-x. 2 user2    user2     4096 ene 27 19:42 ejercicios
-r--r--r--. 1 user2    user2       72 ene 27 18:50 errores
-rw-rw-r--. 1 user2    user2        0 feb  3 12:14 examen
drwxrwxr-x. 2 user2    user2     4096 feb  3 12:06 Examenes
drwxrwxr-x. 3 user2    user2     4096 ene 27 17:59 github
-rw-rw-r--. 1 user2    user2     1123 feb  3 10:59 mes1
-rw-r--r--. 1 user2    user2     2991 feb  3 11:42 passwd
prw-rw-r--. 1 user2    user2        0 feb  3 12:19 tuberia
[user2@luiscarrera ~]$
```





```sh
[user2@luiscarrera CentOS]$ mkdir /home/user2/Examenes
[user2@luiscarrera CentOS]$ pwd
/home/user2/Linux/CentOS
[user2@luiscarrera CentOS]$ cd
[user2@luiscarrera ~]$ pwd
/home/user2
[user2@luiscarrera ~]$ yum install tree
Complementos cargados:fastestmirror, refresh-packagekit, security
Necesita ser usuario root para poder ejecutar este comando.
[user2@luiscarrera ~]$ tree
.
├── 2
├── CLASE1.txt
├── ejercicios
├── errores
├── Examenes
├── github
│   └── hola.tex
├── Linux
│   └── CentOS
│       ├── clase1
│       ├── clase2
│       ├── clase[2]
│       ├── clase3
│       └── clase4
├── mes1
└── passwd

10 directories, 6 files
[user2@luiscarrera ~]$ tree Linux/
Linux/
└── CentOS
    ├── clase1
    ├── clase2
    ├── clase[2]
    ├── clase3
    └── clase4

6 directories, 0 files
[user2@luiscarrera ~]$ man mkdir
[user2@luiscarrera ~]$ mkdir Cursos
[user2@luiscarrera ~]$ mv Linux/ C
CLASE1.txt  Cursos/
[user2@luiscarrera ~]$ mv Linux/ Cursos/
[user2@luiscarrera ~]$ tree C
CLASE1.txt  Cursos/
[user2@luiscarrera ~]$ tree Cursos/
Cursos/
└── Linux
    └── CentOS
        ├── clase1
        ├── clase2
        ├── clase[2]
        ├── clase3
        └── clase4

7 directories, 0 files
[user2@luiscarrera ~]$ ^C
[user2@luiscarrera ~]$
[user2@luiscarrera ~]$ cp CLASE1.txt C
CLASE1.txt  Cursos/
[user2@luiscarrera ~]$ cp CLASE1.txt Cursos/Linux/CentOS/clase1/
[user2@luiscarrera ~]$ ls
2  CLASE1.txt  Cursos  ejercicios  errores  Examenes  github  mes1  passwd
[user2@luiscarrera ~]$ ls Cursos/Linux/CentOS/clase1/
CLASE1.txt
[user2@luiscarrera ~]$ cp CLASE1.txt Cursos/Linux/CentOS/clase1/shell.txt
[user2@luiscarrera ~]$ ls Cursos/Linux/CentOS/clase1/
CLASE1.txt  shell.txt
[user2@luiscarrera ~]$ tree Cursos/
Cursos/
└── Linux
    └── CentOS
        ├── clase1
        │   ├── CLASE1.txt
        │   └── shell.txt
        ├── clase2
        ├── clase[2]
        ├── clase3
        └── clase4

7 directories, 2 files
[user2@luiscarrera ~]$ rm Cursos/Linux/CentOS/clase1/CLASE1.txt
[user2@luiscarrera ~]$ tree Cursos/
Cursos/
└── Linux
    └── CentOS
        ├── clase1
        │   └── shell.txt
        ├── clase2
        ├── clase[2]
        ├── clase3
        └── clase4

7 directories, 1 file
[user2@luiscarrera ~]$
[user2@luiscarrera ~]$ rm -r Cursos/Linux/CentOS/
[user2@luiscarrera ~]$ tree
.
├── 2
├── CLASE1.txt
├── Cursos
│   └── Linux
├── ejercicios
├── errores
├── Examenes
├── github
│   └── hola.tex
├── mes1
└── passwd

5 directories, 6 files
[user2@luiscarrera ~]$ tree Cursos/
Cursos/
└── Linux

1 directory, 0 files
[user2@luiscarrera ~]$
[user2@luiscarrera ~]$ tree Cursos/
Cursos/
└── Linux

1 directory, 0 files
[user2@luiscarrera ~]$ touch prueba
[user2@luiscarrera ~]$ ls -l
total 44
-rw-rw-r--. 1 user2    user2        0 ene 27 20:27 2
-rw-r--r--. 9 lcarrera lcarrera 14232 feb  3 12:03 CLASE1.txt
drwxrwxr-x. 3 user2    user2     4096 feb  3 12:09 Cursos
drwxrwxr-x. 2 user2    user2     4096 ene 27 19:42 ejercicios
-rw-rw-r--. 1 user2    user2       72 ene 27 18:50 errores
drwxrwxr-x. 2 user2    user2     4096 feb  3 12:06 Examenes
drwxrwxr-x. 3 user2    user2     4096 ene 27 17:59 github
-rw-rw-r--. 1 user2    user2     1123 feb  3 10:59 mes1
-rw-r--r--. 1 user2    user2     2991 feb  3 11:42 passwd
-rw-rw-r--. 1 user2    user2        0 feb  3 12:14 prueba
[user2@luiscarrera ~]$ mv prueba examen
[user2@luiscarrera ~]$ ls
2  CLASE1.txt  Cursos  ejercicios  errores  examen  Examenes  github  mes1  passwd
[user2@luiscarrera ~]$ ln /home/lcarrera/CLASE1.txt .
ln: creating hard link «./CLASE1.txt»: El fichero ya existe
[user2@luiscarrera ~]$
[user2@luiscarrera ~]$ ls -l
total 44
-rw-rw-r--. 1 user2    user2        0 ene 27 20:27 2
-rw-r--r--. 9 lcarrera lcarrera 14232 feb  3 12:03 CLASE1.txt
drwxrwxr-x. 3 user2    user2     4096 feb  3 12:09 Cursos
drwxrwxr-x. 2 user2    user2     4096 ene 27 19:42 ejercicios
-rw-rw-r--. 1 user2    user2       72 ene 27 18:50 errores
-rw-rw-r--. 1 user2    user2        0 feb  3 12:14 examen
drwxrwxr-x. 2 user2    user2     4096 feb  3 12:06 Examenes
drwxrwxr-x. 3 user2    user2     4096 ene 27 17:59 github
-rw-rw-r--. 1 user2    user2     1123 feb  3 10:59 mes1
-rw-r--r--. 1 user2    user2     2991 feb  3 11:42 passwd
[user2@luiscarrera ~]$ ln -s Cursos Clases
[user2@luiscarrera ~]$ ls -l
total 44
-rw-rw-r--. 1 user2    user2        0 ene 27 20:27 2
-rw-r--r--. 9 lcarrera lcarrera 14232 feb  3 12:03 CLASE1.txt
lrwxrwxrwx. 1 user2    user2        6 feb  3 12:16 Clases -> Cursos
drwxrwxr-x. 3 user2    user2     4096 feb  3 12:09 Cursos
drwxrwxr-x. 2 user2    user2     4096 ene 27 19:42 ejercicios
-rw-rw-r--. 1 user2    user2       72 ene 27 18:50 errores
-rw-rw-r--. 1 user2    user2        0 feb  3 12:14 examen
drwxrwxr-x. 2 user2    user2     4096 feb  3 12:06 Examenes
drwxrwxr-x. 3 user2    user2     4096 ene 27 17:59 github
-rw-rw-r--. 1 user2    user2     1123 feb  3 10:59 mes1
-rw-r--r--. 1 user2    user2     2991 feb  3 11:42 passwd
[user2@luiscarrera ~]$ ls Clases/
Linux
[user2@luiscarrera ~]$ tree Clases/
Clases/
└── Linux

1 directory, 0 files
[user2@luiscarrera ~]$ ^C
[user2@luiscarrera ~]$ mkfifo tuberia
[user2@luiscarrera ~]$ ls -l
total 44
-rw-rw-r--. 1 user2    user2        0 ene 27 20:27 2
-rw-r--r--. 9 lcarrera lcarrera 14232 feb  3 12:03 CLASE1.txt
lrwxrwxrwx. 1 user2    user2        6 feb  3 12:16 Clases -> Cursos
drwxrwxr-x. 3 user2    user2     4096 feb  3 12:09 Cursos
drwxrwxr-x. 2 user2    user2     4096 ene 27 19:42 ejercicios
-rw-rw-r--. 1 user2    user2       72 ene 27 18:50 errores
-rw-rw-r--. 1 user2    user2        0 feb  3 12:14 examen
drwxrwxr-x. 2 user2    user2     4096 feb  3 12:06 Examenes
drwxrwxr-x. 3 user2    user2     4096 ene 27 17:59 github
-rw-rw-r--. 1 user2    user2     1123 feb  3 10:59 mes1
-rw-r--r--. 1 user2    user2     2991 feb  3 11:42 passwd
prw-rw-r--. 1 user2    user2        0 feb  3 12:18 tuberia
[user2@luiscarrera ~]$ w > tuberia &
[1] 13607
[user2@luiscarrera ~]$ ls -l
total 44
-rw-rw-r--. 1 user2    user2        0 ene 27 20:27 2
-rw-r--r--. 9 lcarrera lcarrera 14232 feb  3 12:03 CLASE1.txt
lrwxrwxrwx. 1 user2    user2        6 feb  3 12:16 Clases -> Cursos
drwxrwxr-x. 3 user2    user2     4096 feb  3 12:09 Cursos
drwxrwxr-x. 2 user2    user2     4096 ene 27 19:42 ejercicios
-rw-rw-r--. 1 user2    user2       72 ene 27 18:50 errores
-rw-rw-r--. 1 user2    user2        0 feb  3 12:14 examen
drwxrwxr-x. 2 user2    user2     4096 feb  3 12:06 Examenes
drwxrwxr-x. 3 user2    user2     4096 ene 27 17:59 github
-rw-rw-r--. 1 user2    user2     1123 feb  3 10:59 mes1
-rw-r--r--. 1 user2    user2     2991 feb  3 11:42 passwd
prw-rw-r--. 1 user2    user2        0 feb  3 12:18 tuberia
[user2@luiscarrera ~]$ cat tuberia
 12:19:24 up  2:40, 17 users,  load average: 0,00, 0,00, 0,05
USER     TTY      FROM              LOGIN@   IDLE   JCPU   PCPU WHAT
root     tty1     :0               09:41    2:40m  3:39   3:39  /usr/bin/Xorg :
root     pts/0    :0.0             09:41   12:13   0.02s  0.02s bash
root     pts/1    :0.0             09:49    2:18m  0.06s  0.06s bash
root     pts/2    :0.0             10:01    1.00s  0.27s  0.00s cat tuberia
user4    pts/3    172.17.3.252     10:04    1.00s  0.34s  0.34s -bash
user2    pts/4    172.17.2.219     10:14    0.00s  0.38s  0.00s cat tuberia
user1    pts/5    172.17.2.217     10:14   32:57   0.07s  0.07s -bash
user11   pts/6    172.17.2.216     10:16    1:23m  0.03s  0.03s -bash
user3    pts/7    172.17.3.220     10:29   44.00s  0.36s  0.36s -bash
user5    pts/8    172.17.2.223     10:34   10:44   0.14s  0.14s -bash
user8    pts/9    172.17.2.227     10:57   30.00s  0.07s  0.07s -bash
user11   pts/10   172.17.2.216     10:57    1:21m  0.02s  0.02s -bash
user9    pts/11   172.17.2.226     11:02    3:37   0.07s  0.07s -bash
user7    pts/12   172.17.2.231     11:08   10:16   0.17s  0.17s -bash
user10   pts/13   172.17.2.233     11:33    1.00s  0.12s  0.12s -bash
user11   pts/14   172.17.2.216     11:43    2:43   0.04s  0.04s -bash
user1    pts/15   172.17.2.217     12:12    6:45   0.03s  0.03s -bash
[1]+  Hecho                   w > tuberia
[user2@luiscarrera ~]$ cat tuberia
^C
[user2@luiscarrera ~]$
```


Porciones de memoria que el sistema lo trata como dico duro.

```sh
[user2@luiscarrera ~]$ df
df: «/root/.gvfs»: Permiso denegado
Filesystem     1K-blocks     Used Available Use% Mounted on
/dev/sda4       30237648 15232884  13468764  54% /
tmpfs            3995680    19028   3976652   1% /dev/shm
/dev/sda3         297485    72180    209945  26% /boot
[user2@luiscarrera ~]$ mount
/dev/sda4 on / type ext4 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
tmpfs on /dev/shm type tmpfs (rw,rootcontext="system_u:object_r:tmpfs_t:s0")
/dev/sda3 on /boot type ext4 (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
none on /sys/kernel/config type configfs (rw)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)
gvfs-fuse-daemon on /root/.gvfs type fuse.gvfs-fuse-daemon (rw,nosuid,nodev)
[user2@luiscarrera ~]$
```


Utilitarios

find
	Encuentra archivos que cumplen con alguna característica
	
	find inicio característica

	iname
		nombre del archivo sin considerar mayúsculas y minúsculas
	name
		nombre del archivo
	type
		tipo del archivo
			f 		archivo regular
			d 		directorio
			s 		socket
			l 		enlace simbólico


Expresión regular, se usa para 

Investigar las opciones con find.

vi
	Editor de texto instalado de manera predeterminada en todas las distribuciones linux y en la mayoría de versiones de UNIX.

	Es un editor de dos estados (comando, edición), siendo el estado predeterminado el estado comando.

	Estado comando

	En este estado el editor interpreta la digitación de celdas como órdenes que debe ejecutar.

	Órdenes comunes:
	De edición:

	x 	eliminar un caracter
	dd 	eliminar una línea
	D 	eliminar desde la posición actual del curso hasta el fin de la línea
	cw 	modificar el contenido hasta la siguiente palabra
	dw 	eliminar desde la posición actual hasta la siguiente palabra
	
	De desplazamiento
	
	h 	un caracter a la izquierda
	j 	una línea abajo
	k 	una línea arriba
	l 	un caracter a la derecha
	G 	ir a la última línea
	#G 	ir a la línea N
	De búsqueda

	/cadena buscar cadena hacia el final del archivo
	?cadena buscar cadena hacia el inicio del archivo
	n 		Repetir la búsqueda en la dirección inicial
	N 		Repetir la búsqueda en la dirección contraria a la inicial

	Para ingresar al modo edición
	a 		Agregar contenido a la derecha del cursor
	A 		Agregar contenido al final de la línea
	i 		Agregar contenido a la izquierda del cursor
	I 		Agregar contenido al inicio de la línea
	o 		Agregar contenido una línea abajo
	O 		Agregar contenido una línea arriba

	Regresar al modo comando

	ESC

	Comandos dos puntos (se requiere presionar : antes del comando)
	w 		grabar (ya debe tener nombre)
	wnombre grabar como (nombre)
	q 		salir del editor
	wq 		grabar y salir
	!q 		salir desechando los cambios.


	cp /tmp/messages .

archivo de registro


[user2@luiscarrera academia]$ cd javascript/
[user2@luiscarrera javascript]$ ls
[user2@luiscarrera javascript]$ for i in {1..4}; do
> mkdir clase"$i"
> done
[user2@luiscarrera javascript]$
[user2@luiscarrera javascript]$ ls
clase1  clase2  clase3  clase4
[user2@luiscarrera javascript]$ cd ..
[user2@luiscarrera academia]$ tree
.
├── css
│   ├── clase1
│   ├── clase2
│   ├── clase3
│   └── clase4
├── html
│   ├── clase1
│   ├── clase2
│   ├── clase3
│   └── clase4
├── javascript
│   ├── clase1
│   ├── clase2
│   ├── clase3
│   └── clase4
├── linux
│   ├── clase1
│   ├── clase2
│   ├── clase3
│   └── clase4
├── mysql
│   ├── clase1
│   ├── clase2
│   ├── clase3
│   └── clase4
└── php
    ├── clase1
    ├── clase2
    ├── clase3
    └── clase4

30 directories, 0 files
[user2@luiscarrera academia]$ cd
[user2@luiscarrera ~]$ ps
  PID TTY          TIME CMD
14825 pts/10   00:00:00 bash
15811 pts/10   00:00:00 ps
[user2@luiscarrera ~]$ mkdir bien
[user2@luiscarrera ~]$ cd bien/
[user2@luiscarrera bien]$ mkdir -p academia/cursos/
[user2@luiscarrera bien]$ cd academia/cursos/
[user2@luiscarrera cursos]$ mkdir -p {linux,php,mysql,html,css,javascript}/{clase1,clase2,clase3,clase4,examen}/{ejercicio}
[user2@luiscarrera cursos]$ cd ..
[user2@luiscarrera academia]$ cd ..
[user2@luiscarrera bien]$ cd academia/
[user2@luiscarrera academia]$ cd ..
[user2@luiscarrera bien]$ tree academia/
academia/
└── cursos
    ├── css
    │   ├── clase1
    │   │   └── {ejercicio}
    │   ├── clase2
    │   │   └── {ejercicio}
    │   ├── clase3
    │   │   └── {ejercicio}
    │   ├── clase4
    │   │   └── {ejercicio}
    │   └── examen
    │       └── {ejercicio}
    ├── html
    │   ├── clase1
    │   │   └── {ejercicio}
    │   ├── clase2
    │   │   └── {ejercicio}
    │   ├── clase3
    │   │   └── {ejercicio}
    │   ├── clase4
    │   │   └── {ejercicio}
    │   └── examen
    │       └── {ejercicio}
    ├── javascript
    │   ├── clase1
    │   │   └── {ejercicio}
    │   ├── clase2
    │   │   └── {ejercicio}
    │   ├── clase3
    │   │   └── {ejercicio}
    │   ├── clase4
    │   │   └── {ejercicio}
    │   └── examen
    │       └── {ejercicio}
    ├── linux
    │   ├── clase1
    │   │   └── {ejercicio}
    │   ├── clase2
    │   │   └── {ejercicio}
    │   ├── clase3
    │   │   └── {ejercicio}
    │   ├── clase4
    │   │   └── {ejercicio}
    │   └── examen
    │       └── {ejercicio}
    ├── mysql
    │   ├── clase1
    │   │   └── {ejercicio}
    │   ├── clase2
    │   │   └── {ejercicio}
    │   ├── clase3
    │   │   └── {ejercicio}
    │   ├── clase4
    │   │   └── {ejercicio}
    │   └── examen
    │       └── {ejercicio}
    └── php
        ├── clase1
        │   └── {ejercicio}
        ├── clase2
        │   └── {ejercicio}
        ├── clase3
        │   └── {ejercicio}
        ├── clase4
        │   └── {ejercicio}
        └── examen
            └── {ejercicio}

67 directories, 0 files
[user2@luiscarrera bien]$
[user2@luiscarrera bien]$ find . -name clase1
./academia/cursos/linux/clase1
./academia/cursos/javascript/clase1
./academia/cursos/php/clase1
./academia/cursos/mysql/clase1
./academia/cursos/html/clase1
./academia/cursos/css/clase1
[user2@luiscarrera bien]$ find . -name clase[1-4]
./academia/cursos/linux/clase2
./academia/cursos/linux/clase3
./academia/cursos/linux/clase4
./academia/cursos/linux/clase1
./academia/cursos/javascript/clase2
./academia/cursos/javascript/clase3
./academia/cursos/javascript/clase4
./academia/cursos/javascript/clase1
./academia/cursos/php/clase2
./academia/cursos/php/clase3
./academia/cursos/php/clase4
./academia/cursos/php/clase1
./academia/cursos/mysql/clase2
./academia/cursos/mysql/clase3
./academia/cursos/mysql/clase4
./academia/cursos/mysql/clase1
./academia/cursos/html/clase2
./academia/cursos/html/clase3
./academia/cursos/html/clase4
./academia/cursos/html/clase1
./academia/cursos/css/clase2
./academia/cursos/css/clase3
./academia/cursos/css/clase4
./academia/cursos/css/clase1
[user2@luiscarrera bien]$ find .type -d
find: atención: la opción -d está obsoleta; por favor utilice -depth en su lugar,
ya que se trata de una característica que cumple con POSIX.
find: «.type»: No existe el fichero o el directorio
[user2@luiscarrera bien]$ find . -type d
.
./academia
./academia/cursos
./academia/cursos/linux
./academia/cursos/linux/examen
./academia/cursos/linux/examen/{ejercicio}
./academia/cursos/linux/clase2
./academia/cursos/linux/clase2/{ejercicio}
./academia/cursos/linux/clase3
./academia/cursos/linux/clase3/{ejercicio}
./academia/cursos/linux/clase4
./academia/cursos/linux/clase4/{ejercicio}
./academia/cursos/linux/clase1
./academia/cursos/linux/clase1/{ejercicio}
./academia/cursos/javascript
./academia/cursos/javascript/examen
./academia/cursos/javascript/examen/{ejercicio}
./academia/cursos/javascript/clase2
./academia/cursos/javascript/clase2/{ejercicio}
./academia/cursos/javascript/clase3
./academia/cursos/javascript/clase3/{ejercicio}
./academia/cursos/javascript/clase4
./academia/cursos/javascript/clase4/{ejercicio}
./academia/cursos/javascript/clase1
./academia/cursos/javascript/clase1/{ejercicio}
./academia/cursos/php
./academia/cursos/php/examen
./academia/cursos/php/examen/{ejercicio}
./academia/cursos/php/clase2
./academia/cursos/php/clase2/{ejercicio}
./academia/cursos/php/clase3
./academia/cursos/php/clase3/{ejercicio}
./academia/cursos/php/clase4
./academia/cursos/php/clase4/{ejercicio}
./academia/cursos/php/clase1
./academia/cursos/php/clase1/{ejercicio}
./academia/cursos/mysql
./academia/cursos/mysql/examen
./academia/cursos/mysql/examen/{ejercicio}
./academia/cursos/mysql/clase2
./academia/cursos/mysql/clase2/{ejercicio}
./academia/cursos/mysql/clase3
./academia/cursos/mysql/clase3/{ejercicio}
./academia/cursos/mysql/clase4
./academia/cursos/mysql/clase4/{ejercicio}
./academia/cursos/mysql/clase1
./academia/cursos/mysql/clase1/{ejercicio}
./academia/cursos/html
./academia/cursos/html/examen
./academia/cursos/html/examen/{ejercicio}
./academia/cursos/html/clase2
./academia/cursos/html/clase2/{ejercicio}
./academia/cursos/html/clase3
./academia/cursos/html/clase3/{ejercicio}
./academia/cursos/html/clase4
./academia/cursos/html/clase4/{ejercicio}
./academia/cursos/html/clase1
./academia/cursos/html/clase1/{ejercicio}
./academia/cursos/css
./academia/cursos/css/examen
./academia/cursos/css/examen/{ejercicio}
./academia/cursos/css/clase2
./academia/cursos/css/clase2/{ejercicio}
./academia/cursos/css/clase3
./academia/cursos/css/clase3/{ejercicio}
./academia/cursos/css/clase4
./academia/cursos/css/clase4/{ejercicio}
./academia/cursos/css/clase1
./academia/cursos/css/clase1/{ejercicio}
[user2@luiscarrera bien]$ find . -type f -exec ls - {} \;
[user2@luiscarrera bien]$ cd
[user2@luiscarrera ~]$ find . -type f -exec ls - {} \;
ls: no se puede acceder a -: No existe el fichero o el directorio
./.bash_history
ls: no se puede acceder a -: No existe el fichero o el directorio
./CLASE1.txt
ls: no se puede acceder a -: No existe el fichero o el directorio
./2
ls: no se puede acceder a -: No existe el fichero o el directorio
./examen
ls: no se puede acceder a -: No existe el fichero o el directorio
./github/.git/description
ls: no se puede acceder a -: No existe el fichero o el directorio
./github/.git/info/exclude
ls: no se puede acceder a -: No existe el fichero o el directorio
./github/.git/hooks/pre-rebase.sample
ls: no se puede acceder a -: No existe el fichero o el directorio
./github/.git/hooks/prepare-commit-msg.sample
ls: no se puede acceder a -: No existe el fichero o el directorio
./github/.git/hooks/post-update.sample
ls: no se puede acceder a -: No existe el fichero o el directorio
./github/.git/hooks/applypatch-msg.sample
ls: no se puede acceder a -: No existe el fichero o el directorio
./github/.git/hooks/post-commit.sample
ls: no se puede acceder a -: No existe el fichero o el directorio
./github/.git/hooks/post-receive.sample
ls: no se puede acceder a -: No existe el fichero o el directorio
./github/.git/hooks/commit-msg.sample
ls: no se puede acceder a -: No existe el fichero o el directorio
./github/.git/hooks/pre-applypatch.sample
ls: no se puede acceder a -: No existe el fichero o el directorio
./github/.git/hooks/pre-commit.sample
ls: no se puede acceder a -: No existe el fichero o el directorio
./github/.git/hooks/update.sample
ls: no se puede acceder a -: No existe el fichero o el directorio
./github/.git/config
ls: no se puede acceder a -: No existe el fichero o el directorio
./github/.git/HEAD
ls: no se puede acceder a -: No existe el fichero o el directorio
./github/hola.tex
ls: no se puede acceder a -: No existe el fichero o el directorio
./archivo2
ls: no se puede acceder a -: No existe el fichero o el directorio
./ejercicios/academia/cursos/linux/clase2
ls: no se puede acceder a -: No existe el fichero o el directorio
./ejercicios/academia/cursos/linux/clase3
ls: no se puede acceder a -: No existe el fichero o el directorio
./ejercicios/academia/cursos/linux/clase4
ls: no se puede acceder a -: No existe el fichero o el directorio
./ejercicios/academia/cursos/linux/clase1
ls: no se puede acceder a -: No existe el fichero o el directorio
./ejercicios/academia/cursos/javascript/clase2
ls: no se puede acceder a -: No existe el fichero o el directorio
./ejercicios/academia/cursos/javascript/clase3
ls: no se puede acceder a -: No existe el fichero o el directorio
./ejercicios/academia/cursos/javascript/clase4
ls: no se puede acceder a -: No existe el fichero o el directorio
./ejercicios/academia/cursos/javascript/clase1
ls: no se puede acceder a -: No existe el fichero o el directorio
./ejercicios/academia/cursos/php/clase2
ls: no se puede acceder a -: No existe el fichero o el directorio
./ejercicios/academia/cursos/php/clase3
ls: no se puede acceder a -: No existe el fichero o el directorio
./ejercicios/academia/cursos/php/clase4
ls: no se puede acceder a -: No existe el fichero o el directorio
./ejercicios/academia/cursos/php/clase1
ls: no se puede acceder a -: No existe el fichero o el directorio
./ejercicios/academia/cursos/mysql/clase2
ls: no se puede acceder a -: No existe el fichero o el directorio
./ejercicios/academia/cursos/mysql/clase3
ls: no se puede acceder a -: No existe el fichero o el directorio
./ejercicios/academia/cursos/mysql/clase4
ls: no se puede acceder a -: No existe el fichero o el directorio
./ejercicios/academia/cursos/mysql/clase1
ls: no se puede acceder a -: No existe el fichero o el directorio
./ejercicios/academia/cursos/html/clase2
ls: no se puede acceder a -: No existe el fichero o el directorio
./ejercicios/academia/cursos/html/clase3
ls: no se puede acceder a -: No existe el fichero o el directorio
./ejercicios/academia/cursos/html/clase4
ls: no se puede acceder a -: No existe el fichero o el directorio
./ejercicios/academia/cursos/html/clase1
ls: no se puede acceder a -: No existe el fichero o el directorio
./ejercicios/academia/cursos/css/clase2
ls: no se puede acceder a -: No existe el fichero o el directorio
./ejercicios/academia/cursos/css/clase3
ls: no se puede acceder a -: No existe el fichero o el directorio
./ejercicios/academia/cursos/css/clase4
ls: no se puede acceder a -: No existe el fichero o el directorio
./ejercicios/academia/cursos/css/clase1
ls: no se puede acceder a -: No existe el fichero o el directorio
./.bash_profile
ls: no se puede acceder a -: No existe el fichero o el directorio
./passwd
ls: no se puede acceder a -: No existe el fichero o el directorio
./.emacs
ls: no se puede acceder a -: No existe el fichero o el directorio
./mes1
ls: no se puede acceder a -: No existe el fichero o el directorio
./ejercicios2
ls: no se puede acceder a -: No existe el fichero o el directorio
./.bashrc
ls: no se puede acceder a -: No existe el fichero o el directorio
./.bash_logout
ls: no se puede acceder a -: No existe el fichero o el directorio
./errores
[user2@luiscarrera ~]$ find . -type f -exec ls -l {} \;
-rw-------. 1 user2 user2 5067 ene 27 20:54 ./.bash_history
-rw-r--r--. 8 lcarrera lcarrera 18469 feb  3 14:39 ./CLASE1.txt
-rw-rw-r--. 1 user2 user2 0 ene 27 20:27 ./2
-rw-rw-r--. 1 user2 user2 0 feb  3 12:14 ./examen
-rw-rw-r--. 1 user2 user2 73 ene 27 17:31 ./github/.git/description
-rw-rw-r--. 1 user2 user2 240 ene 27 17:31 ./github/.git/info/exclude
-rwxrwxr-x. 1 user2 user2 4951 ene 27 17:31 ./github/.git/hooks/pre-rebase.sample
-rwxrwxr-x. 1 user2 user2 1239 ene 27 17:31 ./github/.git/hooks/prepare-commit-msg.sample
-rwxrwxr-x. 1 user2 user2 189 ene 27 17:31 ./github/.git/hooks/post-update.sample
-rwxrwxr-x. 1 user2 user2 452 ene 27 17:31 ./github/.git/hooks/applypatch-msg.sample
-rwxrwxr-x. 1 user2 user2 160 ene 27 17:31 ./github/.git/hooks/post-commit.sample
-rwxrwxr-x. 1 user2 user2 548 ene 27 17:31 ./github/.git/hooks/post-receive.sample
-rwxrwxr-x. 1 user2 user2 896 ene 27 17:31 ./github/.git/hooks/commit-msg.sample
-rwxrwxr-x. 1 user2 user2 398 ene 27 17:31 ./github/.git/hooks/pre-applypatch.sample
-rwxrwxr-x. 1 user2 user2 1578 ene 27 17:31 ./github/.git/hooks/pre-commit.sample
-rwxrwxr-x. 1 user2 user2 3611 ene 27 17:31 ./github/.git/hooks/update.sample
-rw-rw-r--. 1 user2 user2 92 ene 27 17:31 ./github/.git/config
-rw-rw-r--. 1 user2 user2 23 ene 27 17:31 ./github/.git/HEAD
-rw-rw-r--. 1 user2 user2 11 ene 27 17:59 ./github/hola.tex
-rw-------. 1 user2 user2 0 feb  3 13:32 ./archivo2
-rw-rw-r--. 1 user2 user2 0 feb  3 13:56 ./ejercicios/academia/cursos/linux/clase2
-rw-rw-r--. 1 user2 user2 0 feb  3 13:56 ./ejercicios/academia/cursos/linux/clase3
-rw-rw-r--. 1 user2 user2 0 feb  3 13:56 ./ejercicios/academia/cursos/linux/clase4
-rw-rw-r--. 1 user2 user2 0 feb  3 13:55 ./ejercicios/academia/cursos/linux/clase1
-rw-rw-r--. 1 user2 user2 0 feb  3 13:59 ./ejercicios/academia/cursos/javascript/clase2
-rw-rw-r--. 1 user2 user2 0 feb  3 13:59 ./ejercicios/academia/cursos/javascript/clase3
-rw-rw-r--. 1 user2 user2 0 feb  3 13:59 ./ejercicios/academia/cursos/javascript/clase4
-rw-rw-r--. 1 user2 user2 0 feb  3 13:59 ./ejercicios/academia/cursos/javascript/clase1
-rw-rw-r--. 1 user2 user2 0 feb  3 13:57 ./ejercicios/academia/cursos/php/clase2
-rw-rw-r--. 1 user2 user2 0 feb  3 13:57 ./ejercicios/academia/cursos/php/clase3
-rw-rw-r--. 1 user2 user2 0 feb  3 13:57 ./ejercicios/academia/cursos/php/clase4
-rw-rw-r--. 1 user2 user2 0 feb  3 13:57 ./ejercicios/academia/cursos/php/clase1
-rw-rw-r--. 1 user2 user2 0 feb  3 13:58 ./ejercicios/academia/cursos/mysql/clase2
-rw-rw-r--. 1 user2 user2 0 feb  3 13:58 ./ejercicios/academia/cursos/mysql/clase3
-rw-rw-r--. 1 user2 user2 0 feb  3 13:58 ./ejercicios/academia/cursos/mysql/clase4
-rw-rw-r--. 1 user2 user2 0 feb  3 13:58 ./ejercicios/academia/cursos/mysql/clase1
-rw-rw-r--. 1 user2 user2 0 feb  3 13:58 ./ejercicios/academia/cursos/html/clase2
-rw-rw-r--. 1 user2 user2 0 feb  3 13:58 ./ejercicios/academia/cursos/html/clase3
-rw-rw-r--. 1 user2 user2 0 feb  3 13:58 ./ejercicios/academia/cursos/html/clase4
-rw-rw-r--. 1 user2 user2 0 feb  3 13:58 ./ejercicios/academia/cursos/html/clase1
-rw-rw-r--. 1 user2 user2 0 feb  3 13:59 ./ejercicios/academia/cursos/css/clase2
-rw-rw-r--. 1 user2 user2 0 feb  3 13:59 ./ejercicios/academia/cursos/css/clase3
-rw-rw-r--. 1 user2 user2 0 feb  3 13:59 ./ejercicios/academia/cursos/css/clase4
-rw-rw-r--. 1 user2 user2 0 feb  3 13:59 ./ejercicios/academia/cursos/css/clase1
-rw-r--r--. 1 user2 user2 176 feb 21  2013 ./.bash_profile
-rw-r--r--. 1 user2 user2 2991 feb  3 11:42 ./passwd
-rw-r--r--. 1 user2 user2 500 feb 27  2012 ./.emacs
-rw-rw-r--. 1 user2 user2 1123 feb  3 10:59 ./mes1
-rw-r--r--. 3 root root 626 feb  3 13:43 ./ejercicios2
-rw-r--r--. 1 user2 user2 124 feb 21  2013 ./.bashrc
-rw-r--r--. 1 user2 user2 18 feb 21  2013 ./.bash_logout
----------. 1 user2 user2 72 ene 27 18:50 ./errores
[user2@luiscarrera ~]$ touch clase1
[user2@luiscarrera ~]$ find . -name clase1
./academia/linux/clase1
./academia/javascript/clase1
./academia/php/clase1
./academia/mysql/clase1
./academia/html/clase1
./academia/css/clase1
./bien/academia/cursos/linux/clase1
./bien/academia/cursos/javascript/clase1
./bien/academia/cursos/php/clase1
./bien/academia/cursos/mysql/clase1
./bien/academia/cursos/html/clase1
./bien/academia/cursos/css/clase1
./ejercicios/academia/cursos/linux/clase1
./ejercicios/academia/cursos/javascript/clase1
./ejercicios/academia/cursos/php/clase1
./ejercicios/academia/cursos/mysql/clase1
./ejercicios/academia/cursos/html/clase1
./ejercicios/academia/cursos/css/clase1
./clase1
[user2@luiscarrera ~]$ find . -name clase1 -type f
./ejercicios/academia/cursos/linux/clase1
./ejercicios/academia/cursos/javascript/clase1
./ejercicios/academia/cursos/php/clase1
./ejercicios/academia/cursos/mysql/clase1
./ejercicios/academia/cursos/html/clase1
./ejercicios/academia/cursos/css/clase1
./clase1
[user2@luiscarrera ~]$ find . -name clase1 -type f -exec ls -l {} \;
-rw-rw-r--. 1 user2 user2 0 feb  3 13:55 ./ejercicios/academia/cursos/linux/clase1
-rw-rw-r--. 1 user2 user2 0 feb  3 13:59 ./ejercicios/academia/cursos/javascript/clase1
-rw-rw-r--. 1 user2 user2 0 feb  3 13:57 ./ejercicios/academia/cursos/php/clase1
-rw-rw-r--. 1 user2 user2 0 feb  3 13:58 ./ejercicios/academia/cursos/mysql/clase1
-rw-rw-r--. 1 user2 user2 0 feb  3 13:58 ./ejercicios/academia/cursos/html/clase1
-rw-rw-r--. 1 user2 user2 0 feb  3 13:59 ./ejercicios/academia/cursos/css/clase1
-rw-rw-r--. 1 user2 user2 0 feb  3 14:44 ./clase1
[user2@luiscarrera ~]$ man find
[user2@luiscarrera ~]$ cp /tmp/messages .^C
[user2@luiscarrera ~]$ cp /tmp/messages .
[user2@luiscarrera ~]$ cp /tmp/messages .
[user2@luiscarrera ~]$ cp /tmp/messages .
[user2@luiscarrera ~]$ ls
2  academia  archivo2  bien  clase1  CLASE1.txt  Clases  Cursos  directorio1  directorio2  ejercicios  ejercicios2  errores  examen  Examenes  github  mes1  messages  passwd  tuberia
[user2@luiscarrera ~]$



chmod a+x cuenta.sh
ls -l cuenta.sh
./cuenta.sh

```bash
[user2@luiscarrera ~]$ ^C
[user2@luiscarrera ~]$ vi messages
[user2@luiscarrera ~]$ vi messages
[user2@luiscarrera ~]$ vi messages
[user2@luiscarrera ~]$ vi mensajes.txt
[user2@luiscarrera ~]$ cat mensajes.txt
Este es un archivo
creado con vi
en la clase de linux I

[user2@luiscarrera ~]$ vi mensajes2.sh
[user2@luiscarrera ~]$ cat mensajes
cat: mensajes: No existe el fichero o el directorio
[user2@luiscarrera ~]$ cat
cat        catchsegv
[user2@luiscarrera ~]$ cat mensajes.sh
cat: mensajes.sh: No existe el fichero o el directorio
[user2@luiscarrera ~]$ vi cuenta.sh
[user2@luiscarrera ~]$ cat cuenta.sh
#!/bin/bash
for i in 1 2 3 4 5 6
do
echo "i=$i"
done
[user2@luiscarrera ~]$ chmod a+x cuenta.sh
[user2@luiscarrera ~]$ ls -l cuenta.sh
-rwxrwxr-x. 1 user2 user2 53 feb  3 15:16 cuenta.sh
[user2@luiscarrera ~]$ ./cuenta.sh
i=1
i=2
i=3
i=4
i=5
i=6
[user2@luiscarrera ~]$ cat cuenta.sh
#!/bin/bash
for i in 1 2 3 4 5 6
do
echo "i=$i"
done
[user2@luiscarrera ~]$
```

vi cuenta.cc
ls -l cuenta .cc
g++ -o cuenta cuenta.cc
ls -l cuenta

./cuenta

file cuenta.sh
file academia/


La edición de un archivo nuevo inicia ejecutando el comando vi

La edición de un archivo nuevo incia ejecutando el comando vi.

La edición de un archivo ya creado inicia ejecutando el comando vi usando como parámetro el nombre del archivo.

El comando file devuelve el tipo de contenido del archivo


Lista de comandos:

 1  pwd
    2  ls
    3  id
    4  hostname
    5  uname
    6  uname -r
    7  date
    8  who
    9  w
   10  who
   11  who -r
   12  man who
   13  cat /etc/resolv.conf
   14  man cat
   15  man dns
   16  cat /etc/resolv.conf
   17  cat /etc/resolv.conf
   18  head /etc/passwd
   19  head -1/etc/passwd
   20  head -1 /etc/passwd
   21  head -20 /etc/passwd
   22  tail -20 /etc/passwd
   23  tail -1 /etc/passwd
   24  wc /etc/passwd
   25  wc -l /etc/passwd
   26  wc -w /etc/passwd
   27  wc -c /etc/passwd
   28  wc -l /etc/passwd
   29  58 /etc/passwd
   30  [user2@luiscarrera ~]$ wc -w /etc/passwd
   31  99 /etc/passwd
   32  [user2@luiscarrera ~]$ wc -c /etc/passwd
   33  2925 /etc/passwd
   34  wc -l /etc/passwd
   35  58 /etc/passwd
   36  [user2@luiscarrera ~]$ wc -w /etc/passwd
   37  99 /etc/passwd
   38  [user2@luiscarrera ~]$ wc -c /etc/passwd
   39  2925 /etc/passwd
   40  wc -l /etc/passwd
   41  58 /etc/passwd
   42  [user2@luiscarrera ~]$ wc -w /etc/passwd
   43  99 /etc/passwd
   44  [user2@luiscarrera ~]$ wc -c /etc/passwd
   45  2925 /etc/passwd
   46  wc -l /etc/passwd
   47  58 /etc/passwd
   48  [user2@luiscarrera ~]$ wc -w /etc/passwd
   49  99 /etc/passwd
   50  [user2@luiscarrera ~]$ wc -c /etc/passwd
   51  2925 /etc/passwd
   52  wc -l /etc/passwd
   53  58 /etc/passwd
   54  [user2@luiscarrera ~]$ wc -w /etc/passwd
   55  99 /etc/passwd
   56  [user2@luiscarrera ~]$ wc -c /etc/passwd
   57  2925 /etc/passwd
   58  wc -l /etc/passwd
   59  58 /etc/passwd
   60  [user2@luiscarrera ~]$ wc -w /etc/passwd
   61  99 /etc/passwd
   62  [user2@luiscarrera ~]$ wc -c /etc/passwd
   63  2925 /etc/passwd
   64  grep user /etc/passwd
   65  logout
   66  grep user[1-5] /etc/passwd
   67  cut -c1-10 /etc/passwd
   68  cut -d: -f1 /etc/passwd
   69  cut -d: -f1-3 /etc/passwd
   70  cut -d: -f15,6 /etc/passwd
   71  cut -d: -f16,7 /etc/passwd
   72  cut -d: -f3- /etc/passwd
   73  su
   74  cal
   75  cal 2018
   76  man cal
   77  cal 25 12 1
   78  cal 23 3 1964
   79  wall
   80  su
   81  write user1
   82  write user1 user3
   83  write user2 user3
   84  write user3
   85  write user1
   86  wall
   87  who
   88  talk user1
   89  cat /etc/host
   90  cat /etc/hosts
   91  talk user1
   92  who
   93  talk user3
   94  logout
   95  talk user3
   96  logout
   97  talk user3
   98  who
   99  talk user3
  100  mail user1
  101  mail
  102  mail user3
  103  mail
  104  su - lcarrera
  105  su
  106  git --v
  107  pwd
  108  git clone https://github.com/carlosal1015/Linux-Administrator.git
  109  ls
  110  pwd
  111  mkdir github
  112  cd github/
  113  git init
  114  git clone https://github.com/carlosal1015/Linux-Administrator.git
  115  cd
  116  mail
  117  mailq
  118  mail -u
  119  mail
  120  id
  121  archivo /etc/passwd
  122  cat /etc/passwd
  123  tex --v
  124  ls
  125  cd github/
  126  echo "Hola mundo" > hola.tex
  127  ls
  128  cat hola.tex
  129  CURSO="Linux Administracion"
  130  echo Universidad Nacional de Ingeniería
  131  echo CURSO
  132  echo $CURSO
  133  pwd
  134  set
  135  PS1
  136  PS1='Linux Administracion>'
  137  PS1='[\u@\h \W]\$ '
  138  ls
  139  ls /etc/passwd
  140  ls /etc/passwd/
  141  cd
  142  ls /etc/passwd/
  143  ls /etc/passwd
  144  ls /etc
  145  ls /etc/
  146  ls -l /etc/
  147  ls /dev/
  148  ls -l /dev/
  149  ls -l /dev/tty
  150  ls -l /dev/tty1
  151  ls -l /dev/tty[1-5]
  152  ls -l /dev/tty[1-5]
  153  ls -l /dev/tty1 /dev/tty3 /dev/tty3 /dev/tty4 /dev/tty5
  154  ls -l /dev/tty[^1357]
  155  ls -l /dev/tty[1357][2468]
  156  ls -l /dev/tty? #imprime un caracter
  157  for i [1-5] i
  158  for i[1-5] i
  159  for i[1-5];i
  160  for i[1-5];1
  161  for i[1-5];exit
  162  ls -l /dev/tty*
  163  ls /dev/tty*
  164  pwd
  165  ls
  166  cal
  167  ls cal > enero
  168  cal > enero
  169  ls
  170  cat enero
  171  date > enero
  172  cat enero
  173  cat >> enero
  174  cal >> enero
  175  cat enero
  176  ls -l enero
  177  ls -l enero febrero
  178  cal >> enero
  179  cat enero
  180  cal > enero
  181  cat enero
  182  ls -l enero
  183  ls -l enero febrero
  184  ls -l enero febrero 2> errores
  185  ñs
  186  ls
  187  cat errores
  188  write user1
  189  writer user2
  190  write user2
  191  write user3
  192  dsadasdasd
  193  q
  194  .
  195  -
  196  ls
  197  write user3 < errores
  198  write user3 < /home/user2/errores
  199  mail
  200  write user2 < /home/user2/enero
  201  mail -s enero user3 < /home/user2/enero
  202  mail -s enero user3 < /home/user2/enero
  203  write user1 << FIN
  204  Este mensaje
  205  es una prueba
  206  entrada con etiqueta
  207  FIN
  208  mail
  209  cal | write user3
  210  who | mail -s salida user3
  211  who | mail -s salida lcarrera user1 user2 user3 user4 user5 user6 user7 user8 user9 user10 user11
  212  mail
  213  which cal
  214  ls -l /usr/bin/cal
  215  ls -l `which cal`
  216  mail
  217  grep sh /etc/passwd | cut -c1-5 | wc-l
  218  grep sh /etc/passwd |cut -d: 1-5|wc -l
  219  pwd
  220  mkdir ejercicios
  221  cd ejercicios/
  222  cd
  223  pwd
  224  ls
  225  cd ejercicios/
  226  cd
  227  cd ..
  228  ls
  229  cd ..
  230  cal ? 7 1821
  231  cal 1 7 1821
  232  who
  233  man who
  234  who -count
  235  who --count
  236  man who
  237  man -q --count
  238  who -q |--count
  239  man who
  240  who -q --count
  241  who --count
  242  man cat
  243  grep user[10-20] /etc/passwd
  244  cat[10-20] /etc/passwd
  245  cat [10-20] /etc/passwd
  246  man head
  247  man cat
  248  head -[10] /etc/passwd
  249  head [-10] /etc/passwd
  250  head -20 /etc/passwd
  251  head -20 /etc/passwd | head -^10 /etc/passwd
  252  cd
  253  ls
  254  ls /etc/passwd
  255  cat /etc/passwd.
  256  cat /etc/passwd
  257  cat /etc/passwd -n | head -n 20 | tail -n 9
  258  cat /etc/passwd -n | head -n 20 | tail -n 10
  259  cat /etc/passwd -n | head -n 20 | tail -n 11
  260  man cat
  261  man who
  262  who
  263  man who
  264  who [-imqsuwHT]
  265  who [--count]
  266  who[--count] > 2
  267  who --count > 2
  268  cat 2
  269  man who
  270  who -imqsuwHT > 2
  271  who [-imqsuwHT] > 2
  272  cat 2
  273  who --imqsuwHT > 2
  274  man whi
  275  man who
  276  who am i
  277  who --count
  278  man who
  279  who -i
  280  who --i
  281  who -i
  282  man whi
  283  man who
  284  who --idle
  285  who -idle
  286  who
  287  who -m
  288  who -u
  289  who
  290  man cut
  291  who
  292  man who
  293  who --heading
  294  man who
  295  who --idle
  296  man who
  297  who --idle
  298  who -idle
  299  who --help
  300  ´who -q
  301  whi --count
  302  who -q
  303  who --count
  304  who -u
  305  who --help
  306  who --heading
  307  who -p
  308  who --process
  309  who -process > 2
  310  who --process > 2
  311  cat 2
  312  who -p
  313  who -a
  314  cal 1 7 1821
  315  who -u
  316  who --help
  317  who -q
  318  who -r
  319  who -l
  320  who -u --users
  321  who -p --process
  322  who -u
  323  cut -d: -f1 /etc/passwd
  324  cut -d: -f1,5 /etc/passwd
  325  cut -d: -f11,15 /etc/passwd
  326  cut -d: -f11-15 /etc/passwd
  327  cut -d: -f=11-15 /etc/passwd
  328  cut -d: -f5 /etc/passwd
  329  cut -d: -f15 /etc/passwd
  330  cut -d: -f1,5 /etc/passwd
  331  cut -d: -f1,6 /etc/passwd
  332  cut -d: -f1,7 /etc/passwd
  333   cat /etc/passwd -n | head -n 20 | tail -n 11
  334  logout
  335  ln /home/lcarrera/ejercicios2 .
  336  ls
  337  cat ejercicios2
  338  man ln
  339  ls
  340  cd ejercicios
  341  ls
  342  mkdir academia
  343  cd academia/
  344  mkdir cursos
  345  cd cursos/
  346  mkdir linux
  347  pwd
  348  cd linux/
  349  ls
  350  cd ..
  351  pwd
  352  cd cursos/
  353  ls
  354  cd linux/
  355  ls
  356  touch clase1 & clase2 & clase3 & clase4
  357  ls
  358  touch clase2
  359  touch clase3
  360  touch clase4
  361  ls
  362  cd --
  363  cd ejercicios/academia/
  364  ls
  365  cd cursos/
  366  ls
  367  mkdir php
  368  cd php/
  369  ls
  370  touch clase1
  371  touch clase2
  372  touch clase3
  373  touch clase4
  374  ls
  375  cd ..
  376  ls
  377  mkdir mysql
  378  cd mysql/
  379  touch clase1
  380  touch clase2
  381  touch clase3
  382  touch clase4
  383  ls
  384  cd ..
  385  mkdir html
  386  cd html/
  387  ls
  388  touch clase1
  389  touch clase2
  390  touch clase3
  391  touch clase4
  392  ls
  393  cd ..
  394  mkdir css
  395  cd cd
  396  cd css/
  397  touch clase1
  398  touch clase2
  399  touch clase3
  400  touch clase4
  401  cd ..
  402  mkdir javascript
  403  cd javascript/
  404  touch clase1
  405  touch clase2
  406  touch clase3
  407  touch clase4
  408  ls
  409  cd ..
  410  tree
  411  cd ..
  412  tree academia/
  413  cd
  414  pwd
  415  ls
  416  cd ejercicios
  417  ls
  418  tree academia/
  419  ls
  420  cd
  421  cd ejercicios
  422  ls
  423  cd academia/
  424  ls
  425  tree
  426  cd css
  427  cd cursos/
  428  ls
  429  cd css/
  430  mkdir ejercicios
  431  cd ..
  432  cd html/
  433  mkdir ejercicios
  434  cd ..
  435  cd javascript/
  436  mkdir ejercicios
  437  cd ..
  438  cd linux/
  439  mkdir ejercicios
  440  cd ..
  441  cd mysql/
  442  mkdir ejercicios
  443  cd ..
  444  cd php/
  445  mkdir ejercicios
  446  cd ..
  447  tree
  448  cd css/
  449  mkdir examen
  450  cd ..
  451  cd html/
  452  mkdir examen
  453  cd ..
  454  cd javascript/
  455  mkdir examen
  456  cd ..
  457  cd linux/
  458  mkdir examen
  459  cd ..
  460  cd mysql/
  461  mkdir examen
  462  cd ..
  463  cd php/
  464  mkdir examen
  465  cd ..
  466  tree
  467  cd css
  468  rmdir ejercicios
  469  cd clase1
  470  ls -l
  471  cd ..
  472  ls
  473  cd css
  474  if for i in {1..4}; do   mkdir clase"$i"; done;
  475  ls
  476  cd ..
  477  tree
  478  cd ..
  479  cd
  480  ls
  481  mkdir academia
  482  mkdir css
  483  rmdir css/
  484  cd academia/
  485  ls
  486  mkdir css
  487  mkdir javascript
  488  mkdir html
  489  mkdir mysql
  490  mkdir php
  491  mkdir linux
  492  ls
  493  if for i in {1..4}; do
  494  ls
  495  cd css/
  496  if for i in {1..4}; do mkdir clase"$i"; done;
  497  ls
  498  cd ..
  499  ls
  500  cd css/
  501  ls
  502  for i in {1..4}; do mkdir clase"$i"; done
  503  ls
  504  cd --
  505  cd academia/
  506  ls
  507  cd html/
  508  ls
  509  for i in {1..4}; do mkdir clase"$i"; done
  510  ls
  511  cd ..
  512  cd linux/
  513  for i in {1..4}; do mkdir clase"$i"; done
  514  ls
  515  cd ..
  516  cd php/
  517  ls
  518  for i in {1..4}; do mkdir clase"$i"; done
  519  ls
  520  cd ..
  521  cd mysql/
  522  ls
  523  for i in {1..4}; do mkdir clase"$i"; done
  524  ls
  525  cd ..
  526  cd html/
  527  ls
  528  cd ..
  529  cd css/
  530  ls
  531  cd ..
  532  cd javascript/
  533  ls
  534  for i in {1..4}; do mkdir clase"$i"; done
  535  ls
  536  cd ..
  537  tree
  538  cd
  539  ps
  540  mkdir bien
  541  cd bien/
  542  mkdir -p academia/cursos/
  543  cd academia/cursos/
  544  mkdir -p {linux,php,mysql,html,css,javascript}/{clase1,clase2,clase3,clase4,examen}/{ejercicio}
  545  cd ..
  546  cd academia/
  547  cd ..
  548  tree academia/
  549  find . -name clase1
  550  find . -name clase[1-4]
  551  find .type -d
  552  find . -type d
  553  find . -type f -exec ls - {} \;
  554  cd
  555  find . -type f -exec ls - {} \;
  556  find . -type f -exec ls -l {} \;
  557  touch clase1
  558  find . -name clase1
  559  find . -name clase1 -type f
  560  find . -name clase1 -type f -exec ls -l {} \;
  561  man find
  562  cp /tmp/messages .
  563  ls
  564  vi messages
  565  vi mensajes.txt
  566  cat mensajes.txt
  567  vi mensajes2.sh
  568  cat mensajes
  569  cat mensajes.sh
  570  vi cuenta.sh
  571  cat cuenta.sh
  572  chmod a+x cuenta.sh
  573  ls -l cuenta.sh
  574  ./cuenta.sh
  575  cat cuenta.sh
  576  ls
  577  vi cuenta.sh
  578  vi programa.cpp
  579  history


  El comando mail

  Permite leer los correos almacenados en la casilla de correo así como enviar correos a los demás usuarios del sistema o remotos.

  Modo lectura
  	mail
 luego de ejecutar el comando, se presentará la lista de correos disponibles para lectura.

 El correo activo está marcado por el caracter > es el correo sobre el cual se ejecutarán los comandos.

 Comandos básicos
r
	Responer a todos los destinarios
R
	Responder al remitente
d
	Borrar el mensaje.

Si no se indica el mensaje se ejecutará sobre el correo activo (el que tiene el símbolo >)

Si se indica un número, el comando se ejecutará sobre el correo que esté identificando con ese número.

Modo escritura

Inicia con el comando mail y las direcciones de correo a las cuales se quiere enviar un mensaje
Debe incluirse el subject o tema del correo
y a continuación se ingresa el contenido del mensaje
para terminar la escritura del mensaje se debe incluir un punto al inicio de una línea en blanco

Archivo de configuración

El archivo de configuración se encuentra en el directorio hogar del usuario y se llama .mailrc dentro podremos crear nuestras listas de correo:

alias alumnos user1 user2 user3 user4 user5 user6 user7 user8 user9 user10 user11


mail alumnos
Subject: lista
~r ! who
~r ! cal
.
EOT


Repasar el editor de texto, vi a full y modificar archivos de sistema.

lcarrera@uni.edu.pe

Preguntar y mandar pantallazos. Esto se aprende practicando.


[user2@luiscarrera ~]$ man mail
[user2@luiscarrera ~]$ mail
Heirloom Mail version 12.4 7/29/08.  Type ? for help.
"/var/spool/mail/user2": 22 messages 2 new 7 unread
    1 user3@luiscarrera.pe  Sat Jan 27 16:59  19/588   "examen"
    2 user3@luiscarrera.pe  Sat Jan 27 16:59  19/574   "aaaa"
    3 user3@luiscarrera.pe  Sat Jan 27 17:01  19/584   "examen final 2"
    4 Mail Delivery System  Sat Jan 27 17:07  74/2246  "Undelivered Mail Returned to Sender"
    5 Mail Delivery System  Sat Jan 27 17:07  72/2254  "Undelivered Mail Returned to Sender"
    6 lcarrera@luiscarrera  Sat Jan 27 17:36  25/796   "Re: Las fijas"
    7 user3@luiscarrera.pe  Sat Jan 27 17:40  29/847   "Re: aaaa"
    8 Mail Delivery System  Sat Jan 27 17:41  74/2241  "Undelivered Mail Returned to Sender"
 U  9 Mail Delivery System  Sat Jan 27 17:41  75/2242  "Undelivered Mail Returned to Sender"
 U 10 user1@luiscarrera.pe  Sat Jan 27 17:42  24/760   "Re: examen"
 U 11 user3@luiscarrera.pe  Sat Jan 27 17:43  28/846   "Re: aaaa"
   12 user9@luiscarrera.pe  Sat Jan 27 17:44  19/579   "quien es?"
   13 user3@luiscarrera.pe  Sat Jan 27 18:57  21/765   "enero"
   14 user3@luiscarrera.pe  Sat Jan 27 18:59  21/765   "enero"
   15 user3@luiscarrera.pe  Sat Jan 27 19:21  21/765   "enero"
   16 root                  Sat Jan 27 19:25  36/1556  "salida"
 U 17 user2@luiscarrera.pe  Sat Jan 27 19:25  37/1579  "salida"
   18 user3@luiscarrera.pe  Sat Jan 27 19:26  33/1329  "salida"
   19 user5@luiscarrera.pe  Sat Jan 27 19:27  49/1536  "Re: salida"
 U 20 user3@luiscarrera.pe  Sat Jan 27 19:28  33/1328  "salida"
>N 21 Mail Delivery System  Sat Feb  3 09:39  73/2395  "Undelivered Mail Returned to Sender"
 N 22 user2@luiscarrera.pe  Sat Feb  3 15:36  22/816   "salida"
& d
& h
    1 user3@luiscarrera.pe  Sat Jan 27 16:59  19/588   "examen"
    2 user3@luiscarrera.pe  Sat Jan 27 16:59  19/574   "aaaa"
    3 user3@luiscarrera.pe  Sat Jan 27 17:01  19/584   "examen final 2"
    4 Mail Delivery System  Sat Jan 27 17:07  74/2246  "Undelivered Mail Returned to Sender"
    5 Mail Delivery System  Sat Jan 27 17:07  72/2254  "Undelivered Mail Returned to Sender"
    6 lcarrera@luiscarrera  Sat Jan 27 17:36  25/796   "Re: Las fijas"
    7 user3@luiscarrera.pe  Sat Jan 27 17:40  29/847   "Re: aaaa"
    8 Mail Delivery System  Sat Jan 27 17:41  74/2241  "Undelivered Mail Returned to Sender"
 U  9 Mail Delivery System  Sat Jan 27 17:41  75/2242  "Undelivered Mail Returned to Sender"
 U 10 user1@luiscarrera.pe  Sat Jan 27 17:42  24/760   "Re: examen"
 U 11 user3@luiscarrera.pe  Sat Jan 27 17:43  28/846   "Re: aaaa"
   12 user9@luiscarrera.pe  Sat Jan 27 17:44  19/579   "quien es?"
   13 user3@luiscarrera.pe  Sat Jan 27 18:57  21/765   "enero"
   14 user3@luiscarrera.pe  Sat Jan 27 18:59  21/765   "enero"
   15 user3@luiscarrera.pe  Sat Jan 27 19:21  21/765   "enero"
   16 root                  Sat Jan 27 19:25  36/1556  "salida"
 U 17 user2@luiscarrera.pe  Sat Jan 27 19:25  37/1579  "salida"
   18 user3@luiscarrera.pe  Sat Jan 27 19:26  33/1329  "salida"
   19 user5@luiscarrera.pe  Sat Jan 27 19:27  49/1536  "Re: salida"
 U 20 user3@luiscarrera.pe  Sat Jan 27 19:28  33/1328  "salida"
>N 22 user2@luiscarrera.pe  Sat Feb  3 15:36  22/816   "salida"
& d 8
& h
    1 user3@luiscarrera.pe  Sat Jan 27 16:59  19/588   "examen"
    2 user3@luiscarrera.pe  Sat Jan 27 16:59  19/574   "aaaa"
    3 user3@luiscarrera.pe  Sat Jan 27 17:01  19/584   "examen final 2"
    4 Mail Delivery System  Sat Jan 27 17:07  74/2246  "Undelivered Mail Returned to Sender"
    5 Mail Delivery System  Sat Jan 27 17:07  72/2254  "Undelivered Mail Returned to Sender"
    6 lcarrera@luiscarrera  Sat Jan 27 17:36  25/796   "Re: Las fijas"
    7 user3@luiscarrera.pe  Sat Jan 27 17:40  29/847   "Re: aaaa"
>U  9 Mail Delivery System  Sat Jan 27 17:41  75/2242  "Undelivered Mail Returned to Sender"
 U 10 user1@luiscarrera.pe  Sat Jan 27 17:42  24/760   "Re: examen"
 U 11 user3@luiscarrera.pe  Sat Jan 27 17:43  28/846   "Re: aaaa"
   12 user9@luiscarrera.pe  Sat Jan 27 17:44  19/579   "quien es?"
   13 user3@luiscarrera.pe  Sat Jan 27 18:57  21/765   "enero"
   14 user3@luiscarrera.pe  Sat Jan 27 18:59  21/765   "enero"
   15 user3@luiscarrera.pe  Sat Jan 27 19:21  21/765   "enero"
   16 root                  Sat Jan 27 19:25  36/1556  "salida"
 U 17 user2@luiscarrera.pe  Sat Jan 27 19:25  37/1579  "salida"
   18 user3@luiscarrera.pe  Sat Jan 27 19:26  33/1329  "salida"
   19 user5@luiscarrera.pe  Sat Jan 27 19:27  49/1536  "Re: salida"
 U 20 user3@luiscarrera.pe  Sat Jan 27 19:28  33/1328  "salida"
 N 22 user2@luiscarrera.pe  Sat Feb  3 15:36  22/816   "salida"
& r 1
To: user2@luiscarrera.pe user3@luiscarrera.pe
Subject: Re: examen

user3@luiscarrera.pe wrote:

> el examen es mañana!!!!
?
saludos!!
.
EOT
&
Message  2:
From user3@luiscarrera.pe  Sat Jan 27 16:59:41 2018
Return-Path: <user3@luiscarrera.pe>
X-Original-To: user2
Delivered-To: user2@luiscarrera.pe
Date: Sat, 27 Jan 2018 16:59:41 -0500
To: user2@luiscarrera.pe
Subject: aaaa
User-Agent: Heirloom mailx 12.4 7/29/08
Content-Type: text/plain; charset=us-ascii
From: user3@luiscarrera.pe
Status: RO


New mail has arrived.
Loaded 1 new message
 N 23 user2@luiscarrera.pe  Sat Feb  3 15:38  24/774   "Re: examen"
& q
Held 21 messages in /var/spool/mail/user2
Tiene correo en /var/spool/mail/user2
[user2@luiscarrera ~]$ vi .mailrc
Tiene correo nuevo en /var/spool/mail/user2
[user2@luiscarrera ~]$ mail
Heirloom Mail version 12.4 7/29/08.  Type ? for help.
"/var/spool/mail/user2": 22 messages 1 new 8 unread
    1 user3@luiscarrera.pe  Sat Jan 27 16:59  19/588   "examen"
    2 user3@luiscarrera.pe  Sat Jan 27 16:59  19/574   "aaaa"
    3 user3@luiscarrera.pe  Sat Jan 27 17:01  19/584   "examen final 2"
    4 Mail Delivery System  Sat Jan 27 17:07  74/2246  "Undelivered Mail Returned to Sender"
    5 Mail Delivery System  Sat Jan 27 17:07  72/2254  "Undelivered Mail Returned to Sender"
    6 lcarrera@luiscarrera  Sat Jan 27 17:36  25/796   "Re: Las fijas"
    7 user3@luiscarrera.pe  Sat Jan 27 17:40  29/847   "Re: aaaa"
 U  8 Mail Delivery System  Sat Jan 27 17:41  75/2242  "Undelivered Mail Returned to Sender"
 U  9 user1@luiscarrera.pe  Sat Jan 27 17:42  24/760   "Re: examen"
 U 10 user3@luiscarrera.pe  Sat Jan 27 17:43  28/846   "Re: aaaa"
   11 user9@luiscarrera.pe  Sat Jan 27 17:44  19/579   "quien es?"
   12 user3@luiscarrera.pe  Sat Jan 27 18:57  21/765   "enero"
   13 user3@luiscarrera.pe  Sat Jan 27 18:59  21/765   "enero"
   14 user3@luiscarrera.pe  Sat Jan 27 19:21  21/765   "enero"
   15 root                  Sat Jan 27 19:25  36/1556  "salida"
 U 16 user2@luiscarrera.pe  Sat Jan 27 19:25  37/1579  "salida"
   17 user3@luiscarrera.pe  Sat Jan 27 19:26  33/1329  "salida"
   18 user5@luiscarrera.pe  Sat Jan 27 19:27  49/1536  "Re: salida"
 U 19 user3@luiscarrera.pe  Sat Jan 27 19:28  33/1328  "salida"
 U 20 user2@luiscarrera.pe  Sat Feb  3 15:36  23/826   "salida"
 U 21 user2@luiscarrera.pe  Sat Feb  3 15:38  25/784   "Re: examen"
>N 22 lcarrera@luiscarrera  Sat Feb  3 15:40  21/812   "examen"
& r 22
To: lcarrera@luiscarrera.pe user10@luiscarrera.pe user11@luiscarrera.pe
 user1@luiscarrera.pe user2@luiscarrera.pe user3@luiscarrera.pe
 user4@luiscarrera.pe user5@luiscarrera.pe user6@luiscarrera.pe
 user7@luiscarrera.pe user8@luiscarrera.pe user9@luiscarrera.pe
Subject: Re: examen

lcarrera@luiscarrera.pe wrote:

> El examen es la sgte clase
.
EOT
& ^CInterrupt
New mail has arrived.
Loaded 1 new message
 N 23 user2@luiscarrera.pe  Sat Feb  3 15:41  25/994   "Re: examen"
& q
Held 23 messages in /var/spool/mail/user2
Tiene correo en /var/spool/mail/user2
[user2@luiscarrera ~]$
[user2@luiscarrera ~]$ mail
Heirloom Mail version 12.4 7/29/08.  Type ? for help.
"/var/spool/mail/user2": 24 messages 1 new 9 unread
    1 user3@luiscarrera.pe  Sat Jan 27 16:59  19/588   "examen"
    2 user3@luiscarrera.pe  Sat Jan 27 16:59  19/574   "aaaa"
    3 user3@luiscarrera.pe  Sat Jan 27 17:01  19/584   "examen final 2"
    4 Mail Delivery System  Sat Jan 27 17:07  74/2246  "Undelivered Mail Returned to Sender"
    5 Mail Delivery System  Sat Jan 27 17:07  72/2254  "Undelivered Mail Returned to Sender"
    6 lcarrera@luiscarrera  Sat Jan 27 17:36  25/796   "Re: Las fijas"
    7 user3@luiscarrera.pe  Sat Jan 27 17:40  29/847   "Re: aaaa"
 U  8 Mail Delivery System  Sat Jan 27 17:41  75/2242  "Undelivered Mail Returned to Sender"
 U  9 user1@luiscarrera.pe  Sat Jan 27 17:42  24/760   "Re: examen"
 U 10 user3@luiscarrera.pe  Sat Jan 27 17:43  28/846   "Re: aaaa"
   11 user9@luiscarrera.pe  Sat Jan 27 17:44  19/579   "quien es?"
   12 user3@luiscarrera.pe  Sat Jan 27 18:57  21/765   "enero"
   13 user3@luiscarrera.pe  Sat Jan 27 18:59  21/765   "enero"
   14 user3@luiscarrera.pe  Sat Jan 27 19:21  21/765   "enero"
   15 root                  Sat Jan 27 19:25  36/1556  "salida"
 U 16 user2@luiscarrera.pe  Sat Jan 27 19:25  37/1579  "salida"
   17 user3@luiscarrera.pe  Sat Jan 27 19:26  33/1329  "salida"
   18 user5@luiscarrera.pe  Sat Jan 27 19:27  49/1536  "Re: salida"
 U 19 user3@luiscarrera.pe  Sat Jan 27 19:28  33/1328  "salida"
 U 20 user2@luiscarrera.pe  Sat Feb  3 15:36  23/826   "salida"
 U 21 user2@luiscarrera.pe  Sat Feb  3 15:38  25/784   "Re: examen"
   22 lcarrera@luiscarrera  Sat Feb  3 15:40  22/823   "examen"
 U 23 user2@luiscarrera.pe  Sat Feb  3 15:41  26/1004  "Re: examen"
>N 24 lcarrera@luiscarrera  Sat Feb  3 15:41  21/797   "test"
& r 24
To: lcarrera@luiscarrera.pe user10@luiscarrera.pe user11@luiscarrera.pe
 user1@luiscarrera.pe user2@luiscarrera.pe user3@luiscarrera.pe
 user4@luiscarrera.pe user5@luiscarrera.pe user6@luiscarrera.pe
 user7@luiscarrera.pe user8@luiscarrera.pe user9@luiscarrera.pe
Subject: Re: test

lcarrera@luiscarrera.pe wrote:

.
EOT
& q
New mail has arrived.
Held 24 messages in /var/spool/mail/user2
[user2@luiscarrera ~]$ mail
Heirloom Mail version 12.4 7/29/08.  Type ? for help.
"/var/spool/mail/user2": 25 messages 1 new 9 unread
    1 user3@luiscarrera.pe  Sat Jan 27 16:59  19/588   "examen"
    2 user3@luiscarrera.pe  Sat Jan 27 16:59  19/574   "aaaa"
    3 user3@luiscarrera.pe  Sat Jan 27 17:01  19/584   "examen final 2"
    4 Mail Delivery System  Sat Jan 27 17:07  74/2246  "Undelivered Mail Returned to Sender"
    5 Mail Delivery System  Sat Jan 27 17:07  72/2254  "Undelivered Mail Returned to Sender"
    6 lcarrera@luiscarrera  Sat Jan 27 17:36  25/796   "Re: Las fijas"
    7 user3@luiscarrera.pe  Sat Jan 27 17:40  29/847   "Re: aaaa"
 U  8 Mail Delivery System  Sat Jan 27 17:41  75/2242  "Undelivered Mail Returned to Sender"
 U  9 user1@luiscarrera.pe  Sat Jan 27 17:42  24/760   "Re: examen"
 U 10 user3@luiscarrera.pe  Sat Jan 27 17:43  28/846   "Re: aaaa"
   11 user9@luiscarrera.pe  Sat Jan 27 17:44  19/579   "quien es?"
   12 user3@luiscarrera.pe  Sat Jan 27 18:57  21/765   "enero"
   13 user3@luiscarrera.pe  Sat Jan 27 18:59  21/765   "enero"
   14 user3@luiscarrera.pe  Sat Jan 27 19:21  21/765   "enero"
   15 root                  Sat Jan 27 19:25  36/1556  "salida"
 U 16 user2@luiscarrera.pe  Sat Jan 27 19:25  37/1579  "salida"
   17 user3@luiscarrera.pe  Sat Jan 27 19:26  33/1329  "salida"
   18 user5@luiscarrera.pe  Sat Jan 27 19:27  49/1536  "Re: salida"
 U 19 user3@luiscarrera.pe  Sat Jan 27 19:28  33/1328  "salida"
 U 20 user2@luiscarrera.pe  Sat Feb  3 15:36  23/826   "salida"
 U 21 user2@luiscarrera.pe  Sat Feb  3 15:38  25/784   "Re: examen"
   22 lcarrera@luiscarrera  Sat Feb  3 15:40  22/823   "examen"
 U 23 user2@luiscarrera.pe  Sat Feb  3 15:41  26/1004  "Re: examen"
   24 lcarrera@luiscarrera  Sat Feb  3 15:41  22/808   "test"
>N 25 user2@luiscarrera.pe  Sat Feb  3 15:42  24/963   "Re: test"
&
Message 25:
From user2@luiscarrera.pe  Sat Feb  3 15:42:17 2018
Return-Path: <user2@luiscarrera.pe>
X-Original-To: user2@luiscarrera.pe
Delivered-To: user2@luiscarrera.pe
Date: Sat, 03 Feb 2018 15:42:17 -0500
To: user9@luiscarrera.pe, user8@luiscarrera.pe, user7@luiscarrera.pe,
 user6@luiscarrera.pe, user5@luiscarrera.pe, user4@luiscarrera.pe,
 user3@luiscarrera.pe, user2@luiscarrera.pe, user1@luiscarrera.pe,
 user11@luiscarrera.pe, user10@luiscarrera.pe, lcarrera@luiscarrera.pe
Subject: Re: test
User-Agent: Heirloom mailx 12.4 7/29/08
Content-Type: text/plain; charset=us-ascii
From: user2@luiscarrera.pe
Status: R

lcarrera@luiscarrera.pe wrote:


& q
Held 25 messages in /var/spool/mail/user2
[user2@luiscarrera ~]$ mail
Heirloom Mail version 12.4 7/29/08.  Type ? for help.
"/var/spool/mail/user2": 25 messages 8 unread
    1 user3@luiscarrera.pe  Sat Jan 27 16:59  19/588   "examen"
    2 user3@luiscarrera.pe  Sat Jan 27 16:59  19/574   "aaaa"
    3 user3@luiscarrera.pe  Sat Jan 27 17:01  19/584   "examen final 2"
    4 Mail Delivery System  Sat Jan 27 17:07  74/2246  "Undelivered Mail Returned to Sender"
    5 Mail Delivery System  Sat Jan 27 17:07  72/2254  "Undelivered Mail Returned to Sender"
    6 lcarrera@luiscarrera  Sat Jan 27 17:36  25/796   "Re: Las fijas"
    7 user3@luiscarrera.pe  Sat Jan 27 17:40  29/847   "Re: aaaa"
>U  8 Mail Delivery System  Sat Jan 27 17:41  75/2242  "Undelivered Mail Returned to Sender"
 U  9 user1@luiscarrera.pe  Sat Jan 27 17:42  24/760   "Re: examen"
 U 10 user3@luiscarrera.pe  Sat Jan 27 17:43  28/846   "Re: aaaa"
   11 user9@luiscarrera.pe  Sat Jan 27 17:44  19/579   "quien es?"
   12 user3@luiscarrera.pe  Sat Jan 27 18:57  21/765   "enero"
   13 user3@luiscarrera.pe  Sat Jan 27 18:59  21/765   "enero"
   14 user3@luiscarrera.pe  Sat Jan 27 19:21  21/765   "enero"
   15 root                  Sat Jan 27 19:25  36/1556  "salida"
 U 16 user2@luiscarrera.pe  Sat Jan 27 19:25  37/1579  "salida"
   17 user3@luiscarrera.pe  Sat Jan 27 19:26  33/1329  "salida"
   18 user5@luiscarrera.pe  Sat Jan 27 19:27  49/1536  "Re: salida"
 U 19 user3@luiscarrera.pe  Sat Jan 27 19:28  33/1328  "salida"
 U 20 user2@luiscarrera.pe  Sat Feb  3 15:36  23/826   "salida"
 U 21 user2@luiscarrera.pe  Sat Feb  3 15:38  25/784   "Re: examen"
   22 lcarrera@luiscarrera  Sat Feb  3 15:40  22/823   "examen"
 U 23 user2@luiscarrera.pe  Sat Feb  3 15:41  26/1004  "Re: examen"
   24 lcarrera@luiscarrera  Sat Feb  3 15:41  22/808   "test"
   25 user2@luiscarrera.pe  Sat Feb  3 15:42  25/974   "Re: test"
& d 3,4
Cannot determine parent Message-ID of the current message
& d 3
& d 4
& h
    1 user3@luiscarrera.pe  Sat Jan 27 16:59  19/588   "examen"
    2 user3@luiscarrera.pe  Sat Jan 27 16:59  19/574   "aaaa"
>   5 Mail Delivery System  Sat Jan 27 17:07  72/2254  "Undelivered Mail Returned to Sender"
    6 lcarrera@luiscarrera  Sat Jan 27 17:36  25/796   "Re: Las fijas"
    7 user3@luiscarrera.pe  Sat Jan 27 17:40  29/847   "Re: aaaa"
 U  8 Mail Delivery System  Sat Jan 27 17:41  75/2242  "Undelivered Mail Returned to Sender"
 U  9 user1@luiscarrera.pe  Sat Jan 27 17:42  24/760   "Re: examen"
 U 10 user3@luiscarrera.pe  Sat Jan 27 17:43  28/846   "Re: aaaa"
   11 user9@luiscarrera.pe  Sat Jan 27 17:44  19/579   "quien es?"
   12 user3@luiscarrera.pe  Sat Jan 27 18:57  21/765   "enero"
   13 user3@luiscarrera.pe  Sat Jan 27 18:59  21/765   "enero"
   14 user3@luiscarrera.pe  Sat Jan 27 19:21  21/765   "enero"
   15 root                  Sat Jan 27 19:25  36/1556  "salida"
 U 16 user2@luiscarrera.pe  Sat Jan 27 19:25  37/1579  "salida"
   17 user3@luiscarrera.pe  Sat Jan 27 19:26  33/1329  "salida"
   18 user5@luiscarrera.pe  Sat Jan 27 19:27  49/1536  "Re: salida"
 U 19 user3@luiscarrera.pe  Sat Jan 27 19:28  33/1328  "salida"
 U 20 user2@luiscarrera.pe  Sat Feb  3 15:36  23/826   "salida"
 U 21 user2@luiscarrera.pe  Sat Feb  3 15:38  25/784   "Re: examen"
   22 lcarrera@luiscarrera  Sat Feb  3 15:40  22/823   "examen"
 U 23 user2@luiscarrera.pe  Sat Feb  3 15:41  26/1004  "Re: examen"
   24 lcarrera@luiscarrera  Sat Feb  3 15:41  22/808   "test"
   25 user2@luiscarrera.pe  Sat Feb  3 15:42  25/974   "Re: test"
& h
    1 user3@luiscarrera.pe  Sat Jan 27 16:59  19/588   "examen"
    2 user3@luiscarrera.pe  Sat Jan 27 16:59  19/574   "aaaa"
>   5 Mail Delivery System  Sat Jan 27 17:07  72/2254  "Undelivered Mail Returned to Sender"
    6 lcarrera@luiscarrera  Sat Jan 27 17:36  25/796   "Re: Las fijas"
    7 user3@luiscarrera.pe  Sat Jan 27 17:40  29/847   "Re: aaaa"
 U  8 Mail Delivery System  Sat Jan 27 17:41  75/2242  "Undelivered Mail Returned to Sender"
 U  9 user1@luiscarrera.pe  Sat Jan 27 17:42  24/760   "Re: examen"
 U 10 user3@luiscarrera.pe  Sat Jan 27 17:43  28/846   "Re: aaaa"
   11 user9@luiscarrera.pe  Sat Jan 27 17:44  19/579   "quien es?"
   12 user3@luiscarrera.pe  Sat Jan 27 18:57  21/765   "enero"
   13 user3@luiscarrera.pe  Sat Jan 27 18:59  21/765   "enero"
   14 user3@luiscarrera.pe  Sat Jan 27 19:21  21/765   "enero"
   15 root                  Sat Jan 27 19:25  36/1556  "salida"
 U 16 user2@luiscarrera.pe  Sat Jan 27 19:25  37/1579  "salida"
   17 user3@luiscarrera.pe  Sat Jan 27 19:26  33/1329  "salida"
   18 user5@luiscarrera.pe  Sat Jan 27 19:27  49/1536  "Re: salida"
 U 19 user3@luiscarrera.pe  Sat Jan 27 19:28  33/1328  "salida"
 U 20 user2@luiscarrera.pe  Sat Feb  3 15:36  23/826   "salida"
 U 21 user2@luiscarrera.pe  Sat Feb  3 15:38  25/784   "Re: examen"
   22 lcarrera@luiscarrera  Sat Feb  3 15:40  22/823   "examen"
 U 23 user2@luiscarrera.pe  Sat Feb  3 15:41  26/1004  "Re: examen"
   24 lcarrera@luiscarrera  Sat Feb  3 15:41  22/808   "test"
   25 user2@luiscarrera.pe  Sat Feb  3 15:42  25/974   "Re: test"
New mail has arrived.
Loaded 1 new message
 N 26 lcarrera@luiscarrera  Sat Feb  3 15:43  38/1990  "test2"
&
Message  5:
From MAILER-DAEMON  Sat Jan 27 17:07:58 2018
Return-Path: <>
X-Original-To: user2@luiscarrera.pe
Delivered-To: user2@luiscarrera.pe
Date: Sat, 27 Jan 2018 17:07:58 -0500 (PET)
From: MAILER-DAEMON@luiscarrera.pe (Mail Delivery System)
Subject: Undelivered Mail Returned to Sender
To: user2@luiscarrera.pe
Auto-Submitted: auto-replied
Content-Type: multipart/report; report-type=delivery-status;
        boundary="557351C1F1D.1517090878/luiscarrera.pe"
Status: RO

Part 1:
Content-Description: Notification
Content-Type: text/plain; charset=us-ascii

This is the mail system at host luiscarrera.pe.

I'm sorry to have to inform you that your message could not
be delivered to one or more recipients. It's attached below.

For further assistance, please send mail to postmaster.

If you do so, please include this problem report. You can
delete your own text from the attached returned message.

                   The mail system

<who@luiscarrera.pe> (expanded from <who>): unknown user: "who"

Part 2:
Content-Description: Delivery report
Content-Type: message/delivery-status


Part 3:
Content-Description: Undelivered Message
Content-Type: message/rfc822

From user2@luiscarrera.pe Sat Jan 27 17:07:58 2018
Return-Path: <user2@luiscarrera.pe>
Date: Sat, 27 Jan 2018 17:07:58 -0500
To: who@luiscarrera.pe
User-Agent: Heirloom mailx 12.4 7/29/08
Content-Type: text/plain; charset=us-ascii
From: user2@luiscarrera.pe

& q
Held 24 messages in /var/spool/mail/user2
Tiene correo en /var/spool/mail/user2
[user2@luiscarrera ~]$ mail alumnos
Subject: lista
~r ! who
▒! who: No existe el fichero o el directorio
q
q
^C
(Interrupt -- one more to kill letter)
^C"/home/user2/dead.letter" 2/4
[user2@luiscarrera ~]$ mail
Heirloom Mail version 12.4 7/29/08.  Type ? for help.
"/var/spool/mail/user2": 26 messages 2 new 11 unread
    1 user3@luiscarrera.pe  Sat Jan 27 16:59  19/588   "examen"
    2 user3@luiscarrera.pe  Sat Jan 27 16:59  19/574   "aaaa"
    3 Mail Delivery System  Sat Jan 27 17:07  72/2254  "Undelivered Mail Returned to Sender"
    4 lcarrera@luiscarrera  Sat Jan 27 17:36  25/796   "Re: Las fijas"
    5 user3@luiscarrera.pe  Sat Jan 27 17:40  29/847   "Re: aaaa"
 U  6 Mail Delivery System  Sat Jan 27 17:41  75/2242  "Undelivered Mail Returned to Sender"
 U  7 user1@luiscarrera.pe  Sat Jan 27 17:42  24/760   "Re: examen"
 U  8 user3@luiscarrera.pe  Sat Jan 27 17:43  28/846   "Re: aaaa"
    9 user9@luiscarrera.pe  Sat Jan 27 17:44  19/579   "quien es?"
   10 user3@luiscarrera.pe  Sat Jan 27 18:57  21/765   "enero"
   11 user3@luiscarrera.pe  Sat Jan 27 18:59  21/765   "enero"
   12 user3@luiscarrera.pe  Sat Jan 27 19:21  21/765   "enero"
   13 root                  Sat Jan 27 19:25  36/1556  "salida"
 U 14 user2@luiscarrera.pe  Sat Jan 27 19:25  37/1579  "salida"
   15 user3@luiscarrera.pe  Sat Jan 27 19:26  33/1329  "salida"
   16 user5@luiscarrera.pe  Sat Jan 27 19:27  49/1536  "Re: salida"
 U 17 user3@luiscarrera.pe  Sat Jan 27 19:28  33/1328  "salida"
 U 18 user2@luiscarrera.pe  Sat Feb  3 15:36  23/826   "salida"
 U 19 user2@luiscarrera.pe  Sat Feb  3 15:38  25/784   "Re: examen"
   20 lcarrera@luiscarrera  Sat Feb  3 15:40  22/823   "examen"
 U 21 user2@luiscarrera.pe  Sat Feb  3 15:41  26/1004  "Re: examen"
   22 lcarrera@luiscarrera  Sat Feb  3 15:41  22/808   "test"
   23 user2@luiscarrera.pe  Sat Feb  3 15:42  25/974   "Re: test"
 U 24 lcarrera@luiscarrera  Sat Feb  3 15:43  39/2000  "test2"
>N 25 lcarrera@luiscarrera  Sat Feb  3 15:44  43/1706  "lista"
 N 26 user4@luiscarrera.pe  Sat Feb  3 15:44  44/2209  "Re: test2"
& r 25
To: lcarrera@luiscarrera.pe user10@luiscarrera.pe user11@luiscarrera.pe
 user1@luiscarrera.pe user2@luiscarrera.pe user3@luiscarrera.pe
 user4@luiscarrera.pe user5@luiscarrera.pe user6@luiscarrera.pe
 user7@luiscarrera.pe user8@luiscarrera.pe user9@luiscarrera.pe
Subject: Re: lista

lcarrera@luiscarrera.pe wrote:

> root     tty1         2018-02-03 09:41 (:0)
> root     pts/0        2018-02-03 09:41 (:0.0)
> root     pts/1        2018-02-03 09:49 (:0.0)
> user4    pts/3        2018-02-03 10:04 (172.17.3.252)
> user2    pts/4        2018-02-03 10:14 (172.17.2.219)
> user8    pts/5        2018-02-03 15:38 (172.17.2.227)
> user11   pts/6        2018-02-03 13:49 (172.17.2.216)
> user3    pts/7        2018-02-03 10:29 (172.17.3.220)
> user7    pts/8        2018-02-03 15:27 (172.17.2.231)
> user8    pts/9        2018-02-03 10:57 (172.17.2.227)
> user2    pts/10       2018-02-03 13:51 (172.17.2.219)
> user9    pts/11       2018-02-03 11:02 (172.17.2.226)
> user11   pts/12       2018-02-03 15:37 (172.17.2.216)
> user10   pts/13       2018-02-03 12:43 (172.17.2.233)
> user1    pts/2        2018-02-03 15:15 (172.17.2.217)
>    febrero de 2018
> lu ma mi ju vi sá do
>           1  2  3  4
>  5  6  7  8  9 10 11
> 12 13 14 15 16 17 18
> 19 20 21 22 23 24 25
> 26 27 28
>
h
q
^C
(Interrupt -- one more to kill letter)
^C"/home/user2/dead.letter" 27/1002
& q
Held 26 messages in /var/spool/mail/user2
Tiene correo en /var/spool/mail/user2
[user2@luiscarrera ~]$
[user2@luiscarrera ~]$ mail
Heirloom Mail version 12.4 7/29/08.  Type ? for help.
"/var/spool/mail/user2": 26 messages 10 unread
    1 user3@luiscarrera.pe  Sat Jan 27 16:59  19/588   "examen"
    2 user3@luiscarrera.pe  Sat Jan 27 16:59  19/574   "aaaa"
    3 Mail Delivery System  Sat Jan 27 17:07  72/2254  "Undelivered Mail Returned to Sender"
    4 lcarrera@luiscarrera  Sat Jan 27 17:36  25/796   "Re: Las fijas"
    5 user3@luiscarrera.pe  Sat Jan 27 17:40  29/847   "Re: aaaa"
>U  6 Mail Delivery System  Sat Jan 27 17:41  75/2242  "Undelivered Mail Returned to Sender"
 U  7 user1@luiscarrera.pe  Sat Jan 27 17:42  24/760   "Re: examen"
 U  8 user3@luiscarrera.pe  Sat Jan 27 17:43  28/846   "Re: aaaa"
    9 user9@luiscarrera.pe  Sat Jan 27 17:44  19/579   "quien es?"
   10 user3@luiscarrera.pe  Sat Jan 27 18:57  21/765   "enero"
   11 user3@luiscarrera.pe  Sat Jan 27 18:59  21/765   "enero"
   12 user3@luiscarrera.pe  Sat Jan 27 19:21  21/765   "enero"
   13 root                  Sat Jan 27 19:25  36/1556  "salida"
 U 14 user2@luiscarrera.pe  Sat Jan 27 19:25  37/1579  "salida"
   15 user3@luiscarrera.pe  Sat Jan 27 19:26  33/1329  "salida"
   16 user5@luiscarrera.pe  Sat Jan 27 19:27  49/1536  "Re: salida"
 U 17 user3@luiscarrera.pe  Sat Jan 27 19:28  33/1328  "salida"
 U 18 user2@luiscarrera.pe  Sat Feb  3 15:36  23/826   "salida"
 U 19 user2@luiscarrera.pe  Sat Feb  3 15:38  25/784   "Re: examen"
   20 lcarrera@luiscarrera  Sat Feb  3 15:40  22/823   "examen"
 U 21 user2@luiscarrera.pe  Sat Feb  3 15:41  26/1004  "Re: examen"
   22 lcarrera@luiscarrera  Sat Feb  3 15:41  22/808   "test"
   23 user2@luiscarrera.pe  Sat Feb  3 15:42  25/974   "Re: test"
 U 24 lcarrera@luiscarrera  Sat Feb  3 15:43  39/2000  "test2"
   25 lcarrera@luiscarrera  Sat Feb  3 15:44  44/1717  "lista"
 U 26 user4@luiscarrera.pe  Sat Feb  3 15:44  45/2219  "Re: test2"
& r 26
To: lcarrera@luiscarrera.pe user10@luiscarrera.pe user11@luiscarrera.pe
 user1@luiscarrera.pe user2@luiscarrera.pe user3@luiscarrera.pe
 user4@luiscarrera.pe user5@luiscarrera.pe user6@luiscarrera.pe
 user7@luiscarrera.pe user8@luiscarrera.pe user9@luiscarrera.pe
Subject: Re: test2

user4@luiscarrera.pe wrote:

> lcarrera@luiscarrera.pe wrote:
>
> >  15:43:05 up  6:04, 15 users,  load average: 0,19, 0,18, 0,22
> > USER     TTY      FROM              LOGIN@   IDLE   JCPU   PCPU WHAT
> > root     tty1     :0               09:41    6:04m  4:25   4:25  /usr/bin/Xorg :
> > root     pts/0    :0.0             09:41    3:35m  0.02s  0.02s bash
> > root     pts/1    :0.0             09:49    0.00s  0.19s  0.00s mail alumnos
> > user4    pts/3    172.17.3.252     10:04    2:08   0.96s  0.00s mail
> > user2    pts/4    172.17.2.219     10:14    1:56m  0.59s  0.59s -bash
> > user8    pts/5    172.17.2.227     15:38    5.00s  0.03s  0.03s -bash
> > user11   pts/6    172.17.2.216     13:49   25:51   0.64s  0.29s -bash
> > user3    pts/7    172.17.3.220     10:29   28:56   0.91s  0.91s -bash
> > user7    pts/8    172.17.2.231     15:27   10.00s  0.04s  0.00s mail
> > user8    pts/9    172.17.2.227     10:57   35:13   0.31s  0.02s vim messages
> > user2    pts/10   172.17.2.219     13:51    6.00s  0.67s  0.00s mail
> > user9    pts/11   172.17.2.226     11:02    3.00s  1.69s  0.03s vim .mailrc
> > user11   pts/12   172.17.2.216     15:37   15.00s  0.08s  0.00s mail
> > user10   pts/13   172.17.2.233     12:43   45.00s  0.92s  0.00s mail
> > user1    pts/2    172.17.2.217     15:15    1:03   0.03s  0.00s mail
> > q
>
> q
mail
^C
(Interrupt -- one more to kill letter)
^C"/home/user2/dead.letter" 25/1353
& q
Held 26 messages in /var/spool/mail/user2
[user2@luiscarrera ~]$
[user2@luiscarrera ~]$ mail alumnos
Subject: Lista
~r ! who
~e ! cal
838
.
user9    pts/2        2018-02-03 15:44 (172.17.2.226)
.
user9    pts/2        2018-02-03 15:44 (172.17.2.226)
q
(continue)
q
.
EOT
Tiene correo en /var/spool/mail/user2
[user2@luiscarrera ~]$ h
-bash: h: no se encontró la orden
[user2@luiscarrera ~]$ maiñ
-bash: maiñ: no se encontró la orden
[user2@luiscarrera ~]$ mail
Heirloom Mail version 12.4 7/29/08.  Type ? for help.
"/var/spool/mail/user2": 26 messages 9 unread
    1 user3@luiscarrera.pe  Sat Jan 27 16:59  19/588   "examen"
    2 user3@luiscarrera.pe  Sat Jan 27 16:59  19/574   "aaaa"
    3 Mail Delivery System  Sat Jan 27 17:07  72/2254  "Undelivered Mail Returned to Sender"
    4 lcarrera@luiscarrera  Sat Jan 27 17:36  25/796   "Re: Las fijas"
    5 user3@luiscarrera.pe  Sat Jan 27 17:40  29/847   "Re: aaaa"
>U  6 Mail Delivery System  Sat Jan 27 17:41  75/2242  "Undelivered Mail Returned to Sender"
 U  7 user1@luiscarrera.pe  Sat Jan 27 17:42  24/760   "Re: examen"
 U  8 user3@luiscarrera.pe  Sat Jan 27 17:43  28/846   "Re: aaaa"
    9 user9@luiscarrera.pe  Sat Jan 27 17:44  19/579   "quien es?"
   10 user3@luiscarrera.pe  Sat Jan 27 18:57  21/765   "enero"
   11 user3@luiscarrera.pe  Sat Jan 27 18:59  21/765   "enero"
   12 user3@luiscarrera.pe  Sat Jan 27 19:21  21/765   "enero"
   13 root                  Sat Jan 27 19:25  36/1556  "salida"
 U 14 user2@luiscarrera.pe  Sat Jan 27 19:25  37/1579  "salida"
   15 user3@luiscarrera.pe  Sat Jan 27 19:26  33/1329  "salida"
   16 user5@luiscarrera.pe  Sat Jan 27 19:27  49/1536  "Re: salida"
 U 17 user3@luiscarrera.pe  Sat Jan 27 19:28  33/1328  "salida"
 U 18 user2@luiscarrera.pe  Sat Feb  3 15:36  23/826   "salida"
 U 19 user2@luiscarrera.pe  Sat Feb  3 15:38  25/784   "Re: examen"
   20 lcarrera@luiscarrera  Sat Feb  3 15:40  22/823   "examen"
 U 21 user2@luiscarrera.pe  Sat Feb  3 15:41  26/1004  "Re: examen"
   22 lcarrera@luiscarrera  Sat Feb  3 15:41  22/808   "test"
   23 user2@luiscarrera.pe  Sat Feb  3 15:42  25/974   "Re: test"
 U 24 lcarrera@luiscarrera  Sat Feb  3 15:43  39/2000  "test2"
   25 lcarrera@luiscarrera  Sat Feb  3 15:44  44/1717  "lista"
   26 user4@luiscarrera.pe  Sat Feb  3 15:44  45/2220  "Re: test2"
& r 25
To: lcarrera@luiscarrera.pe user10@luiscarrera.pe user11@luiscarrera.pe
 user1@luiscarrera.pe user2@luiscarrera.pe user3@luiscarrera.pe
 user4@luiscarrera.pe user5@luiscarrera.pe user6@luiscarrera.pe
 user7@luiscarrera.pe user8@luiscarrera.pe user9@luiscarrera.pe
Subject: Re: lista

lcarrera@luiscarrera.pe wrote:

> root     tty1         2018-02-03 09:41 (:0)
> root     pts/0        2018-02-03 09:41 (:0.0)
> root     pts/1        2018-02-03 09:49 (:0.0)
> user4    pts/3        2018-02-03 10:04 (172.17.3.252)
> user2    pts/4        2018-02-03 10:14 (172.17.2.219)
> user8    pts/5        2018-02-03 15:38 (172.17.2.227)
> user11   pts/6        2018-02-03 13:49 (172.17.2.216)
> user3    pts/7        2018-02-03 10:29 (172.17.3.220)
> user7    pts/8        2018-02-03 15:27 (172.17.2.231)
> user8    pts/9        2018-02-03 10:57 (172.17.2.227)
> user2    pts/10       2018-02-03 13:51 (172.17.2.219)
> user9    pts/11       2018-02-03 11:02 (172.17.2.226)
> user11   pts/12       2018-02-03 15:37 (172.17.2.216)
> user10   pts/13       2018-02-03 12:43 (172.17.2.233)
> user1    pts/2        2018-02-03 15:15 (172.17.2.217)
>    febrero de 2018
> lu ma mi ju vi sá do
>           1  2  3  4
>  5  6  7  8  9 10 11
> 12 13 14 15 16 17 18
> 19 20 21 22 23 24 25
> 26 27 28
>
q







q
.
EOT
& q
New mail has arrived.
Held 26 messages in /var/spool/mail/user2
[user2@luiscarrera ~]$ mail
Heirloom Mail version 12.4 7/29/08.  Type ? for help.
"/var/spool/mail/user2": 27 messages 1 new 10 unread
    1 user3@luiscarrera.pe  Sat Jan 27 16:59  19/588   "examen"
    2 user3@luiscarrera.pe  Sat Jan 27 16:59  19/574   "aaaa"
    3 Mail Delivery System  Sat Jan 27 17:07  72/2254  "Undelivered Mail Returned to Sender"
    4 lcarrera@luiscarrera  Sat Jan 27 17:36  25/796   "Re: Las fijas"
    5 user3@luiscarrera.pe  Sat Jan 27 17:40  29/847   "Re: aaaa"
 U  6 Mail Delivery System  Sat Jan 27 17:41  75/2242  "Undelivered Mail Returned to Sender"
 U  7 user1@luiscarrera.pe  Sat Jan 27 17:42  24/760   "Re: examen"
 U  8 user3@luiscarrera.pe  Sat Jan 27 17:43  28/846   "Re: aaaa"
    9 user9@luiscarrera.pe  Sat Jan 27 17:44  19/579   "quien es?"
   10 user3@luiscarrera.pe  Sat Jan 27 18:57  21/765   "enero"
   11 user3@luiscarrera.pe  Sat Jan 27 18:59  21/765   "enero"
   12 user3@luiscarrera.pe  Sat Jan 27 19:21  21/765   "enero"
   13 root                  Sat Jan 27 19:25  36/1556  "salida"
 U 14 user2@luiscarrera.pe  Sat Jan 27 19:25  37/1579  "salida"
   15 user3@luiscarrera.pe  Sat Jan 27 19:26  33/1329  "salida"
   16 user5@luiscarrera.pe  Sat Jan 27 19:27  49/1536  "Re: salida"
 U 17 user3@luiscarrera.pe  Sat Jan 27 19:28  33/1328  "salida"
 U 18 user2@luiscarrera.pe  Sat Feb  3 15:36  23/826   "salida"
 U 19 user2@luiscarrera.pe  Sat Feb  3 15:38  25/784   "Re: examen"
   20 lcarrera@luiscarrera  Sat Feb  3 15:40  22/823   "examen"
 U 21 user2@luiscarrera.pe  Sat Feb  3 15:41  26/1004  "Re: examen"
   22 lcarrera@luiscarrera  Sat Feb  3 15:41  22/808   "test"
   23 user2@luiscarrera.pe  Sat Feb  3 15:42  25/974   "Re: test"
 U 24 lcarrera@luiscarrera  Sat Feb  3 15:43  39/2000  "test2"
   25 lcarrera@luiscarrera  Sat Feb  3 15:44  44/1717  "lista"
   26 user4@luiscarrera.pe  Sat Feb  3 15:44  45/2220  "Re: test2"
>N 27 user2@luiscarrera.pe  Sat Feb  3 15:47  56/1942  "Re: lista"
& r 27
To: lcarrera@luiscarrera.pe user10@luiscarrera.pe user11@luiscarrera.pe
 user1@luiscarrera.pe user2@luiscarrera.pe user3@luiscarrera.pe
 user4@luiscarrera.pe user5@luiscarrera.pe user6@luiscarrera.pe
 user7@luiscarrera.pe user8@luiscarrera.pe user9@luiscarrera.pe
Subject: Re: lista

user2@luiscarrera.pe wrote:

> lcarrera@luiscarrera.pe wrote:
>
> > root     tty1         2018-02-03 09:41 (:0)
> > root     pts/0        2018-02-03 09:41 (:0.0)
> > root     pts/1        2018-02-03 09:49 (:0.0)
> > user4    pts/3        2018-02-03 10:04 (172.17.3.252)
> > user2    pts/4        2018-02-03 10:14 (172.17.2.219)
> > user8    pts/5        2018-02-03 15:38 (172.17.2.227)
> > user11   pts/6        2018-02-03 13:49 (172.17.2.216)
> > user3    pts/7        2018-02-03 10:29 (172.17.3.220)
> > user7    pts/8        2018-02-03 15:27 (172.17.2.231)
> > user8    pts/9        2018-02-03 10:57 (172.17.2.227)
> > user2    pts/10       2018-02-03 13:51 (172.17.2.219)
> > user9    pts/11       2018-02-03 11:02 (172.17.2.226)
> > user11   pts/12       2018-02-03 15:37 (172.17.2.216)
> > user10   pts/13       2018-02-03 12:43 (172.17.2.233)
> > user1    pts/2        2018-02-03 15:15 (172.17.2.217)
> >    febrero de 2018
> > lu ma mi ju vi sá do
> >           1  2  3  4
> >  5  6  7  8  9 10 11
> > 12 13 14 15 16 17 18
> > 19 20 21 22 23 24 25
> > 26 27 28
> >
> q
>
>
>
>
>
>
>
> q
.
EOT
& h
    1 user3@luiscarrera.pe  Sat Jan 27 16:59  19/588   "examen"
    2 user3@luiscarrera.pe  Sat Jan 27 16:59  19/574   "aaaa"
    3 Mail Delivery System  Sat Jan 27 17:07  72/2254  "Undelivered Mail Returned to Sender"
    4 lcarrera@luiscarrera  Sat Jan 27 17:36  25/796   "Re: Las fijas"
    5 user3@luiscarrera.pe  Sat Jan 27 17:40  29/847   "Re: aaaa"
 U  6 Mail Delivery System  Sat Jan 27 17:41  75/2242  "Undelivered Mail Returned to Sender"
 U  7 user1@luiscarrera.pe  Sat Jan 27 17:42  24/760   "Re: examen"
 U  8 user3@luiscarrera.pe  Sat Jan 27 17:43  28/846   "Re: aaaa"
    9 user9@luiscarrera.pe  Sat Jan 27 17:44  19/579   "quien es?"
   10 user3@luiscarrera.pe  Sat Jan 27 18:57  21/765   "enero"
   11 user3@luiscarrera.pe  Sat Jan 27 18:59  21/765   "enero"
   12 user3@luiscarrera.pe  Sat Jan 27 19:21  21/765   "enero"
   13 root                  Sat Jan 27 19:25  36/1556  "salida"
 U 14 user2@luiscarrera.pe  Sat Jan 27 19:25  37/1579  "salida"
   15 user3@luiscarrera.pe  Sat Jan 27 19:26  33/1329  "salida"
   16 user5@luiscarrera.pe  Sat Jan 27 19:27  49/1536  "Re: salida"
 U 17 user3@luiscarrera.pe  Sat Jan 27 19:28  33/1328  "salida"
 U 18 user2@luiscarrera.pe  Sat Feb  3 15:36  23/826   "salida"
 U 19 user2@luiscarrera.pe  Sat Feb  3 15:38  25/784   "Re: examen"
   20 lcarrera@luiscarrera  Sat Feb  3 15:40  22/823   "examen"
 U 21 user2@luiscarrera.pe  Sat Feb  3 15:41  26/1004  "Re: examen"
   22 lcarrera@luiscarrera  Sat Feb  3 15:41  22/808   "test"
   23 user2@luiscarrera.pe  Sat Feb  3 15:42  25/974   "Re: test"
 U 24 lcarrera@luiscarrera  Sat Feb  3 15:43  39/2000  "test2"
   25 lcarrera@luiscarrera  Sat Feb  3 15:44  44/1717  "lista"
   26 user4@luiscarrera.pe  Sat Feb  3 15:44  45/2220  "Re: test2"
>  27 user2@luiscarrera.pe  Sat Feb  3 15:47  56/1942  "Re: lista"
New mail has arrived.
Loaded 1 new message
 N 28 user2@luiscarrera.pe  Sat Feb