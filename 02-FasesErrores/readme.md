<h3> Trabajo Práctico #2 - Fases de la Traducción y Errores</h3>

<h4> Objetivos </h4>

Este trabajo tiene como objetivo identificar las fases del proceso de traducción o
Build y los posibles errores asociados a cada fase.

Para lograr esa identificación se ejecutan las fases de traducción una a una, se
detectan y corrigen errores, y se registran las conclusiones en readme.md.

No es un trabajo de desarrollo; es más, el programa que usamos como ejemplo es
simple, similar a hello.c pero con errores que se deben corregir. La complejidad
está en la identificación y comprensión de las etapas y sus productos.


<h4> Temas </h4>

• Fases de traducción.

• Preprocesamiento.

• Compilación.

• Ensamblado.

• Vinculación (Link).

• Errores en cada fase.

• Compilación separada.

<h4> Secuencia de Pasos </h4>

Se parte de un archivo fuente que es corregido y refinado en sucesivos pasos.
Es importante no saltearse pasos para mantener la correlación, ya que el estado
dejado por el paso anterior es necesario para el siguiente.

<h4> Tareas </h4>

1. La primera tarea es investigar las funcionalidades y opciones que su
compilador presenta para limitar el inicio y fin de las fases de traducción.
2. La siguiente tarea es poner en uso lo que se encontró. Para eso se debe
transcribir al readme.md cada comando ejecutado y su resultado o error
correspondiente a la siguiente secuencia de pasos. También en readme.md se
vuelcan las conclusiones y se resuelven los puntos solicitados. Para claridad,
mantener en readme.md la misma numeración de la secuencia de pasos.

<h4> Restricciones </h4>

• El programa ejemplo debe enviar por stdout la frase La respuesta es 42, el
valor 42 debe surgir de una variable.


<h3> hello2.c -> hello2.i </h3>

Comando Ejecutado: gcc hello2.c -E > hello2.i

Resultado: Se observa en el archivo preprocesado que reemplaza el comentario /*medio*/ por un espacio en blanco.
Además, en los primeros renglones se visualiza código de las funciones de la biblioteca estándar.

<h3> hello3.c -> hello3.i </h3>

Comando Ejecutado: gcc hello3.c -E > hello3.i

Resultado: Las diferencias se dan en la primera linea
#1 "hello3.c"   #1 "<built-in>"   #1 "<command-line>"   #1 "hello3.c"
  
<h3> hello3.c -> hello3.s </h3>

Comando Ejecutado: gcc -S hello3.c

Error: Tira un warning porque la función no ha sido declarada y sugiere otro nombre. Además, espera que en la sentencia main haya un } para cerrarla.

<h3> hello4.c -> hello4.s </h3>

Comando Ejecutado: gcc -S hello4.c

Resultado: Se puede observar el programa en código ensamblador. Por lo que ve, muestra las llamadas a las funciones main y prontf en código ensamblador. 

<h3> hello4.s -> hello4.o </h3>

Comando Ejecutado: as -o hello4.o hello4.s

Resultado: Transforma el programa de código ensamblador a código objeto.

<h3> hello4.o </h3>

Comando Ejecutado: ld -o hello4 hello4.o

Errores: undefined reference to `__main`
         undefined reference to `prontf`
         
Al intentar enlazar y generar el ejecutable, no reconoce las funciones main ni prontf.
         
<h3> hello5.c -> hello5 </h3>

Comando Ejecutado: gcc -o hello5 hello5.c

Resultado: La respuesta es 4200880

Para corregirlo modificamos el prontf por printf, por lo que ya puede encontrar la definición en la biblioteca estándar.
Dado que la función printf esperaba imprimir una variable, al no encontrarlo especificado arroja un valor cualquiera. 

<h3> hello6.c -> hello6 </h3>

Comando Ejecutado: gcc -o hello6 hello6.c

Resultado: La respuesta es 42
Al colocar la variable i, no arroja errores ya que la función esperaba una variable.

<h3> hello7.c -> hello7 </h3>

Comando Ejecutado: gcc -o hello7 hello7.c

Resultado: La respuesta es 42
Al quitar el primer prototipo de printf, no le quita la funcionalidad al programa dado que ahí no se encuentra la definición. Sin embargo, si arroja un Warning aclarando la declaración implícita de la función printf.
