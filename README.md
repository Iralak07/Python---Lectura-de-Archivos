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

¿Por Qué Vemos Líneas Vacías Extras?
La razón por la cual ves líneas vacías adicionales es debido a cómo funciona el método print en Python y cómo las líneas son leídas desde el archivo.

Líneas con saltos de línea: Cuando lees una línea de un archivo usando un bucle for, cada línea que se lee incluye el carácter de salto de línea (\n) al final. Por ejemplo, una línea que se lee del archivo podría ser From: stephen.marquard@uct.ac.za\n.

El método print agrega otro salto de línea: El método print en Python, por defecto, agrega un carácter de salto de línea adicional después de la cadena que imprime. Esto significa que si ya hay un salto de línea al final de la cadena, print agregará otro, resultando en una línea vacía adicional en la salida.

El método rstrip() es una forma conveniente y efectiva de eliminar los caracteres de espacio en blanco (incluyendo los saltos de línea) del lado derecho de una cadena. Esto se ajusta perfectamente a tu necesidad de evitar las líneas vacías adicionales en la salida. Aquí te muestro cómo puedes usar rstrip() en tu código:

      man_a = open('mbox-short.txt')  # Abre el archivo 'mbox-short.txt' y asigna el objeto archivo a la variable man_a.
      for linea in man_a:  # Itera sobre cada línea en el archivo.
          linea = linea.rstrip()  # Elimina los espacios en blanco del lado derecho de la línea, incluyendo el salto de línea.
          if linea.startswith('From:'):  # Si la línea empieza con 'From:', entonces...
              print(linea)  # Imprime la línea.
    

¿Por Qué Funciona rstrip()?
Salto de línea incluido: Cuando se lee una línea de un archivo, cada línea termina con un salto de línea (\n). El método rstrip() elimina este carácter (y otros espacios en blanco) del lado derecho de la cadena.
Impresión sin líneas vacías adicionales: Al eliminar el salto de línea antes de imprimir, print agrega su propio salto de línea, resultando en una salida sin líneas vacías adicionales.
Este método es más sencillo y directo comparado con el uso de troceado de líneas, y es muy común en la práctica para manejar este tipo de situaciones.



