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
2>&1	Redirecciona el file descriptor 2 y 1