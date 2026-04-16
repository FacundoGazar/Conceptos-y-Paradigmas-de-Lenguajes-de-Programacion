
# Práctica 4

### Ejercicio 1: a) Tome una de las variables de la línea 3 del siguiente código e indique y defina cuales son sus atributos:

	1. Procedure Practica4();
	2. var
	3. a,i:integer
	4. p:puntero
	5. Begin
	6. a:=0;
	7. new(p);
	8. p:= ^i
	9. for i:=1 to 9 do
	10.a:=a+i;
	11.end;
	12....
	13.p:= ^a;
	14....
	15.dispose(p);
	16.end;

variable **a**:
- Nombre: a
- Alcance: estático, 3-16
- Tipo: predefinido integer, ligadura estática
- L-Value: automática
- R-Value: indefinido 
- Lifetime: 1-16

### b) Compare los atributos de la variable del punto a) con los atributos de la variable de la línea 4. Que dato contiene esta variable?

variable **p**:
- Nombre: p
- Alcance: estático, 4-16
- Tipo: definido puntero, ligadura estática
- L-Value: p automática, p^ dinámica 
- R-Value: p indefinido, p^ indefinido 
- Lifetime: p 1-16, p^ ?

### Ejercicio 2: 
a. Indique cuales son las diferentes formas de inicializar una variable en el momento de la declaración de la misma. 

- **Inicialización por defecto**: las variables se inicializan con un valor por defecto, por ejemplo los enteros en 0, los caracteres en blanco, etc.
- **Inicialización en la declaración**: las variables pueden inicializarse en el mismo momento que se declaran, por ejemplo “int i = 0;”.
- **Ignorar el problema**: la variable toma como valor inicial lo que hay en memoria (la cadena de bits asociados al área de almacenamiento). Puede llevar a errores y requiere chequeos adicionales.

b. Analice en los lenguajes: Java, C, Phyton y Ruby las diferentes formas de inicialización de variables que poseen. Realice un cuadro comparativo de esta característica.

**HACER DESPUES**

### Ejercicio 3: Explique los siguientes conceptos asociados al atributo l-valor de una:

1.  Variable estática
2. Variable automática o semiestática.
3. Variable dinámica.
4. Variable semidinámica.

### Ejercicio 4: 

1.  ¿A qué se denomina variable local y a qué se denomina variable global?
2. ¿Una variable local puede ser estática respecto de su l-valor? En caso afirmativo dé un ejemplo
3. Una variable global ¿siempre es estática? Justifique la respuesta
4. Indique qué diferencia hay entre una variable estática respecto de su l-valor y una constante

### Ejercicio 5:  
1.  En Ada hay dos tipos de constantes, las numéricas y las comunes. Indique a que se debe dicha clasificación. 

2. En base a lo respondido en el punto a), determine el momento de ligadura de las constantes del siguiente código: 

				H: constant Float:= 3,5; 
				I: constant:= 2; 
				K: constant float:= H*I;

### a. Tipos de constantes en Ada y su clasificación

La clasificación entre "constantes numéricas" (conocidas formalmente en Ada como _named numbers_ o números nombrados) y "constantes comunes" (objetos constantes) se debe fundamentalmente a **cómo el compilador maneja su tipado, su asignación en memoria y su momento de evaluación**.

**Característica**

**Constantes Numéricas (Named numbers)**

**Constantes Comunes (Objetos constantes)**

**Declaración explícita**

**No** llevan tipo.

**Sí** llevan tipo (ej. `Integer`, `Float`).

**Naturaleza**

Son identificadores simbólicos para valores matemáticos puros (tipo implícito `universal_integer` o `universal_real`).

Son variables reales en memoria, pero de solo lectura.

**Uso de Memoria**

Generalmente no ocupan espacio en memoria en tiempo de ejecución; el compilador reemplaza el nombre por el valor.

Ocupan espacio en la memoria RAM asignada según el tamaño del tipo especificado.

**Precisión**

Tienen precisión perfecta (la máxima que soporte el compilador internamente).

Limitada por la representación del tipo en el hardware (ej. 32 o 64 bits para un Float).

----------

### b. Momento de ligadura (Binding Time)

El "momento de ligadura" se refiere a cuándo se asocia de forma definitiva el valor y la dirección de memoria al identificador.

**1. `H: constant Float:= 3.5;`**

-   **Clasificación:** Constante común.
    
-   **Momento de ligadura:** **Tiempo de ejecución** (específicamente durante la _elaboración_ de la declaración). El sistema reserva una dirección de memoria para un tipo `Float` y almacena el valor.
    

**2. `I: constant:= 2;`**

-   **Clasificación:** Constante numérica.
    
-   **Momento de ligadura:** **Tiempo de compilación** (o tiempo de traducción). Como no tiene tipo explícito, el compilador evalúa el valor `2` y lo asocia al símbolo `I` estáticamente. Durante la compilación, cualquier uso de `I` se reemplaza directamente por el literal `2`.
    

**3. `K: constant float:= H*I;`**

-   **Clasificación:** Constante común.
    
-   **Momento de ligadura:** **Tiempo de ejecución**. Para determinar el valor de `K`, el programa necesita estar corriendo para evaluar la expresión (leer la memoria de `H`, realizar la multiplicación) y luego asignar ese resultado a la dirección de memoria reservada para `K`.
    
### Ejercicio 6: Sea el siguiente archivo con funciones de C: 
*** COMPLETAR CODIGO ***
Analice si llegaría a tener el mismo comportamiento en cuanto a alocación de memoria, sacar la declaración (1) y colocar dentro de func1() la declaración static int x =1;

Tendría distinto comportamiento en cuanto a alocación de memoria porque **static int x =1** se alocaría en tiempo de compilación.

### Ejercicio 7: Sea el siguiente segmento de código escrito en Java, indique para los identificadores si son globales o locales.

Locales: edad y fN (dentro del método getEdad).
Globales: todas las demás, las variables de las clases.

### Ejercicio 8: Sea el siguiente ejercicio escrito en Pascal

	1- Program Uno;
	2- type tpuntero= ^integer;
	3- var mipuntero: tpuntero;
	4- var i:integer;
	5- var h:integer;
	6- Begin
	7- 		i:=3;
	8- 		mipuntero:=nil;
	9- 		new(mipuntero);
	10- 	mipunterno^:=i;
	11- 	h:= mipuntero^+i;
	12- 	dispose(mipuntero);
	13- 	write(h);
	14- 	i:= h- mipuntero;
	15- End.

1. Indique el rango de instrucciones que representa el tiempo de vida de las variables i, h y mipuntero.
- i: 1-15
- h: 1-15
- mipuntero: 1-15
2. Indique el rango de instrucciones que representa el alcance de las variables i, h y mipuntero.
- i: 4-15
- h: 5-15
- mipuntero: 3-15
3. Indique si el programa anterior presenta un error al intentar escribir el valor de h. Justifique
- Al llegar a la línea 13 (`write(h);`), el compilador simplemente busca el valor almacenado en `h` e imprime el número `6` en pantalla sin arrojar ningún tipo de error.
4. Indique si el programa anterior presenta un error al intentar asignar a i la resta de h con mipuntero.
Justifique
- Pascal es un lenguaje fuertemente tipado, lo que significa que es muy estricto con las operaciones entre diferentes tipos de datos. En la línea `i:= h - mipuntero;` se está intentando mezclar dos tipos incompatibles:
-   `h` es  `integer`.    
-   `mipuntero` es una dirección de memoria (`^integer`).
5. Determine si existe otra entidad que necesite ligar los atributos de alcance y tiempo de vida para
justificar las respuestas anteriores. En ese caso indique cuál es la entidad y especifique su tiempo
de vida y alcance.
- La entidad faltante es el **programa principal**, este necesita ligar los atributos de alcance y tiempo de vida para justificar las respuestas anteriores. Tiene alcance global y su tiempo de vida es desde su declaración hasta el final del programa (6 –15).
6. Especifique el tipo de variable de acuerdo a la ligadura con el l-valor de las variables que encontró
en el ejercicio.
- Variable “i”: Automática, Integer. 
- Variable “h”: Automática, Integer. 
- Variable “mipuntero”: Automática, Puntero. 
- Variable “mipuntero^”: Dinámica, Integer.

### Ejercicio 9: Elija un lenguaje y escriba un ejemplo: 

1. En el cual el tiempo de vida de un identificador sea mayor que su alcance 
2. En el cual el tiempo de vida de un identificador sea menor que su alcance 
3. En el cual el tiempo de vida de un identificador sea igual que su alcance

### Ejercicio 10: Si tengo la siguiente declaración al comienzo de un procedimiento: 
	int c; **en C** 
	var c:integer; **en Pascal** 
	c: integer; **en ADA** 
	
Y ese procedimiento NO contiene definiciones de procedimientos internos. ¿Puedo asegurar que el alcance y el tiempo de vida de la variable “c” es siempre todo el procedimiento en donde se encuentra definida?. Analícelo y justifique la respuesta, para todos los casos. 
- Sí, para todos los casos, ya que no existen subprocesos internos que puedan modificar el alcance o el tiempo de vida de la misma.

### Ejercicio 11: 

1. Responda Verdadero o Falso para cada opción. 
El tipo de dato de una variable es? 
I) Un string de caracteres que se usa para referenciar a la variable y operaciones que se pueden realizar sobre ella.  **F**
II) Conjunto de valores que puede tomar y un rango de instrucciones en el que se conoce el nombre.  **F**
III) Conjunto de valores que puede tomar y lugar de memoria asociado con la variable.  **F**
IV) Conjunto de valores que puede tomar y conjunto de operaciones que se pueden realizar sobre esos valores. **V**

2. Escriba la definición correcta de tipo de dato de una variable.
- La definición del inciso IV).

### Ejercicio 12: Sea el siguiente programa en ADA, completar el cuadro siguiente indicando para cada variable de que tipo es en cuanto al momento de ligadura de su l-valor, su r-valor al momento de alocación en memoria y para todos los identificadores cuál es su alcance y cual es su el tiempo de vida. Indicar para cada variable su r-valor al momento de alocación en memoria

	1. with text_io; use text_io;
	2. Procedure Main is;
	3. type vector is array(integer range <>);
	4. a, n, p:integer;
	5. v1:vector(1..100);
	6. c1: constant integer:=10;
	7. Procedure Uno is;
	8. type puntero is access integer;
	9. v2:vector(0..n);
	10. c1, c2: character;
	11. p,q: puntero;
		5. begin
			7.5.1. n:=4;
			7.5.2. v2(n):= v2(1) + v1(5);
			7.5.3. p:= new puntero;
			7.5.4. q:= p;
			7.5.5. .......
			7.5.6. free p;
			7.5.7. ......
			7.5.8. free q;
			7.5.9. ......
		7.6. end;
	12. begin
	13. n:=5;
	14. .....
	15. Uno;
	16. a:= n + 2;
	17. .....
	18. end

|Ident.|Tipo|R-Valor|Alcance|T.V.|
|-|-|-|-|-|
|main (lin. 2)|-|-|3-14|2-14|
|a (lin. 4)|automática|basura|5-14|1-14|
|n (lin. 4)|automática|basura|5-14|1-14|
|p (lin. 4)|automática|basura|5-14|1-14|
|v1 (lin. 5)|automática|basura|6-14|1-14|
|c1 (lin. 6)|automática|basura|7-7.3, 8-14|1-14|
|Uno (lin. 7)|-|-|7.1-14|7-7.6|
|v2 (lin. 7.2)|semidinámica|basura|7.3-7.6|7-7.6|
|c1 (lin. 7.3)|automática|basura|7.4-7.6|7-7.6|
|c2 (lin. 7.3)|automática|basura|7.4-7.6|7-7.6|
|p (lin. 7.4)|automática|null|7.5-7.6|7-7.6|
|q (lin. 7.4)|automática|null|7.5-7.6|7-7.6|
|pˆ (lin. 7.4)|dinámica|basura|7.5-7.6|7.5.3|
|qˆ (lin. 7.4)|dinámica|basura|7.5-7.6|7.5.4|


### Ejercicio 13: El nombre de una variable puede condicionar: 
- Su tiempo de vida.
- Su alcance.
- Su r-valor.
- Su tipo. 
Justifique la respuesta

### Ejercicio 14: Sean los siguientes archivos en C, los cuales se compilan juntos

Indicar para cada variable de que tipo es en cuanto al momento de ligadura de su l-valor. Indicar para cada identificador cuál es su alcance y cual es su el tiempo de vida. Indicar para cada variable su r-valor al momento de alocación en memoria

	ARCHIVO1.C
		1. int v1;
		2. int *a;
		3. Int fun2 ()
			4. { int v1, y;
			5. for(y=0; y<8; y++)
			6. { extern int v2;
			7. ...}
			8. }
		9. main()
			10. {static int var3;
			11. extern int v2;
			12. int v1, y;
			13. for(y=0; y<10; y++)
			14. { char var1='C';
			15. a=&v1;}
			16. }
	ARCHIVO2.C
		17. static int aux;
		18. int v2;
		19. static int fun2( )
			20. { extern int v1;
			21. aux=aux+1;
			22. …
			23. }
		24. int fun3( )
			25. { int aux;
			26. aux=aux+1;
			27. …
			28. }

|Ident.|Tipo|R-Valor|Alcance|T.V.|
|-|-|-|-|-|
|v1 (lin. 1)|automática|0|2-4, 9-12- 21-23|1-28|
|a (lin. 2)|automática|nil|3-28|1-28|
|*a (lin. 2)|dinámica|&v1|3-28|16|
|fun2 (lin. 3)|-|-|4-8|3-8|
|v1 (lin. 4)|automática|basura|5-8|3-8|
|y (lin. 4)|automática|basura|5-8|3-8|
|v2 (lin. 18)|automática|0|7-8, 12-16, 19-28|1-28|
|main (lin. 9)|-|-|10-16|9-16|
|var3 (lin. 10)|estática|0|11-16|<1-28>|
|v1 (lin. 12)|automática|basura|13-16|9-16|
|y (lin. 12)|automática|basura|13-16|9-16|
|var1 (lin. 14)|automática|basura|15-16|9-16|
|aux (lin. 17)|estática|0|18-25|<1-28>|
|aux (lin. 25)|automática|basura|26-28|24-28|
|fun2 (lin. 19)|-|-|20-23|19-23|
|fun3 (lin. 24)|-|-|25-28|24-28|

### Ejercicio 15 
Para javascript investigue la diferencia semántica para declarar una variable utilizando los modificadores const, var, let y la ausencia de cualquiera de estos. Compárelo con un lenguaje de su preferencia.
