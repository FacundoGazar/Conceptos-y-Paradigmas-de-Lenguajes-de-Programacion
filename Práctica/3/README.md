
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

### Ejercicio 5: Sean los siguientes ejemplos de programas. Analice y diga qué tipo de error se produce (Semántico o Sintáctico) y en qué momento se detectan dichos errores (Compilación o Ejecución). Aclaración: Los valores de la ayuda pueden ser mayores.

a) Pascal:

	Program P
	var 5: integer;
	var a:char;
	Begin
		for i:=5 to 10 do begin
			write(a);
			a=a+1;
		end;
	End.

- Errores sintácticos:
	- Falta el ";" luego de Program P. Se detecta en la compilación. La gramática de Pascal exige Program P;. El compilador detecta la ausencia del punto y coma al parsear el encabezado.
	- Identificador inválido en var 5: integer. Se detecta en la compilación. Un nombre de variable no puede comenzar con un dígito.
	- Operador de asignacion incorrecto en a = a+1. Se detecta en la compilación. En Pascal la asignación es ":=".

- Errores semánticos:
	- variable i no declarada en for i:= 5 to 10 - i. Se detecta en la compilación. El compilador lo detecta durante el análisis de la tabla de símbolos. No se puede usar un identificador sin declarar.
	- a no inicializada en write(a). Se detecta en ejecución. a está declarada como char pero nunca es inicializada. Pascal no garantiza un valor por defecto; el comportamiento es indefinido y el problema se manifiesta al ejecutar.

b) Java:

	public String tabla(int numero, arrayList<Boolean> listado)
	{
		String result = null;
		for(i = 1; i < 11; i--) {
			result += numero + "x" + i + "=" + (i*numero) + "\n";
			listado.get(listado.size()-1)=(BOOLEAN) numero>i;
		}
		return true;
	}

- Errores sintácticos:
	- BOOLEAN no existe, deberia ser boolean o Boolean.
	- listado.get(listado.size()-1)=(BOOLEAN) numero>i; deberia ser una variable.
	
- Errores semánticos:
	- La variable i en el for no está declarada. Se detecta en compilación. Ademas se genera un bucle infinito que se detecta en ejecución. **consultar**
	- El return true es un tipo incompatible con String. Se detecta en compilación. El método declara retornar un String pero devuelve un boolean. El compilador detecta la incompatibilidad de tipos. Se detecta en compilación.
	- result += ... — result es null. Se detecta en ejecución.

**consultar que seria el error de arrayListBoolean — nombre incorrecto**

c) C

	# include <stdio.h>
	int suma; /* Esta es una variable global */
	int main()
	{ int indice;
		encabezado;
		for (indice = 1 ; indice <= 7 ; indice ++)
		cuadrado (indice);
		final(); Llama a la función final */
		return 0;
	}
	cuadrado (numero)
	int numero;
	{ int numero_cuadrado;
		numero_cuadrado == numero * numero;
		suma += numero_cuadrado;
		printf("El cuadrado de %d es %d\n",
		numero, numero_cuadrado);
	}

- Errores sintácticos:
	- final(); Llama a la función final */ — comentario sin apertura. Se detecta en compilación. Falta el de apertura. El compilador ve texto libre fuera de una cadena y falla al parsear.

- Errores semánticos:
	- encabezado; — llamada sin paréntesis ni declaración previa. Se detecta en la compilación.
	- cuadrado(numero) — sin tipo de retorno. Se detecta en compilación.
	- int numero; — estilo K&R de declaración de parámetros. Se detecta en compilación.
	- numero_cuadrado == numero * numero. Se detecta en ejecución. Se usa == (comparacion) en lugar de = (asignacion). Sintácticamente es válido en C (es una expresión); el compilador puede emitir una advertencia pero compila. El resultado: numero_cuadrado queda sin inicializar y printf imprime basura en tiempo de ejecución.
	- suma += numero_cuadrado — variable acumulada sin inicializar. Se detecta en ejecución. suma es global y se inicializa a 0 por el estándar C, pero numero_cuadrado nunca recibe valor (por el error anterior). El acumulado resulta en un valor indefinido.

d) Python:

	#!/usr/bin/python
	print "\nDEFINICION DE NUMEROS PRIMOS"
	r = 1
	while r = True:
		N = input("\nDame el numero a analizar: ")
		i = 3
		fact = 0
		if (N mod 2 == 0) and (N != 2):
			print "\nEl numero %d NO es primo\n" % N
		else:
			while i <= (N^0.5):
				if (N % i) == 0:
					mensaje="\nEl numero ingresado NO es primo\n" % N
					msg = mensaje[4:6]
					print msg
					fact = 1
				i+=2
			if fact == 0:
				print "\nEl numero %d SI es primo\n" % N
	r = input("Consultar otro número? SI (1) o NO (0)--->> ")

- Erres sintácticos:
	- print "\nDEFINICION..." — sintaxis Python 2. Se detecta en compilación. En Python 3, print es una función: se requiere print(...). El intérprete detecta esto en la fase de parsing, antes de ejecutar.
	- while r = True: — asignación en condición. Se detecta en compilación. Python no permite = dentro de una expresión condicional. El parser lo rechaza de inmediato. La forma correcta sería while r == True: o while r:.
	- if (N mod 2 == 0) — operador inexistente. Se detecta en compilación. 

- Errores semánticos:
	- while i <= (N^0.5) — operador XOR en lugar de potencia. Se detecta en ejecución. La potencia en python no se hace con ese simbolo.
	- if (N mod 2 == 0) and (N != 2). Hay que parsear a n a int con (int). Se detecta en compilacion.

e) Ruby:

	def ej1
		Puts 'Hola, ¿Cuál es tu nombre?'
		nom = gets.chomp
		puts 'Mi nombre es ', + nom
		puts 'Mi sobrenombre es 'Juan''
		puts 'Tengo 10 años'
		meses = edad*12
		dias = 'meses' *30
		hs= 'dias * 24'
		puts 'Eso es: meses + ' meses o ' + dias + ' días o ' + hs + ' horas'
		puts 'vos cuántos años tenés'
		edad2 = gets.chomp
		edad = edad + edad2.to_i
		puts 'entre ambos tenemos ' + edad + ' años'
		puts '¿Sabes que hay ' + name.length.to_s + ' caracteres en tu nombre, ' + name + '?'
	end

- Errores sintácticos:
	- Puts 'Hola, ¿Cuál es tu nombre?' puts va con mayuscula
	- puts 'Mi sobrenombre es 'Juan'' se cierra el ‘’ y se sigue escribiendo, falta un “

- Errores semánticos:
	- meses = edad*12 nunca se declaró la edad. Se detecta en compilación.
	- puts 'Eso es: meses + ' meses o ' + dias + ' días o ' + hs + ' horas' no existen las variables meses o y días o . Se detecta en compilación.
	- edad = edad + edad2.to_i edad no está declarada. Se detecta en compilación.
	- puts '¿Sabes que hay ' + name.length.to_s + ' caracteres en tu nombre, ' + name + '?' name no esta definido. Se detecta en compilación.

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
