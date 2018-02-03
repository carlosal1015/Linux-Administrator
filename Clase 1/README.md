## LINUX ##
[![N|Solid](http://apprize.info/linux/pic.jpg)](https://nodesource.com/products/nsolid)


Sistema operativo que replica las caracteristicas del sistema operativo UNIX
Sistema operativo
        Programa que se encarga de administrar los recursos de un sistema de computo, tales como: cpu, ram, disco duros etc...

Caracteristicas
        -Multitarea
          Capacidad de realizar multiples procesos simultanemamente.
        -Multiusuario
          Capacidad de ejecutar los procesos de multiples usuarios
          simultaneamente
        -Mutiplataforma
          Capacidad de ejecutar el sistema operativo en diferentes
         plataformas de hardware (intel,risc,sparc)


Linux consiste, solamente en el nucleo del sistema operativo, si a este nucleo le añadimos un conjunto de aplicaciones, creamos una distribuciòn tal como redhat, fedora, centos, debian, ubuntu, slackware, mandriva etc...

Sistema de computo.
Sistema que permite realizar tareas de procesamiento de datos, consisten basicamente en cpU (Unidad central de proceso), RAM (memoria de acceso aleatorio) y disco duro (sistema de archivos).
EL acceso a un sistema de computo, requiere que se tenga asignado un usuario y una contraseña de acceso.
EL acceso pueder ser:
        Local
          EL usuario se encuentra frente al teclado y monitor conectado directamente al sistema.
Remoto
EL usuario accede a travez de un terminal fisico o un emulador de terminal.
Los terminales fisicos se conecta al puerto de comunicaciones del sistema de computo su extension (cuan separado esta el terminal del sistema de computo) es limitado generalmente una decena de metros y obliga el uso de repetidores.
Los emuladores de terminal son programas que se ejecutan en cualquier sistema operativo, el unico requisito es que el sistema tenga conigurado el lenguaje de comunicaciòn de red tcp/ip, el emulador se conectara al sistema de computo usando los protocolos telnet (en desuso) o ssh para iniciar una sesion remota, a partir de aqui el comportamiento es igual como si estuviera conectado directamente al sistema de computo.

tcp/ip
Servicio  Puerto de acceso
http            80
https           443
ssh             22
telnet          23

/etc/services


Acceso al servidor

IP : 172.17.2.229
usuario : userx
clave : userx


Comandos bàsicos
id
  Identificacion del usuario
date
  Fecha y hora del sistema
cal
  calendario del mes en curso
who
  Muestra la lista de usuarios
w
  Muestra la lista de usuarios
cat
  Muestra el contenido del archivo
head
  Muestra las 10 primeras lineas del archivo
tail
  Muestra las 10 ultimas lineas del archivo
grep
  Extrae lineas de un archivo que contengan una cadena especifica o expresio regular
cut
  Extrae columnas de un archivo o campos de un archivo de texto delimitado,el delimitador se indica con la opcion d
wc (word count)
  Cuenta el numero de linea, palabras, caracteres de un archivo de texto
write
   Envia un mensaje al terminal del usuario
talk
   Inicia un chat entre dos usuarios activos

   Procedemiento:
   1.- El usuario A inicia una conversacion con el usuario B

       talk B

    2.-El usuario B recibe una invitacion para el chat, entonces debe responder con:

        talk A

    3.- Se inicia la conversaciòn-

mail
  Envia mensajes entre usuarios del sistema que no esten en linea. los mensajes son almacenados en el mailbox del usuario, los cuales podran ser leidos con el mismo comando mail.

        mail nombreUsuario
        subject: mensaje
        mensaje de prueba
        .

Para terminar la edicion del mensaje y enviarlo, debemos incluir un punto al inicio de una linea en blanco.

Para lee el correo se utiliza el comando mail:


[lcarrera@luiscarrera ~]$ mail
Heirloom Mail version 12.4 7/29/08.  Type ? for help.
"/var/spool/mail/lcarrera": 3 messages
>   1 user7@luiscarrera.pe  Sat Jan 27 17:00  19/586   "Mensaje"
    2 user2@luiscarrera.pe  Sat Jan 27 17:03  19/599   "Las fijas"
    3 user3@luiscarrera.pe  Sat Jan 27 17:04  19/590   "linux"
&

El simbolo > indica el correo "activo"
Los comandos se escriben luego del simbolo &.
Si se presiona la tencla enter se ve el contenenido del mensaje activo
Si se presiona un numero, se vera el contenido del mensaje identificado con ese numero.
Para responder se utiliza la tecka R y el numero del mensaje


Archivo /etc/passwd
Este archivo contiene la informacion de los usuarios que pueden acceder al sistema, es un archivo de texto delimitado, donde el delimitador es el caracter :

Formato

      dovenull:x:495:491:Dovecot's unauthorized user:/usr/libexec/dovecot:/sbin/nologin
         |     |  |   |                 |                      |                |
         |     | uid gid                |                      |                |
         |     |                        |            Directorio Hogar   Programa de inicio
         |   clave        Comentario o campo GECOS
         |
nombre del usuario

SHELL
Programa que permite la interacciòn del usuario con el sistema operativo para ejecutar las tareas de: ejecutar comandos.
Los comandos son archivos almancenados en el sistema de archivos, generalmamente en las carpetas /bin,/usr/bin,/usr/local/bin, /usr/bin.

Para que un programa sea considerado como un shell, debe tener las sgtes caracteristicas:
1.- Debe proporcionar una linea de comandos, y realizar su analisis.
2.- Debe realizar la expansion de variables.
3.- Debe proporcinar substitucion de nombres de archivo.
4.- Debe implementar la redirecciòn de entrada y salida.
5.- Debe proporcionar un lenguaje de programacion interpretado.

Ejemplos: sh, bash, csh, zsh, csh.....

1.- Linea de comandos
    La linea de comandos està compuesta por:

    prompt comando opciones enter

    Donde:
        prompt
           Cadena de de texto que le indica al usuario que el shell està esperando por sus ordenes.
           Por regla general si el prompt acaba en $ el usuario es un usuario normal.
           Si el prompt acaba en # el usuario es un superusuario (root)
           Existen tambien prompts secundarios, que indican que el shell esta esperando que se digite
           la linea completa del comando.
        comando
           Nombre del comando que se quiere ejecutar
        opciones
           Caracteres precedidos de guion que afecta el comportamiento del comando.
        enter
           Digitalizacion de la tecla enter que le indica al shell que se termino de scribir el comando.

    AL finalizar de escribir el comando el shell pasa a analizar la linea de comando en busca de caracteres especiales
    para realizar las tareas indicadas respectivamente.

2.- Expansion de variables
    Tarea de reemplazar el nombre de una variable por su contenido.
    Variables predefinidas
    USER (nombre de usuario)
    PWD  (Directorio de trabajo)
    PS1='[\u@\h \W]\$ '  (prompt principal.

3.- Substituciòn de nombres de archivo
    permite manipular varios archivos codificando sus nombres con expresiones regulares simples.

    Para este proposito el shell utiliza estos caracteres:

        *       cualquier cadena de caracteres
        ?       un caracter
        [a-z]   un caracter del rango
        [^a-z]  un caracter excepto los del rango
        [adhjf] un caracter de los especificados
        [^dhjf] un caracter excepto los especificados.

4.- Redireccion de entrada y salida.
    Premisa de diseño:
                        Todo y absolutamente todo es una archivo.

    EL sistema operativo considera que los elementos de hardware son archivos y por lo tanto estaran representados como
    archivos en el directorio dev

    Al lanzar un comando y este obtiene memoria y tiempo de ejecucion decimos que hemos creado un proceso.

    AL ser creado un proceso este recibe tres archivos: archivo de entrada de datos (stdin), archivo de salida de datos
    (stdout) y archivo de salida de error (stderr) identificados por los descriptores de archivo 0, 1, y 2 respectivamente.




                              (0)>--------proceso-------->(1)
                        stdin                |          stdout
                                             |
                                             |
                                             |
                                            (2)
                                           stderr


     EL shell inicialmente enlaza estos tres descriptores al terminal del usuario de manera que si el proceso requiere datos, los toma del terminal, si genera algun resultado, lo guarda en el terminal y si genera algùn mensaje de erros lo guarda en el terminal.

LA redireccion de entrada y salida es la forma mediante la cual el shell permite que los archivos antes mencionados sean redireccionados a otros archivos.

REDIRECCION DE SALIDA
                                comando > archivo
                                comando >> archivo

REDIRECCION DE ENTRADA
                                comando < archivo
                                comando <<ETIQUETA

                                LA etiqueta indica el fin de la entrada de datos (EOF)

REDIRECCION ENTRE COMANDOS.

                                comando1 | comando2 | comando3 |..........|comandoN

                                La salida del comando1 se toma como entrada para el comando2
                                la salida del comando2 se toma como entrada para el comando3
                                .....


                                comando2 `comando1`

                                la salida del comando1 se toma como parametro del comando2


SISTEMA DE ARCHIVOS

Es la parte del sistema operativo encargada del almacenamiento y recuperaciòn de los datos de un medio fisico (cintas, discos duros, discos portatiles, cds etc)

Archivo
        Secuencia de bits.

La definiciòn de archivo en unix no contempla analisis ni reconocimiento del contenido, es por eso, que en UNIX no existe el concepto de extension en el nombre de archivo

Nomnbre de archivo
        Secuencia de caracteres alfanumericos que sirve como identificador del archivo para el usuario.

i-nodo
        Estructura de datos que almacena las propiedades del archivo, esta estructura se identifica con un # proporcionado por el sistema y es la unica forma como el SA reconoce a un archivo.

Propiedades almacenadas en el i-nodo:
        tipo de archivo
        permisos del archivo
        # de enlaces
        uid del dueño del archivo
        gid del grupo principal del dueño
        tamaño en bytes
        fecha y hora de ultima actualizacion
        Fecha y hora de ultima modificacion
        Fecha y hora de creacion
        lista de blocks

Enlace
        Relacion entre el i-nodo y el nombre del archivo.

Tipos de archivos
Archivo regular (-)
        Archivo que contiene cualquier flujo de bits
Directorio (d)
        Archivo que contiene enlaces, al crea un directorio, este ya tiene dos enlaces almacenados,
        el enlace . y el enlace .. que identifican los i-nodos del directorio actual y el directorio
        padre respectivamente.
        EL comando que crea directorios es el comando mkdir (make directory)
Enlace simbolico (l)
        Enlace simbolico, es un tipo de archivo que almacena un "puntero" hacia otro archivo, es util para poder
        crear referencias a directorios y a archivos que se encuentran en otra partición.
        El comando que crea enlaces simbolicos es el comando ln.
Archivos de dispositivos
Dispositivo de bloques (b)
        Utiliza un area de memoria intermedia (buffer) para comunicarse con el SO, la comunicación se realiza en
        unidades de buffer
Dispositivo de caracteres
        Se comunica con el SO enviando serie de caracteres (caracter por caracter).
Archivos de comunicación entre procesos
Tuberia con nombre (p)
        Permite la comunicación entre procesos de manera asincrona, El primer proceso almacena información en la
        tuberia, esta información se mantiene en la tuberia hasta que el segundo proceso la extrae, quedando entoces
        la tuberia vacia.
Sockets (s)
        Permite la comunicación entre procesos de manera sincrona, los sockets se crean utilizando librerias de
        programación.


ENLACES

                nombreAarchivo-------------->#i-nodo
                                                 ^
                nombreArchivo2-------------------|

SAlida del comando ls

        -rw-rw-r--. 2 lcarrera lcarrera 1153 feb  3 10:59 enero
        |    |      |   |          |      |       |         |
    tipo de  |      | dueño     grupo     |   ´ultima       ----------nombre
     archivo |      #                     |    modificacion
             |  enlaces                   |
             |                     tamaño en bytes
        cadena de
        permisos

Comandos del sistema de archivos

ls (list)
        Lista el contenido del directorio
        Opciones
        -l      lista propiedades
        -i      lista i-nodos
        -a      muestra los archivos oculto (su nombre inicia con .)
        -R      Inicia un listado recursivo

mkdir (make directory)
        Crea un directorio
        Opciones
        -p      crea los subdirectorios faltantes

rmdir (remove directory)
        Elimina un directorio, siempre y cuando este vacio
        Opciones
        -r      Elimina el directorio y los susbdirectorios,aun si no estan vacios.

rm (remove)
        ELimina un archivo
        Opciones
        -r      Ejecuta un borrado recursivo (si dentro de la lista de archivos a borrar hay un directorio
                ingresa al directorio y borra los archivos)

cp (copy)
        Sintaxis:
                cp origen destino
        Copia el archivo origen como el archivo destino.
        Opciones
        -r      Inicia una copia recursiva

mv (move)
        Sintaxis;
                mv origen destino

        Mueve un archivo de una ubicación a otra

pwd (program work directory)
        Indica la ruta actual

cd  (change directory)
        Cambia de direcorio




Arbol de directorios
        EL sistema de archivo está organizado en una estructura de árbol invertido, siendo la raiz el directorio padre
        identificado por el simbolo / debajo del cual existe un conjunto de directorios con un uso especifico:


                                                           / raiz (root)
                                                           |
                                                           |
        ---------------------------------------------------------------------------------------------------------------
        |       |       |       |       |       |       |       |       |       |       |
        |       |       |       |       |       |       |       |       |       |       |
        |       |       |       |       |       |       |       |       |       |       |
        /boot   /etc    /dev    /bin    /sbin   /home   /tmp    /usr    /var    /proc   /opt


Usos
        boot
             Contiene los archivos necesarios para iniciar el SO
        etc
             Contiene los archivos de configuracion del sistema y los servicios
        dev
             Contiene la representación como archivo de los dispositivos.
        bin
             Contienen los ejecutables basicos del usuario
        sbin
             Contiene los ejecutables basicos de administracion
        home
             Contiene los directorios hogar de los usuarios
        tmp
             Contiene los archivos temporales del sistema
        usr
             Contiene la estructura de archivos para las aplicaciones y servicios del sistema
        var
             Contiene los archivos de registro y de ejecucion de los servicios.
        proc
             Imagen del contenido de la memoria
        opt
             Parecido a usr muy comun en distribuciones como SuSE

RUTA O PATH
        Es la secuencia de directorios que se deben recorrer desde la raiz hasta llegar al archivo.

        Ruta absoluta
          PArte desde la raiz

                /directorio1/directorio2/directorio3/..........

         Ruta relativa
          PArte del pwd
                Abreviaturas
                                .               Directorio actual
                                ..              Directorio padre
