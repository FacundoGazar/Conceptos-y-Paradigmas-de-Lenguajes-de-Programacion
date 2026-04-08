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
- R-Value: indefinido **consultar**
- Lifetime: 1-16

### b) Compare los atributos de la variable del punto a) con los atributos de la variable de la línea 4. Que dato contiene esta variable?

variable **p**:
- Nombre: p
- Alcance: estático, 4-16
- Tipo: definido puntero, ligadura estática
- L-Value: p automática, p^ dinámica **CONSULTAR**
- R-Value: p indefinido, p^ indefinido **CONSULTAR**
- Lifetime: p 1-16, p^ ?**CONSULTAR**

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
