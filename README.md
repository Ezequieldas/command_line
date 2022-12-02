WILDCARDS

Las wildcards o comodines son una serie de caracteres especiales que nos permiten encontrar patrones o realizar búsquedas más avanzadas. Es aplicable para archivos y directorios.

Las wildcards te sirven para realizar seccionamiento de archivos o directorios, ademas de ls los wildcards tambien pueden usarse con cualquier comando que realice la manipulación de archivos como mv, cp y rm.

Tipos de wildcards
Buscar todo (*)
El asterisco te ayuda a buscar toda la información dentro de una carpeta, pero puedes limitar su uso. Si por ejemplo quieres buscar los archivos que tengan una extensión “.png”, escribes:

`ls -l *.png`

image.png

También lo puedes poner al final, si quisieras buscar, todos los archivos que comiencen por unos caracteres específicos, entonces escribes esos caracteres y luego el asterisco.

Por ejemplo, si quisieras buscar todos los archivos que comiencen por “fotosDe”, habría que escribir:

`ls -l fotoDe*`

image.png
Buscar por cantidad de caracteres (?)
Si dentro de tus archivos tuvieras una especie de código para guardar tus fotos, algo así como “foto1.png”, “foto2.png”, “foto3.png”, etc. En este caso, sabemos que primero tenemos el string “foto”, luego un solo número y por último la extensión “.png”.

Si quisieras buscar esas fotos escribirías:

`ls -l foto?.png`

image.png
Aquí estás indicando:

Busca todo lo que comience por la cadena de caracteres “foto”
Que inmediatamente después tenga un solo caracter
Y que al final tenga la cadena de caracteres “.png”
Pero si sabes que no tiene un solo caracter, sino que tiene varios, entonces escribes tantos signos de interrogación como caracteres existan. Por ejemplo, si quieres buscar las fotos que tengan esta estructura “foto11.jpg”, escribes:

`ls -l foto??.jpg`

image.png
También puedes combinar wildcards. Por ejemplo, si sabes que tus fotos siguen esta especie de código, pero no sabes que extensión tienen, escribes:

`ls -l foto?.*`

image.png
Aquí estás indicando:

Busca todo lo que comience por “foto”
Que inmediatamente después tenga un solo caracter
Y que tenga lo que sea después del punto
Buscar por caracteres específicos ([])
Si quieres buscar por varios caracteres específicos se usan corchetes. Para utilizarlos tienes que colocar dentro de los corchetes los caracteres que quieres buscar.

Por ejemplo, si quisieras buscar los archivos que comiencen por las letras “c” o “i”, entonces escribes:

`ls -l [ci]*`

image.png
Lo que indica el comando es que busque los archivos que comiencen por la letra “c” o por la letra “i” y que tengan lo que sea por delante. Cuando buscamos con esta wildcard ten en cuenta que es case sensitive, por lo que la letra “i” no es lo mismo que la letra “I”.

`ls -l [cCiI]*`

image.png
Por último, si quieres buscar por rango de números también tienes que usar esta wildcard. Para hacerlo, escribe el rango de números que quieres buscar separados por un guion.

`ls -l foto[2-6]*`

image.png
Lo que indica ese comando es:

Busca todo lo que comience por la cadena de texto “foto”
Que justo después tenga un número entre el 2 y el 6
Y que tenga lo que sea por delante.
Tabla de wildcards
Wildcard	Función
*	Busca todo
?	Busca por cantidad de caracteres
[]	Busca por caracteres específicos


Qué son las entradas y salidas de la terminal
En la consola nosotros generamos una entrada cuando escribimos y una salida casi siempre que ejecutamos un comando.

A las entradas típicamente se les suele llamar Standard Input y a las salidas Standard Output, además se les suele abreviar como stdin y stdout respectivamente.

Qué son file descriptors
Los file descriptors son números que identifican un recurso. Funciona asociando un número con una acción, archivo o programa, en el caso de la shell tenemos 3 file descriptors:

image.png
El 2 es Standard Error.

Cómo usar el operador de redirección (>)
A veces queremos guardar la información de una salida porque nos puede interesar almacenar lo que esa salida contiene. Veamos el siguiente ejemplo, si utilizas el comando:

`ls -l`

image.png
Lo que sucede aquí es que le diste un Standard Input (el comando) y obtuviste un Standard Output (la lista de archivos).

Si quieres que el Standard Output no vaya a la consola sino hacia un archivo, entonces puedes usar el operador > seguido del nombre del archivo en el que quieres guardar la salida.

`ls -l > output.txt`

image.png
Cómo concatenar (>>)
Suponiendo que ya tienes el archivo output.txt y ahora también quieres guardar la información de la carpeta de documentos, entonces no puedes volver a ejecutar:

`ls -l > output.txt`

Esto lo que hará es reescribir el contenido del documento, lo que necesitas es concatenar el contenido del documento con el de la salida, para eso ejecutas:

`ls -l >> output.txt`

image.png
Como puedes ver, la salida del comando ls -l se concatenó con la salida del comando ls -l ./SecretosDeEstado. Te puedes dar cuenta porque la palabra total se repite dos veces.

Por cierto, esa palabra total es el tamaño total de la carpeta en kilobytes y dice que la carpeta SecretosDeEstado pesa 0, porque los archivos y carpetas vacías no ocupan espacio.

Redirección de errores (2>|2>&1)
El operador de redirección por defecto solo redirecciona el file descriptor 1 (es decir, el Standard Output). Pero, ¿qué tal si queremos redirigir un error? Pues tenemos que especificar que queremos el Standar Error, que tiene el file descriptor 2.

Vamos a generar un error ejecutando un comando que saldrá mal para redirigirlo a un archivo llamado “error.txt”.

image.png
En este caso la opción “ñ” no existe, por lo que produce un error.

También podemos especificar que no importa lo que pase si me da un Standar Ouput o un Standar Error, igual tiene que guardar la salida en un archivo. Esto lo hacemos así:

`ls -l > output.txt 2>&1`

La orden 2>&1 significa que debe redirigir el file descriptor 2 y el file descriptor 1.

image.png
En la primera ejecución del comando, se ejecuta correctamente y guarda el Standar Output, pero en la segunda ejecución, el comando falla y guarda el Standar Error.

Tabla de operadores
Operador	Función
>	Redirecciona la salida. Por defecto redirecciona el Standar Output
>>	Concatena la salida con lo que ya tenga el archivo a donde se está redirigiendo la salida
2>	Redirecciona el file descriptor 2 (En este caso Standar Error)
2>&1	Redirecciona el file descriptor 2 y 1.


¿Cuáles son los comandos de búsqueda en la terminal?

Para encontrar archivos de forma efectiva, usa el comando find, el cual buscará en la ruta que le indiques el tipo de archivos que necesitas. Su sintaxis es:

find [rutaDesdeDondeEmpezarBuscar] [opciones]

Segmentar por el nombre (-name)
Veamos un ejemplo, voy a buscar en mi carpeta home todos los archivos que tenga una extensión “.png”.

`find ./ -name *.png`

ejemplo-comando-name.png
El punto indica que debe empezar desde la carpeta en la que está y la opción -name es para especificar el nombre que debe buscar.

Segmentar por el tipo (-type)
También puedes segmentar por el tipo, si es un archivo o si es un directorio utilizando la opción -type, el cual acepta f para archivos, d para directorios y l para enlaces simbólicos.

Si quieres usar más de una opción lo separas por comas.

`find ./ -type f -name "f*"`

usar-comando-type-terminal.png
Esto me muestra todos los archivos que comiencen con la letra “f”.

Veamos un ejemplo buscando archivos y directorios.

`find ./ -type f,d -name "D*"`

buscar-archivos-direcorios-con-comando-type-terminal.png
Segmentar por tamaño (-size)
Con la opción -size podemos segmentar por tamaño ingresando el peso que queremos buscar. Esta opción tiene un uso un tanto especial. Primero que todo hay que colocar la unidad de peso c para byte, k para Kilobyte, M para Megabyte y G para Gygabyte.

Entonces, si escribes en la terminal:

`find ./ -size 4k`

Buscará los archivos que pesen exactamente 4kb. Pero claro, atinar el peso exacto de un archivo no es para nada sencillo, así que podemos especificar que sea ese peso en adelante con el símbolo + o de ese peso para abajo con el símbolo -.

`find ./ -size +4k`

Busca los archivos que pesen 4kb o más.

`find ./ -size -4k`

Busca los archivos que pesen 4kb o menos.

Buscar vacíos (-empty)
Para buscar los archivos vacíos usamos la opción empty que es fácil de usar, no tienes que especificarle nada, solo escribirla.

Por ejemplo, si quisiera buscar todas las carpetas vacías, habría que escribir:

`find ./ -type d -empty`

como-buscar-carpetas-vacias-en-la-terminal.png
Limitar la búsqueda (-maxdepth -mindepth)
Puede que no queramos buscar en absolutamente todas las carpetas del sistema, sino que queremos únicamente un pedacito. Para eso limitamos la profundidad de carpetas a la que el comando debe buscar, esto se hace con la opción -maxdepth seguido de la profundidad.

`find ./ -type d -maxdepth 2`

Continuando, a veces ya conocemos más o menos la estructura de nuestras carpetas, así que nos queremos saltar niveles, por lo que le asignamos una profundidad mínima al comando.

`find ./ -type d -mindepth 2`
Una última cosa, es recomendable pasar el output al comando less, así:

`find ./ | less`
De esta forma podrás usar esa interfaz de less para buscar tus archivos.

Tabla de comandos de búsqueda
Opción	Función
-size	Busca por el peso
-mindepth	Asigna una profundidad mínima
-maxdepth	Asigna una profundidad máxima
-type	Busca por el tipo de archivo
-name	Busca por el nombre del archivo

Configuración de tus dispositivos (ifconfig)
Ve a tu consola, escribe el comando ifconfig y miremos el resultado.

configurar-dispositivos-con-ifconfig.png
Cuando ingresamos el comando podemos ver el nombre del dispositivo de red, en este caso es “eth0”, y su configuración, tenemos su dirección IPv4 e IPv6 y su máscara de red.

También tienes la opción del comando netstat solo que te lo mostrará de forma más amigable usando una tabla.

Enviar solicitudes a una página (ping)
A veces queremos saber si una página está disponible desde nuestra dirección IP. Para esto escribimos el comando seguido de la URL a la que queremos acceder.

El comando ping envía paquetes a esa página y evalúa el tiempo de respuesta.

Por defecto, el comando se ejecutará indefinidamente, así que tienes que detenerlo con ctrl + c.

ping www.google.com
De esta salida obtuvimos la dirección IP de esa URL, también cuanto tiempo tardó en responder la página medida en milisegundos y en la parte de abajo tenemos el total de paquetes que se enviaron, los paquetes que se recibieron, el porcentaje de paquetes perdidos y el tiempo de respuesta promedio de las consultas.

Vamos a ver unas pocas opciones más de este comando.

Limitar los paquetes enviados (-c)
Para limitar la cantidad de paquetes que enviamos, usamos la opción -c seguida del número de paquetes por enviar.

`ping -c 4 www.google.com`

uso-de-ping-para-limitar-paquetes-enviados.png
Especificar el tamaño de los paquetes (-s)
Para probar la conectividad con paquetes de diferentes tamaños se utiliza la opción -s seguido del tamaño del paquete que desees usar. El tamaño debe ser en bytes.

Para hacer pruebas con paquetes de 20 bytes escribimos:

`ping -s 20 www.google.com`

uso-de-ping-especificar-tamaño-de-paquetes.png
Obtener el archivo de una página (curl | wget)
Podemos obtener archivos que nos proporcione un sitio web o dirección IP con el comando curl. Este te mostrará la información que haya encontrado en la consola.

`curl www.google.com`
Al ejecutar este comando te dará el documento “.html” de Google, el cual lo verás como un montón de letras locas si estás empezando.

El comando wget hace algo similar, solo que en vez de mostrar lo que h obtenido por consola lo guarda en el archivo que le especifiques.

`wget www.google.com`
uso-de-comando-wget.png
La última línea de la salida del comando wget dice que la información fue guardada en el archivo “index.html”, el cual podemos ver al listar los archivos.

También podemos específicar varias direcciones para descargar varias páginas al mismo tiempo.

`wget www.google.com www.google.com`
ejemplo-uso-wget.png
Aquí vemos como se guardó la página de Google en “index.html.1” y la de google en “index.html.2”.

Ruta de acceso a la página (traceroute)
Cuando nos conectamos a una página en internet no nos conectamos directamente a los servidores en los que está almacenada esa página, sino que primero pasamos por otros servidores que son como intermediarios entre tu computadora y el servidor.

Puedes profundizar aún más sobre el tema con el Curso de Redes Informáticas de Internet de Platzi.

Tabla de comandos de utilidades de red
Comando	Función
ifconfig	Muestra la configuración de los dispositivos de red
ping	Envía paquetes a una dirección para comprobar su conectividad
curl	Muestra por consola el archivo devuelto por la dirección
wget	Guarda el archivo devuelto por la dirección

Comprimiendo archivos con formato .tar
El formato .tar es un tipo de compresión bastante usado en UNIX. Originalmente era utilizado para almacenar información en cintas magnéticas, así que está hecho especialmente para comprimir los archivos de forma lineal.

Para comprimir con este formato en la terminal usamos el comando tar que tiene ciertas opciones para aprender.

Sintaxis:

tar [opciones] [nombreDelArchivoComprimido] [archivoAComprimir]
Comprimir (-c)
Para comprimir un archivo utilizamos la opción -c. En todos los casos hay que usar la opción -f para indicar que estamos comprimiendo o descomprimiendo archivos.

tar -cf compressed.tar Documents/toCompress/
comprimir-archivo-con-tar.png
Ver lo que está haciendo el comando (-v)
Si queremos ver lo que el comando está comprimiendo a medida que se va ejecutando, usamos la opción -v. Por cierto la opción -v es de “Verbose” y muchos comandos la usan, también te la puedes encontrar como --verbose.

tar -cvf compressed.tar Documents/toCompress/
comprimir-con-tar-verbose.png
Comprimir con formato “.tar.gz” (-z)
El formato “.tar.gz” o también “.tgz” es una versión extendida del formato tradicional de compresión “.zip” que puede manejar y comprimir archivos más grandes.

Para manejar la compresión de archivos “.tar.gz” o “.tgz” se usa la opción -z además de tener que especificar en el nombre de archivo la extensión que quieres usar.

tar -czvf compressed.tar.gz Documents/toCompress/
ejemplo-para-comprimir-con-tar.gz.png
Descomprimir (-x)
Para descomprimir es mucho más sencillo, solo hay que especificar la opción -x y el archivo comprimido que se quiere descomprimir.

Si se quiere descomprimir un archivo de extensión “.tar.gz” o “.tgz” hay que especificar la opción -z también.

tar -xzvf compressed.tar.gz
ejemplo-para-descomprimir-tar.gz.png
Comprimiendo archivos .zip
Para comprimir usamos el comando zip con el nombre que quieres que tenga y lo que quieres comprimir.

Si quieres comprimir una carpeta con archivos dentro, tienes que especificar la opción -r de “recursive”.

zip -r copressed.zip Documents/toCompress/
como-comprimir-con-zip.png
Y para descomprimir es incluso más fácil, solo escribe el comando unzip seguido de lo que quieres descomprimir.

unzip compressed.zip
Tabla de comandos tar y zip
Opciones del comando tar
Recuerda siempre colocar la opción -f.

Opción	Función
c	Comprimir
x	Descomprimir
z	Especifica que lo que se va a comprimir o descomprimir tiene extensión “.tar.gz” o “.tgz”
v	Muestra lo que está comprimiendo o descomprimiendo
Comando zip
Recuerda que si lo que vas a comprimir es una carpeta tienes que usar la opción -r.

Comando	Función
zip	Comprimir
unzip	Decomprimir

Ver los procesos activos en la terminal (ps)
El comando ps muestra los procesos que están activos en una tabla muy sencilla de entender, donde el la primera columna tenemos el process ID y en la última el nombre.

ejemplo-de-procesos-activos-en-la-terminal.png
Ver procesos más detallados (top)
Si quieres ver una lista más detallada de los procesos con su consumo en CPU y en RAM, además del usuario que lo activó, usamos el comando top.

uso-del-comando-top-en-terminal.png
Aquí podemos filtrar por user. Si presionas la tecla “u” podrás escribir el nombre de usuario por el cual quieres buscar y si presionas la tecla “h” te mostrará un cuadro de ayuda para más opciones. Para salir presiona “q”.

Matar un proceso (kill)
Para matar un proceso usamos el comando kill seguido del PID del proceso que queremos matar.

Si estás usando Windows y tienes varias aplicaciones abiertas podrás usar la terminal para cerrarlas, pero para los que estamos usando WSL solo podemos acceder a los procesos que se ejecuten en la terminal.

Pero la teoría es la misma, buscamos el PID del proceso que queremos matar y lo matamos.

usar-comando-kill-de-la-terminal.png
En este caso si ejecuto el comando kill 595 voy a cerrar la terminal.

Tabla de comandos para manejo de procesos en la terminal
Comando	Función
ps	Muestra una tabla con los procesos que se están ejecutando
top	Muestra una interfaz con los procesos que se están ejecutando más los recursos que consumen información adicional
kill	Mata el proceso que le indiques

COMANDOS LINUX PARA LA GESTION DE ARCHIVOS Y DIRECTORIOS

cp

Propósito

El comando cp es un abreviatura de copy (copiar); permite copiar archivos y directorios. Para copiar un archivo se usa el siguiente mandato:

Sintaxis

cp [Opciones] archivo_fuente directorio_destino

cp [Opciones] archivo_fuente archivo_destino

Opciones

-a conserva todos los atributos de los archivos.

-b hace un backup antes de proceder a la copia.

-d copia un vínculo pero no el fichero al que se hace referencia.

-i pide confirmación antes de sobreescribir archivos.

-p conserva los sellos de propiedad, permisos y fecha.

-R copia los archivos y subdirectorios.

-s crea enlaces en vez de copiar los ficheros.

-u únicamente procede a la copia si la fecha del archivo origen es posterior a la del destino.

-v muestra mensajes relacionados con el proceso de copia de los archivos.

Descripción

El comando cp copia un archivo a otro. También puede copiar varios ficheros en un directorio determinado.

Ej.

cp manual_linux_v1 ../../../doc/linux

En este ejemplo copia el archivo manual_linux en un directorio dos niveles más arriba del actual, en el directorio doc/linux

 

mv

Propósito

Modifica el nombre de los archivos y directorios moviéndolos de una ubicación a otra.

Sintaxis

mv [Opciones] fuente destino

Opciones

-d hace una copia de seguridad de los archivos que se van a mover o renombrar.

-f elimina los archivos sin solicitar confirmación.

-v pregunta antes de sobreescribir los archivos existentes.

Descripción

El comando mv se puede utilizar para modificar el nombre o mover un archivo de un directorio a otro. Trabaja tanto con archivos como con los directorios.

Ej.

mv manual_linux_v1 manuales/linux

mv manual_linux_v1 manual_linux_v1_doc

mv manual_linux_cap1 manual_linux_cap2 manual_linux_cap2 /manual/linux

 

rm

Propósito

Elimina uno más archivos (puede eliminar un directorio completo con la opción –r).

Sintaxis

rm [Opciones] archivos

Opciones

-f elimina todos los archivos sin preguntar.

-i pregunta antes de eliminar un archivo.

-r elimina todos los archivos que se encuentran en un subdirectorio y por último borra el propio subdirectorio.

-v muestra el nombre de cada archivo antes de eliminarlo.

Descripción

El comando rm se utiliza para borrar los archivos que se le especifiquen. Para eliminar un fichero ha de tener permiso de escritura en el directorio en el que se encuentra.

Ej.

rm manual_linux_v1

rm –r documentos/

 

mkdir

Propósito

crear directorios.

Sintaxis

mkdir [Opciones] nombre_directorio

Opciones

-m modo, asigna la configuración de permisos especificada al nuevo directorio.

-p crea directorios emparentados (en caso de que no existan).

Descripción

El comando mkdir se utiliza para crear un directorio especifico.

Ej.

mkdir manuales

 

rmdir

Propósito

Elimina un directorio (siempre y cuando esté vacío).

Sintaxis

rmdir [Opciones] directorio

Opciones

-p elimina cualquier directorio emparentado que este vacío.

Descripción

El comando rmdir elimina los directorios vacíos. Si tiene algún contenido, tendrá que utilizar el comando rm –r para eliminar el directorio y sus contenidos.

Ej.

rmdir manual

 

ls

Propósito

Listar el contenido de un directorio.

Sintaxis

ls [Opciones] [nombre_directorio o archivo]

Opciones

-a muestra todos los archivos. Incluyendo a los ocultos.

-b muestra los caracteres no imprimibles de los nombres de los ficheros utilizando un código octal.

-c ordena los archivos de acuerdo con la fecha de creación.

-d muestra una lista en la que aparecen los directorios como si fuesen archivos (en vez de mostrar su contenido).

-f muestra el contenido del directorio sin ordenar.

-i muestra información de i-node.

-l muestra la lista de archivos con formato largo y con información detallada (tamaño, usuario, grupo, permisos etc.).

-p añade un carácter al nombre del archivo para indicar a que tipo pertenece.

-r coloca la lista en orden alfabético inverso.

-s muestra el tamaño (kb) de cada archivo próximo al solicitado.

-t ordena la lista de acuerdo con la fecha de cada fichero.

-R muestra una lista con el contenido del directorio actual y de todos sus subdirectorios.

Descripción

El comando ls muestra el contenido de un directorio determinado. Si se omite el nombre del directorio, mostrará el contenido del directorio en el que se encuentre. Por defecto, ls no muestra el nombre de los archivos cuyo nombre comience con un punto; para verlos tendrá que utilizar la opción –a.

Ej.

ls –a

ls –l

ls –la

 

cd

Propósito

Cambiar de directorio.

Sintaxis

cd [directorio]

Opciones

Ninguna

Descripción

Si escribe cd sin ningún nombre de directorio como argumento, se cambiará al directorio home del usuario. En cualquier otro caso se moverá al directorio indicado, si existe.

 

pwd

Propósito

Mostrar la ruta del directorio de trabajo actual.

Sintaxis.

pwd

Opciones

Ninguna

Descripción

El comando pwd imprime el directorio de trabajo (aquel en el que actualmente se está trabajando).

 

chmod

Propósito

Modifica los permisos de uno o más archivos o directorios.

Sintaxis

chmod [Opciones] [permiso_descripción] archivo

Opciones

-c muestra los archivos a los que se les han modificado los permisos.

-f hace que no aparezca en pantalla ningún mensaje de error.

-v muestra los cambios efectuados en los permisos de archivos.

-R cambia los permisos de los archivos de todos los subdirectorios.


Permisos_descripción

Quien Acción Permiso

Quien	Acción	Permiso
u: usuario

g: grupo

o: otros

a: todos

+: agregar

-: quitar

=: asignar

r: lectura

w: escritura

x: ejecutar

s: ajustar con el ID del usuario.

Ej.

chmod u+xr manual_linux

El usuario tendrá los permisos de lectura y ejecución sobre el archivo manual_linux

Descripción

Para utilizar eficazmente el comando chmod, debe especificarse la configuración de los permisos de acuerdo a la tabla de permisos_descripción.

Por ejemplo para que todos tengan permiso de lectura en un determinado archivo se tipea, chmod a+r nombre_archivo. También se podría haber tipeado chmod u=r,g=r,o=r nombre_archivo.

Otra forma de modificar los permisos es a través de un número octal de 3 cifras una cifra por cada grupo de permisos, este número surge de realizar la suma de los permisos que se les quiere asignar de acuerdo a los siguientes valores:

Permiso de lectura r = 4

Permiso de escritura w = 2

Permiso de ejecución x = 1

Y si no se le concede cualquier permiso el valor asignado es 0.

El formato para utilizar chmod especificando los permisos por medio de números es el siguiente.

chmod permiso_usuario permiso_grupo permiso_otros

Ejemplo, supongamos que creamos el archivo permiso.txt y queremos que el usuario tenga todos los permisos, el grupo los permisos de lectura y ejecución y finalmente que el resto de los usuarios tenga sólo el permiso de ejecución.

Para el usuario: lectura r = 4, escritura w = 2, ejecución x =1 ; sumados = 7

Para el grupo: lectura r= 4, escritura w = 0, ejecución x = 1; sumados = 5

Para el resto de los usuarios: lectura r = 0; escritura w = 0, ejecución x = 1; sumados = 1

Entonces el comando seria: chmod 751 permisos.txt

En la lista detallada de los archivos de un directorio (usando el comando ls), los permisos de lectura escritura y ejecución del usuario, grupo y otros se mostrarán a través de la secuencia rwxrwxrwx, cuando algún permiso no está activado aparece un guión en su reemplazo.

 

cat

Propósito

Muestra el contenido de un archivo utilizando la salida estándar (pantalla).

Sintaxis

cat [-benstvA] archivos

Opciones

-b números de líneas que no estén en blanco.

-e muestra el final de una línea (como $) y todos los caracteres no imprimibles.

-n numera todas las líneas de salida, comenzando por el 1.

-s sustituye varias líneas en blanco por una sola.

-t muestra las tabulaciones como ^l.

-v muestra los caracteres no imprimibles.

-A muestra todos los caracteres ( incluidos los no imprimibles).

Descripción

Normalmente, cat se utiliza para mostrar el contenido de un archivo o para concatenar varios dentro de un mismo fichero. Por ejemplo,

cat archivo1, archivo2, archivo3 > todo
combina los tres archivos dentro de uno solo llamado todo.

 

find

Propósito

Muestra una lista con los archivos que coinciden con un criterio especifico.

Sintaxis

find [ruta] [opciones]

Opciones

-depth procesa, en primer lugar, el directorio en el que se encuentra y luego sus subdirectorios.

-maxdepyh n restringe la búsqueda a n niveles de directorios.

-follow procesa los directorios que se incluyen dentro de los enlaces simbólicos.

-name modelo localiza los nombres de los archivos que coinciden con el modelo propuesto.

-ctime n localiza los nombres de los archivos creados n días atrás.

-user nombre_usuario nombre_usuario localiza los archivos pertenecientes al usuario especifico.

-group nombre_grupo localiza los archivos pertenecientes al grupo específico.

-path ruta localiza a los archivos cuya ruta coincide con el modelo propuesto.

-perm modo localiza los archivos con los permisos especificados.

-size +nK localiza los archivos cuyo tamaño ( en kilobytes) es mayor de especificado.

-print imprime el nombre de los archivos que encuentra.

-exec comando [opciones] {} \; ejecuta el comando especificado analizando el nombre del archivo localizado.

Descripción

El comando find es de gran utilidad cuando se quiere localizar todos los archivos que coinciden con algún criterio. Si escribe find sin ningún argumento, la salida mostrará un listado en el que aparecen los archivos de todos los subdirectorios de la carpeta en la que se encuentre.

Para ver todos los archivos cuyo nombre termine con .gz, tendrá que escribir:

find . -name "*.gz ".

Para buscar a partir del directorio /usr/doc todos los archivos con extensión bak y eliminarlos, utilizar el comando:

find /usr/doc -name “*.bak” -exec rm -f {} \;

en donde la secuencia {} se substituirá por el nombre completo de cada archivo encontrado.

 

grep

Propósito

Busca en uno o más archivos las líneas que coincidan con una expresión regular (modelo de búsqueda).

Sintaxis

grep [opciones] modelo archivos

Opciones

-N muestra N líneas que contienen el modelo de búsqueda señalado.

-c muestra el número de líneas que contienen el modelo de búsqueda.

-f archivo lee las opciones del archivo especificado.

-i ignora letras

-l muestra los nombres de los archivos que contienen un modelo.

-q devuelve el número de línea siguiente a aquellas en las que se encuentra el modelo de búsqueda.

-v muestra las líneas que no contienen el modelo de búsqueda.

Descripción

El comando localiza el modelo de búsqueda en los archivos especificados. El modelo es una expresión regular en los archivos especificados que tienen sus propias reglas. Generalmente se utiliza para buscar una secuencia de caracteres en uno o más archivos de texto.

Ejemplo

grep Juan ListadoDeAlumnos.txt

 

 

OTROS COMANDOS DE LINUX

man: Muestra por pantalla secciones del manual del usuario.

Formato: man Nombre del comando.

Ej: man ls.

 

mesg: Habilita o deshabilita la comunicación entre usuarios por medio de write.

Formato : mesg [n/y].

 

lpr: Imprime el contenido de un archivo.

Formato: lpr [Opción] Archivo

Se consideran las principales opciones:

-P cola Indica la cola de impresión a utilizar.

-n<número>: Indica la cantidad de copias a imprimir, por defecto siempre es 1.

-R: Remueve el archivo después de realizada la impresión.

 

tree: Lista todos los directorios a partir del directorio actual o del directorio indicado.

Formato: tree [Directorio].

 

tty: Muestra el número de la terminal donde está trabajando el usuario.

Formato: tty

 

who: Visualiza los usuarios que están activos en el sistema, sin ningún tipo de argumento éste comando muestra los nombres de usuario, número de terminal y horario de conexión por cada usuario activo del sistema. Utilizando los argumentos who am i el comando muestra con que nombre de usuario está usted conectado.

Formato: who [Opción]


write: Envía mensajes a otros usuarios hasta que se digite "Control D". La recepción de estos mensajes puede ser deshabilitada por el usuario utilizando el comando MESG.

Formato: write Usuario Terminal


Comandos de Linux fundamentales para desarrolladores
1. Comando man
Uno de los primeros comandos que debes conocer en Linux es man. Con él podemos conocer el uso de todos los comandos de Linux, mostrando una vista con información como nombre, sinopsis, descripción, opciones, estado de salida, valores de devolución, errores, archivos, versiones, ejemplos, etc. Por ejemplo, si quieres conocer el comando “cd” y sus opciones, tendrías que ejecutar el comando man cd para conocer su descripción y uso.

Sintaxis:

man [command/tool name]
2. Comando touch
Este comando se usa para crear cualquier tipo nuevo de archivo en sistemas Linux. Es muy útil para los desarrolladores permitiendo crear archivos en el servidor. También, se usa para  cambiar la hora de acceso y modificación de archivos. 

Sintaxis:

touch file_name
3. Comando cat
cat es uno de los más utilizados en Linux. El nombre del comando cat viene de “concatenate”, su funcionalidad para concatenar archivos o unir, sumar. Puede leer, concatenar archivos, combinarlos y escribir contenidos de archivos en una salida estándar. 

También se utiliza para mostrar el contenido de un archivo, copiar contenido de un archivo a otro, mostrar el número de línea o mostrar $ al final de la línea.

Para ejecutar este comando, escribe cat seguido del nombre del archivo y su extensión. Por ejemplo: cat archivo.txt .

Sintaxis:

$cat filename
4. Comando cd
Otros de los comandos más útiles en Linux es el comando cd o de cambio de directorio. Con la ayuda de este comando, podemos navegar por todos nuestros directorios en nuestro sistema. Las opciones que nos permite serían:

Cambiar del directorio actual a un nuevo directorio
Cambiar directorio usando una ruta absoluta
Cambiar directorio usando la ruta relativa
Cambiar al directorio de inicio
Cambiar al directorio anterior
Cambiar al directorio principal
Cambiar al directorio raíz
Cambiar al directorio de inicio de otro usuario
Cambiar a directorio con espacios
Cambiar hasta múltiples subdirectorios
La sintaxis del comando cd es la siguiente:

cd [OPTIONS] directory
5. Comando ls
Este comando enumera el contenido del directorio que desee, archivos y otros directorios anidados. Cuando se usa sin opciones ni argumentos, ls muestra una lista en orden alfabético de los nombres de todos los archivos en el directorio de trabajo actual. 

Si quieres ver el contenido de otros directorios, escribe ls y luego indica la ruta del directorio:

Puedes usar estas variaciones con el comando ls:

ls -R Enumera todos los archivos en los subdirectorios
ls -a Lista los archivos ocultos
ls -al Muestra los archivos y directorios con información detallada como los permisos, el tamaño, el propietario, etc.
Sintaxis:

[code] ls [ option …] [ file o directory ] [/code]
6. Comando vim
vim es un editor de texto de terminal gratuito y de código abierto. Puedes usarlo como tu editor de código.

Sintaxis:

vim file
vim [options] [filelist]
7. Comando sed
El editor de flujo es un poderoso comando de búsqueda y reemplazo masivo , pero también es un editor de texto legítimo.

Sintaxis:

sed OPTIONS... [SCRIPT] [INPUTFILE...]
8. Comando tar
Este  comando se utiliza para crear y extraer archivos de almacenamiento. Los indicadores «-cf» y «-xf» se usan para crear y extraer archivos.

Sintaxis: 

tar [options] [archive-file] [file or directory to be archived]
9. Comando pwd
El comando pwd se usa para localizar la ruta del directorio de trabajo en el que te encuentras. Por ejemplo, si mi nombre de usuario es «miriam» y estoy en mi directorio Documentos, la ruta absoluta sería: /home/miriam/Documents.

Sintaxis:

pwd [OPTION]...
10. Comando mkdir
Este comando permite a los usuarios crear directorios (carpetas). Posibilita la creación de varios directorios a la vez, así como establecer los permisos para los directorios.

Sintaxis:

mkdir <dirname>  
11. Comando find
Puedes usar el comando find para buscar archivos y directorios según sus permisos, tipo, fecha, propiedad, tamaño, etc.. También se puede combinar con otras herramientas como grep o sed.

Sintaxis:

find [options] [path...] [expression]
12. Comando rm
rm elimina cada archivo especificado en la línea de comando y directorios. Ten mucho cuidado al usarlo porque no se puede deshacer y es muy difícil recuperar archivos eliminados de esta manera.

Para eliminar un archivo normal, debe escribir la siguiente sintaxis:

rm file_to_copy.txt
13. Comando diff
El comando diff nos ayuda a comparar dos archivos línea por línea y mostrar la diferencia entre ellos. Esta utilidad de línea de comandos lista los cambios que debe aplicar para que los archivos sean iguales.

Sintaxis:

diff [OPTION]... FILES
14. Comando chown
chown permite cambiar el propietario del archivo o directorio. También se puede usar para cambiar la propiedad del grupo para el archivo o directorio.

Sintaxis:

chown user filename(s)
15. Comando uniq
uniq es nos ayuda a detectar las líneas duplicadas adyacentes y también elimina las líneas duplicadas. uniq filtra las líneas coincidentes continuas del archivo de entrada (que se requiere como argumento) y escribe los datos filtrados en el archivo de salida.

Sintaxis:

uniq [OPTION]... [INPUT [OUTPUT]]
16. Comando wget
Este comando permite descargar archivos de Internet. Admite protocolos de red populares como FTP, HTTP y HTTPS. También puede manejar proxies HTTP.

Sintaxis:

wget url
wget [options] url
17. Comando top
El comando top muestra una vista de los procesos en ejecución en Linux en tiempo real y muestra las tareas administradas por el kernel . También, muestra un resumen de información del sistema para ver la utilización de recursos, memoria y uso de CPU.

Sintaxis:

top [opción] [opción]
18. Comando grep
El comando grep «global regular expression print» filtra el contenido de un archivo para facilitar nuestra búsqueda.

Sintaxis:

grep <searchWord>  
grep "linux" long.txt
19. Comando df
Se usa para mostrar la cantidad en porcentaje y KB de espacio libre en disco disponible en Linux.

Sintaxis:

df [opciones] [sistema-de-archivo...]
20. Comando kill
Se usa para cerrar una proceso que no finaliza ayudando a terminarlo de manera manual. Funciona enviando una señal que termina finalizando o eliminando un proceso o grupo de procesos en particular.

Sintaxis:

kill [options] pid
21. Comando ping
ping es uno de los comandos más utilizados que nos ayuda a solucionar problemas, probar y diagnosticar problemas de conectividad de red. Este comando tiene más opciones que incluyen comprobar si se puede acceder a un host, verificar si un servidor está en funcionamiento, su conexión a Internet y posibles demoras en la red.

Sintaxis:

ping [OPTIONS] [IP or Domain]
22. Comando ldd
El comando ldd permite a los usuarios conocer las dependencias de objetos compartidos de un archivo ejecutable o de una biblioteca compartida de un ejecutable.

Sintaxis:

ldd [OPTION]... FILE…
23. Comando lsof
El comando lsof, acrónimo de “list of open files.”, enumera información sobre los archivos que están abiertos por los procesos que se ejecutan en el sistema.

Sintaxis:

 lsof [options]
24. Comando objdump
Permite desensamblar archivos de objetos o archivos ejecutables. También te ayuda a obtener información adicional que puede contener un archivo binario en un formato legible.

Sintaxis:

objdump <opción(es)> <archivo(s)>
25. Comando shutdown
Este comando detiene el sistema de forma segura. En el momento en el que shutdown se ejecuta, se notifica a todos los usuarios y procesos que han iniciado sesión que el sistema se está desactivando y no se permiten más inicios de sesión. Te da la opción de apagar el sistema de manera inmediata o en un momento especifico.

Sintaxis:

shutdown [OPTIONS] [TIME] [MESSAGE]