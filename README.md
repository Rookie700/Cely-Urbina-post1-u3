# Cely-Urbina-post1-u3

Descripción del Laboratorio
Este laboratorio consiste en la configuración del entorno DOSBox para el acceso y uso del depurador DEBUG
. El objetivo principal es que el estudiante interactúe con la arquitectura del procesador mediante la inspección del estado inicial de los registros, la manipulación de bloques de memoria (relleno y volcado) y el desensamblado de código directamente en memoria
.
Configuración del Entorno
Para el desarrollo de la actividad, se realizaron los siguientes pasos iniciales:
Montaje del directorio: Se vinculó la carpeta de trabajo local como una unidad virtual C: mediante el comando MOUNT C C:\RutaTrabajo
.
Creación de estructura: Se creó el directorio específico LAB3POST1 para organizar los archivos del laboratorio
.
Inicio de DEBUG: Se invocó el depurador desde el prompt de DOS para comenzar la inspección del sistema
.

--------------------------------------------------------------------------------
Checkpoint 1: Inspección y Modificación de Registros
Comandos utilizados:
R: Muestra el estado completo de los registros
.
R AX: Permite la modificación selectiva del registro AX
.
Observaciones:
Se observa que, al iniciar el DEBUG, los registros de propósito general (AX, BX, CX, DX) se encuentran en cero
. El puntero de instrucción (IP) inicia en la dirección 0100h, que representa la primera dirección ejecutable tras el PSP (Program Segment Prefix)
. Al modificar el registro AX con el valor 1234h, se confirma que el cambio es selectivo, manteniendo la integridad del resto del estado del procesador
.

--------------------------------------------------------------------------------
Checkpoint 2: Volcado de Memoria y Análisis del PSP
Comandos utilizados:
F 200 L40 AB CD EF: Rellena 64 bytes desde la dirección 0200h con un patrón cíclico
.
D 200 L40: Realiza un volcado hexadecimal de la región de memoria rellenada
.
D 0 L20: Explora los primeros 32 bytes del PSP
.
Análisis de las columnas del comando D:
La salida del comando D (Dump) se organiza en tres secciones principales:
Columna de Direcciones: Muestra la ubicación de memoria en formato Segmento:Offset
.
Sección Hexadecimal: Presenta el contenido de la memoria en bytes representados en hexadecimal, divididos en dos grupos de 8 bytes para facilitar la lectura
.
Columna ASCII: Muestra la representación visual de los bytes; si el valor no es un carácter imprimible, se representa con un punto (.), como sucede con los valores AB, CD y EF
.
Observaciones:
Se verificó que el comando F ejecuta la operación de relleno de manera silenciosa sin mensajes de confirmación
. En la inspección del PSP, se identificó la instrucción INT 20 (CD 20) en la dirección 0000h, la cual es colocada por el DOS como mecanismo de terminación controlada para programas
.

--------------------------------------------------------------------------------
Checkpoint 3: Ensamblado y Desensamblado de Código
Comandos utilizados:
U 100 L10: Desensambla la región de código inicial
.
A 100: Permite introducir instrucciones en lenguaje ensamblador directamente
.
U 100 109: Traduce los bytes de la memoria a mnemónicos legibles para verificar el programa
.
Observaciones:
Se demuestra el principio fundamental del modo real: no existe distinción intrínseca entre código y datos, ya que el procesador interpreta como instrucción cualquier byte señalado por el registro CS:IP
. Al ensamblar un programa simple (MOV, ADD, INT), se observa una correspondencia directa entre los mnemónicos y los códigos de operación (opcodes); por ejemplo, la instrucción MOV AX, 0005 se codifica físicamente como los bytes B8 05 00
.
