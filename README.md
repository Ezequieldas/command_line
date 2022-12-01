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