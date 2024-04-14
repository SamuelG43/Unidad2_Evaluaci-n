# Unidad2_Evaluación

## Introducción:
En esta actividad, nos embarcaremos en el desarrollo de un programa basado en un 
microcontrolador Arduino o una Raspberry Pi Pico. Utilizaremos dos códigos, uno en el 
entorno de Arduino y otro en Unity, para establecer una comunicación efectiva entre 
ambos sistemas.

## Objetivo:
El propósito de este proyecto es crear un programa que actúe como puente de 
comunicación entre una placa Raspberry Pi Pico y dos códigos, uno ejecutado en el 
entorno de Arduino y otro en Unity. La meta principal es establecer una conexión unilateral 
que permita escribir, enviar, recibir y leer datos desde ambas partes de manera eficiente y 
coherente
- 3 Variables y la posibilidad de cambiar su valor inicial, su velocidad de cambio y 
habilitar o deshabilitar la variable
- Una interfaz grafica que permita interactuar con estos datos
- Narrativa que acompañe la experiencia
Funcionamiento del Programa


## Diagrama de estados:




## Codigo de arduino:
Declaracion de Variables: 
Para todas las variables, se declaran variables para manipular su valor inicial, su 
temperatura y una variable de tipo booleano que permita su activación y desactivación
Mediante una máquina de estados en el estado de configuración, se permite habilitar y 
deshabilitar la variable, así como cambiar su valor inicial y su velocidad utilizando la 
entrada de teclado.
Al presionar la tecla J, una vez que toda la configuración haya sido establecida, se avanza 
al siguiente estado de la máquina llamado 'OxigenoProceso', donde se llevará a cabo toda 
la lógica para disminuir las variables.
Mediante el uso de variables temporales establecidas por millis (que cumplen la función 
de una espera de 1000 milisegundos sin tener que recurrir a la función delay, ya que podría 
causar bloqueos en el programa), se disminuye el valor de 
oxígeno/refrigeración/temperatura en el valor escogido en velocidad de consumo. 
Posteriormente, se imprimen/almacenan en el buffer, precedidos por una etiqueta 
distintiva como "B", "M" o "N", que servirá para identificar la variable desde el código de 
Unity
Si las 3 variables llegan a cero, entonces la máquina de estados pasa a su estado final, 
donde todos los valores se restablecen.
CODIGO DE UNITY
Una vez que el código de Arduino esté programado, solo es necesario crear un programa 
en Unity para enviar datos al microcontrolador, recibir nuevos datos y convertirlos a 
valores numéricos. Esto se debe a que lo que se almacena en el buffer son impresiones de 
cadenas de texto, por lo que es necesario convertirlas para poder manipularlas en Unity.
En esta parte del código, declaramos variables de tipo entero que serán las encargadas de 
almacenar, en Unity, los valores traídos desde la placa de Arduino.
Se envía mediante un arreglo de bytes el valor hexadecimal 0x48, que representa la letra 
que desencadena el evento en Arduino. Este valor hexadecimal se envía a la placa 
mediante la instrucción Serial.Write. Posteriormente, se recupera lo almacenado en el 
buffer utilizando Serial.Read. Sin embargo, para un manejo más fácil de lo recibido, se 
reenvía a una variable de tipo entero. Esta variable podrá ser manipulada en Unity. 
(Obsérvese la instrucción 'Out OxygenRate', donde 'OxygenRate' representa la variable de 
tipo entero hacia la que se redirige lo recibido en el buffer). Además, de este modo, el 
buffer podrá estar vacío cuando necesite recibir otra instrucción
Función en Unity que envía, mediante hexadecimales, la letra 'J', la cual en el código de 
Arduino ejecuta el cambio de estado de la máquina a 'OxigenoProceso' o 'Jugar'.
Dentro de la función Update, se reciben los valores enviados desde Arduino en este 
segmento:
Como se mencionó anteriormente, las letras antes de cada valor servirán para identificar a 
qué variable se deben dirigir los datos del búfer. Esto se realiza mediante casos, y a través 
de un arreglo se separa el primer carácter recibido (la letra/etiqueta) del resto de 
caracteres (los valores numéricos de cada variable).
Posteriormente en Unity se revisa si el jugador introdujo una contraseña en un elemento 
de UI de tipo InputField, si es incorrecto no pasara nada, si es correcto entonces el jugador 
ganara.


## Construccion de la interfaz grafica
Para representar la velocidad en la que las variables deben cambiar
Para aumentar o disminuir distintas variables
Como objeto principal en la interfaz, aunque sin funcionalidad aporta a la narrativa y 
ambientacion de una central nuclear
Objeto Grafico para Representar la refrigeracion, el oxigeno y la temperatura
