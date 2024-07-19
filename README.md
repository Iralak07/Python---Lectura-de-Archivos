# Python---Lectura-de-Archivos
Cuando buscas a través de los datos de un archivo, un patrón muy común es leer el archivo, ignorar la mayoría de las líneas y solamente procesar líneas que cumplan con una condición particular.


Si queremos leer un archivo y solamente imprimir las líneas que comienzan con el prefijo “From:”, podríamos usar el método de cadenas startswith para seleccionar solo aquellas líneas con el prefijo deseado.

    man_a = open('mbox-short.txt')
      contador = 0
      for linea in man_a:
        if linea.startswith('From:'):
        print(linea)

Cuando este programa se ejecuta, obtenemos la siguiente salida:

      From: stephen.marquard@uct.ac.za
      
      From: louis@media.berkeley.edu
      
      From: zqian@umich.edu
      
      From: rjlowe@iupui.edu

      ...

## ¿Por Qué Vemos Líneas Vacías Extras?
La razón por la cual ves líneas vacías adicionales es debido a cómo funciona el método print en Python y cómo las líneas son leídas desde el archivo.

Líneas con saltos de línea: Cuando lees una línea de un archivo usando un bucle for, cada línea que se lee incluye el carácter de salto de línea (\n) al final. Por ejemplo, una línea que se lee del archivo podría ser From: stephen.marquard@uct.ac.za\n.

El método print agrega otro salto de línea: El método print en Python, por defecto, agrega un carácter de salto de línea adicional después de la cadena que imprime. Esto significa que si ya hay un salto de línea al final de la cadena, print agregará otro, resultando en una línea vacía adicional en la salida.

El método rstrip() es una forma conveniente y efectiva de eliminar los caracteres de espacio en blanco (incluyendo los saltos de línea) del lado derecho de una cadena. Esto se ajusta perfectamente a tu necesidad de evitar las líneas vacías adicionales en la salida. Aquí te muestro cómo puedes usar rstrip() en tu código:

      man_a = open('mbox-short.txt')  # Abre el archivo 'mbox-short.txt' y asigna el objeto archivo a la variable man_a.
      for linea in man_a:  # Itera sobre cada línea en el archivo.
          linea = linea.rstrip()  # Elimina los espacios en blanco del lado derecho de la línea, incluyendo el salto de línea.
          if linea.startswith('From:'):  # Si la línea empieza con 'From:', entonces...
              print(linea)  # Imprime la línea.
    

## ¿Por Qué Funciona rstrip()?
Salto de línea incluido: Cuando se lee una línea de un archivo, cada línea termina con un salto de línea (\n). El método rstrip() elimina este carácter (y otros espacios en blanco) del lado derecho de la cadena.
Impresión sin líneas vacías adicionales: Al eliminar el salto de línea antes de imprimir, print agrega su propio salto de línea, resultando en una salida sin líneas vacías adicionales.
Este método es más sencillo y directo comparado con el uso de troceado de líneas, y es muy común en la práctica para manejar este tipo de situaciones.


## Simulación de la Búsqueda de un Editor de Texto con el Método find en Python
Podemos usar el método de cadenas find para simular la función de búsqueda de un editor de texto, que encuentra las líneas donde aparece la cadena de búsqueda en alguna parte. Dado que find busca cualquier ocurrencia de una cadena dentro de otra y devuelve la posición de esa cadena o -1 si la cadena no fue encontrada, podemos escribir el siguiente bucle para mostrar las líneas que contienen la cadena “@uct.ac.za” (es decir, los que vienen de la Universidad de Cape Town en Sudáfrica):

        man_a = open('mbox-short.txt')  # Abre el archivo 'mbox-short.txt' y asigna el objeto archivo a la variable man_a.
        for linea in man_a:  # Itera sobre cada línea en el archivo.
            linea = linea.rstrip()  # Elimina los espacios en blanco del lado derecho de la línea, incluyendo el salto de línea.
            if linea.find('@uct.ac.za') == -1:  # Si la cadena '@uct.ac.za' no se encuentra en la línea, continúa con la siguiente iteración.
                continue
            print(linea)  # Imprime la línea si contiene la cadena '@uct.ac.za'.


## Permitiendo al usuario elegir el nombre de archivo

Cuando desarrollamos programas que procesan archivos, es muy conveniente permitir que el usuario especifique el archivo a procesar cada vez que se ejecuta el programa. Esto evita la necesidad de modificar el código cada vez que se desea trabajar con un archivo diferente.

    narchivo = input('Ingresa un nombre de archivo: ')  # Solicita al usuario que ingrese el nombre del archivo.
    man_a = open(narchivo)  # Abre el archivo especificado por el usuario.
    contador = 0  # Inicializa un contador en 0.
    for linea in man_a:  # Itera sobre cada línea en el archivo.
        if linea.startswith('Subject:'):  # Si la línea empieza con 'Subject:', incrementa el contador.
            contador = contador + 1
    print('Hay', contador, 'líneas de asunto (subject) en', narchivo)  # Imprime el número de líneas que empiezan con 'Subject:'.


## Utilizando try, except, y open

¿Qué tal si nuestro usuario escribe algo que no es un nombre de archivo?
python search6.py

        Ingresa un nombre de archivo: missing.txt
        Traceback (most recent call last):
        File "search6.py", line 2, in <module>
        man_a = open(narchivo)
        FileNotFoundError: [Errno 2] No such file or directory: 'missing.txt'


No subestimes a los usuarios; eventualmente, harán cualquier cosa para estropear tus programas, ya sea intencionalmente o no. Por esta razón, los equipos de desarrollo de software incluyen un grupo llamado Control de Calidad (QA), cuya tarea es probar el software de maneras extremas para intentar hacerlo fallar.

El equipo de QA es crucial para identificar fallos en los programas antes de que estos lleguen a los usuarios finales, quienes podrían comprar el software o pagar los salarios de los desarrolladores. Por lo tanto, el equipo de QA es el mejor aliado de un programador.

Para abordar los defectos en un programa, como la posibilidad de que la función open falle al intentar abrir un archivo, podemos manejar los errores de forma elegante utilizando la estructura try/except. Esto permite al programa recuperarse de errores potenciales y continuar funcionando adecuadamente.

        narchivo = input('Ingresa un nombre de archivo: ')  # Solicita al usuario que ingrese el nombre del archivo.
        try:
            man_a = open(narchivo)  # Intenta abrir el archivo especificado por el usuario.
        except:
            print('No se puede abrir el archivo:', narchivo)  # Imprime un mensaje de error si no se puede abrir el archivo.
            exit()  # Sale del programa si el archivo no se puede abrir.
        
        contador = 0  # Inicializa un contador en 0.
        for linea in man_a:  # Itera sobre cada línea en el archivo.
            if linea.startswith('Subject:'):  # Si la línea empieza con 'Subject:', incrementa el contador.
                contador = contador + 1
        print('Hay', contador, 'líneas de asunto (subject) en', narchivo)  # Imprime el número de líneas que empiezan con 'Subject:'.

## Depuracion
### Problemas con Espacios en Blanco en Archivos

Cuando trabajas con archivos, es común que los datos contengan espacios en blanco, como espacios, tabuladores (\t) y saltos de línea (\n). Estos caracteres pueden no ser visibles al inspeccionar rápidamente el contenido de los archivos, lo que puede hacer que los errores relacionados con ellos sean difíciles de detectar y depurar.

Ejemplo de una Cadena con Espacios en Blanco
Considera la siguiente cadena en Python:

        s = '1 2\t 3\n 4'
        print(s)

Esto es porque \t es un tabulador y \n es un salto de línea. Aunque el resultado visual no muestra claramente los espacios y los caracteres especiales, estos están presentes en la cadena y pueden causar problemas en el procesamiento de datos.

### Uso de repr para la Depuración
La función repr de Python puede ser muy útil para depurar este tipo de problemas. repr toma cualquier objeto como argumento y devuelve una representación de cadena de ese objeto que muestra los caracteres invisibles como secuencias de escape. Esto es particularmente útil para ver exactamente cómo se estructura la cadena con sus espacios en blanco y caracteres especiales


        print(repr(s))

El resultado de repr(s) sería:

        '1 2\t 3\n 4'

Aquí puedes ver claramente los caracteres invisibles: el espacio, el tabulador (\t), y el salto de línea (\n).
