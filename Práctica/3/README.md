# Práctica 3

## Semántica

### Ejercicio 1: ¿Qué define la semántica?
La semántica es el conjunto de reglas para dar significado a los programas sintácticamente válidos. Define el significado de los simbolos, palabras y frases de un lenguaje ya sea lenguaje natural o lenguaje informático que es sintácticamente válido.

### Ejercicio 2: 

**a. ¿Qué significa compilar un programa?** 
- Significa que se prepara el programa en el lenguaje máquina para que luego pueda ser ejecutado. El compilador es un programa que traduce nuestro programa previo a la ejecución. El compilador toma todo el programa escrito en un lenguaje de alto nivel (lenguaje fuente) antes de su ejecución. Luego de la compilación va a generar un lenguaje objeto que es generalmente el ejecutable (escrito en lenguaje de máquina .exe) o un lenguaje de nivel intermedio (o lenguaje ensamblador .obj)

**b. Describa brevemente cada uno de los pasos necesarios para compilar un programa.** 
- La compilación puede ser en 1 o 2 etapas. 

- Etapa de Análisis:
	- Análisis léxico (Scanner): 
		- Se fija que cada elemento del programa se corresponda con un operador, un identificador, etc., básicamente divide el programa en sus elementos: identificadores, delimitadores, símbolos especiales, números, palabras clave, palabras reservadas, comentarios, etc. De esta forma ve si todas las palabras son válidas o no.
		- Es el que lleva más tiempo.
		- Filtra comentarios y separadores como: espacios en blanco, tabulaciones, etc.
		- Genera errores si la entrada no coincide con ninguna categoría léxica.
		- Con esto descubrimos los tokens
		- Pone los identificadores en la tabla de símbolos.
		- Reemplaza cada símbolo por su entrada en la tabla de símbolos
		- El resultado de este paso será el descubrimiento de los items léxicos o tokens.
	- Análisis sintáctico (Parser):
		- Se realiza luego de análisis léxico.
		- Se analiza a nivel de cada sentencia.
		- Busca estructuras, sentencia, declaración, expresiones, variable, ayudándose de los tokens.
		- Se alterna el analizador sintáctico con el análisis semántico.
		- Construye el árbol sintáctico del programa.
	- Análisis semántico (semántica estática):
		- Es la fase más importante
		- Todas las estructuras sintácticas reconocidas son analizadas.
		- Se realiza una comprobación de tipos y se agrega información implícita (variables no declaradas).
		- Se agregan tablas de símbolos de los descriptores de tipos, etc.
		- Se hace comprobaciones de nombres y duplicados
		- Nexo entre etapas inicial y final del compilador
- Etapa de Síntesis del compilador:
	- Generación de código intermedio:
		- No se hace siempre ni todos los compiladores lo hacen. Consiste en traducir el programa fuente a una representación intermedia pensada para una máquina abstracta. Es independiente de la arquitectura del hardware. Facilita la optimización y la posterior generación de código objeto.
		- Debe cumplir: ser fácil de generar a partir del árbol sintáctico y ser fácil de traducir a código objeto.
		- Si el programa está dividido en varios módulos o usa bibliotecas, el linker combina todos los módulos objeto en un único programa ejecutable. (módulos del programa, funciones, librerías, subrutinas, procedimientos)
		- El resultado final es un programa ejecutable o módulo de carga.
		- Interviene el Loader (cargador) del sistema operativo, que carga el programa en memoria para su ejecución.

**c. ¿En qué paso interviene la semántica y cual es su importancia dentro de la compilación?**
- La semántica interviene en la etapa de análisis semántico y es de suma importancia ya que es el nexo entre las etapas inicial y final del compilador

### Ejercicio 3: Con respecto al punto anterior ¿es lo mismo compilar un programa que interpretarlo? Justifique su respuesta mostrando las diferencias básicas, ventajas y desventajas de cada uno.

No, no es lo mismo. El intérprete y el compilador se puede comparar de diferentes formas:
- Cómo se realiza la ejecución:
	- Intérprete: lo hace durante la ejecución. Ejecuta sentencia a sentencia, la analiza, decodifica y ejecuta. Para ser ejecutado en otra máquina se necesita tener si o si el intérprete instalado.
	- Compilador: ocurre antes de ejecutar. Compila todo y genera un código objeto de un lenguaje de un modelo más bajo. El programa fuente no será publico
- Orden de ejecución:
	- Interprete: sigue el orden lógico de ejecución (ya que va sentencia por sentencia del código)
	- Compilador: sigue el orden físico de las sentencias.
- Tiempo de ejecución
	- Interprete: por cada sentencia se realiza el proceso de decodificación para determinas las operaciones a ejecutar y sus operandos. Si la sentencia está en un proceso iterativo, se realiza la tarea tantas veces como sea requerido. Puede afectar la velocidad de proceso.
	- Compilador: genera código de máquina para cada sentencia. No repite lazos, se decodifica una sola vez.
- Eficiencia:
	-  Interprete: más lento en ejecución. Se repite el proceso cada vez que se ejecuta el programa.
	- Compilador: más rápido desde el punto de vista del hardware, pero tarda más en compilar. Detectó más errores al pasar por todas las sentencias. Está listo para ser ejecutado. Ya compilado es más eficiente.
- Espacio que ocupa:
	- Interprete: ocupa menos espacio de memoria ya que cada sentencia se deja en la forma original y las instrucciones necesarias para ejecutarlas se almacenan en los subprogramas del interprete en memoria.
	- Compilador: una sentencia puede ocupar decenas o centenas de sentencias de máquina al pasar a código objeto
- Detección de errores
	- Interprete: las sentencias del código fuente puede ser relacionadas directamente con la que se está ejecutando. Se puede ubicar el error, es más fácil detectarlos por donde pasa la ejecución y es más fácil corregirlos
	- Compilador: le cuesta más determinar los errores ya que cualquier referencia al código fuente se pierden en el código objeto. Se pierde la referencia entre el código fuente y el código objeto. Es casi imposible ubicar el error.

### Ejercicio 4: Explique claramente la diferencia entre un error sintáctico y uno semántico. Ejemplifique cada caso.
- Error sintáctico: ocurre cuando el código no sigue las reglas gramaticales del lenguaje de programación. El formato puede estar especificado en documentos BNF/EBNF. Estos errores son detectados por el analizador sintáctico del lenguaje durante la fase de compilación o interpretación. Ejemplo en java:

		public String getName(){
			String x = "hola";
		}
- El error sintáctico se produce debido a la ausencia de una sentencia de return al finalizar el bloque del metodo.

- Error semántico: ocurre cuando el código está bien formado desde el punto de vista sintáctico, pero no produce los resultados esperados debido a una interpretación incorrecta del significado del código. Hay errores semánticos que se detectan en compilación (semántica estática) y otros durante la ejecución (semántica dinámica). Ejemplo en java:

		String nombre;
		nombre = 10 + 5;

- Si bien sintácticamente el programa es correcto, este produce un error semántico porque intentamos asignar a nombre como el resultado de una suma, operación la cual no está asociada a las variables de tipo String.

### Ejercicio 6: Explique cuál es la semántica para las variables predefinidas en lenguaje Ruby self y nil. ¿Qué valor toman; cómo son usadas por el lenguaje?
- self: es una variable especial que hace referencia al objeto actual. En un contexto de clase, self hace referencia a la clase misma. Esta se puede usar dentro de métodos de clase para hacer referencia a la clase en la que se está definiendo el método. Al iniciar el intérprete, sel tiene el valor main, ya que este es el primer objeto que se crea.
- nil: es ub objeto especial que representa la ausencia de valor. Es el equivalente a null. Se utiliza para indicar que una variable o expresión no tiene valor asignado o no retorna nada. 

### Ejercicio 7: Determine la semántica de null y undefined para valores en javascript.¿Qué diferencia hay entre ellos?

- null: representa intencionalmente un valor nulo o "vacío"
- undefined: una variable a la que no se le ha asignado valor, o no se ha declarado en absoluto (no se declara, no existe)
	- La diferencia es que null es intencionalmente declarada como vacio o nulo, undefined no, es asignado sólo por Javascript de forma automática como valor inicial cuando se define una variable y no se le dá un valor.

### Ejercicio 8: Determine la semántica de la sentencia break en C, PHP, javascript y Ruby. Cite las características más importantes de esta sentencia para cada lenguaje
- C: La instrucción break finaliza la ejecución de la instrucción do, for, switch o while más próxima que la incluya. El control pasa a la instrucción que hay a continuación de la instrucción finalizada. La instrucción break se usa con frecuencia para finalizar el procesamiento de un caso concreto en una instrucción switch. Si no existe una instrucción iterativa o una instrucción switch incluyente, se genera un error.
- PHP: break finaliza la ejecución de la estructura for, foreach, while, do-while o switch en curso. break acepta un argumento numérico opcional que indica de cuántas estructuras anidadas circundantes se debe salir. El valor predeterminado es 1, es decir, solamente se sale de la estructura circundante inmediata.
- JavaScript: Termina el bucle actual, sentecia switch o label y transfiere el control del programa a la siguiente sentencia de terminación de éstos elementos. La sentencia break incluye una etiqueta opcional que permite al programa salir de una sentencia etiquetada. La sentencia break necesita estar anidada dentro de la sentencia etiquetada. La sentencia etiquetada puede ser cualquier tipo de sentencia; no tiene que ser una sentencia de bucle.
- Ruby: usado para terminar un bucle actual, normalmente usado en bucles while true. Podemos definir una condición que se debe cumplir para que se ejecute el break (en la misma línea de este) → break if condición. Otro uso potente es que break puede recibir argumentos que devolverá al terminar el bucle.

### Ejercicio 9: Defina el concepto de ligadura y su importancia respecto de la semántica de un programa. ¿Qué diferencias hay entre ligadura estática y dinámica? Cite ejemplos (proponer casos sencillos)

- Los programas trabajan con entidades, estas entidades tienen atributos que tienen que establecerse antes de poder usar la entidad. La ligadura es la asociación entre la entidad y el atributo.
	- Una ligadura es estática si se establece antes de la ejecución y no se puede cambiar. El termino estática referencia al momento del binding y a su estabilidad
	- Una ligadura es dinámica si se establece en el momento de la ejecución y puede cambiarse de acuerdo con alguna regla especifica del lenguaje. Excepción: constantes