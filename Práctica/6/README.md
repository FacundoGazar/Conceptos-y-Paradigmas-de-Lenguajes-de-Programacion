# Práctica 6

## Ejercicio 1: Explique brevemente los siguientes conceptos
- Parámetro: es una forma de compartir datos entre diferentes unidades. Es la más flexible y permite la transferencia de diferentes datos en cada llamada. Proporciona ventajas en legibilidad y modificabilidad.
- Parámetro real: es el valor, variable o expresión que se pasa en la invocación a una rutina. Se específica en la llamada.
- Parámetro formal: recibe el valor del parámetro real. Es la variable definida en la declaración de la rutina.
- Ligadura posicional: se establece la correspondencia entre reales y formales. Van en el mismo orden que la lista de parámetros.
- Ligadura por palabra clave o nombre: pueden estar colocados en distinto orden en la lista de parámetros.

## Ejercicio 2: Unir los siguientes puntos según corresponda y de una definición y un ejemplo de cada par.

	- Modo IN										Resultado
	- Modo OUT										Valor
	- Modo IN / OUT									Valor / Resultado
													Nombre
													Resultado de funciones
													Valor Constante
													Referencia

|Modo IN|Modo OUT| Modo IN/OUT
|-|-|-|
|Valor|Resultado|Valor/Resultado|
|Valor Constante|Resultado de funciones|Referencia|
|||Nombre|

## Ejercicio 3: 
1. Complete el siguiente cuadro según lo correspondiente a cada lenguaje:

|Tipo de pasaje de parámetros|Lenguaje|
|-|-|
|Modo IN: pasaje por valor o por valor constante. 
Modo OUT: pasaje por resultado.|
Modo IN/OUT: pasaje por referencia.|ADA|
|Modo IN: pasaje por valor.
|Modo OUT: se simula usando punteros.
|Modo IN/OUT: se usa el pasaje por referencia mediante punteros.|C|
|Modo IN: pasaje por valor
|Modo OUT: no tiene.
|Modo IN/OUT: pasaje por referencia de objetos.|Ruby|
|Modo IN: pasaje por valor y pasaje por referencia.
|Modo OUT: no tiene.
|Modo IN/OUT: no tiene. Se simula mediante objetos.|Java|
|Modo IN: pasaje por valor para inmutables y por referencia para mutables.
|Modo OUT: no tiene.
|Modo IN/OUT: pasaje por referencia para objetos mutables.|Python|

2. Ada es más seguro que Pascal, respecto al pasaje de parámetros en las funciones. Explique por qué.
	-  ADA es más seguro que Pascal en cuanto al pasaje de parámetros en las funciones debido a sus sistema de tipos más estricto y su sintaxis más clara y explícita para específicar los modos de paso de parámetros.
	
3. Explique cómo maneja Ada los tipos de parámetros in-out de acuerdo al tipo de dato
	- ADA maneja los parámetros IN-OUT de acuerdo al tipo de datos que se está utilizando, usa una técnica de paso por referencia para tipos de datos complejos, y una técnica de copia y devolución para tipos de datos más simples. Esto permite un manejo seguro y eficiente de los parámetros IN-OUT en los programas ADA.

## Ejercicio 4: Sea el siguiente programa escrito en Pascal-like
```Pascal
Program Main:
var j, m, i: integer

Procedure Recibe(x:integer, y:integer);
begin
	m:= m + 1 + y;
	x:= i + x + j;
	y:= m - 1;
end;

Procedure Dos;
var
	m:integer;
begin
	m:= 5;
	Recibe(i,j);
	write(i, j, m);
end;

begin
	m:= 2;
	i:= 1;
	j:= 3;
	write(i, j, m);
End.
```

1.  Arme el árbol de anidamiento sintáctico y el registro de activación de cada una de las unidades.

```Pascal
Main 
├── Recibe
└── Dos
```

|*1|
|-|
|PR|
|LE|
|LD|
|j|
|m|
|i|
|Recibe|
|Dos|
|VR|

##

|*2|
|-|
|PR|
|LE|
|LD|
|m|
|VR|

##

|*3|
|-|
|PR|
|LE|
|LD|
|VR|

2.  Decir qué imprime el programa suponiendo que para todas las variables que se pasan el pasaje de parámetros es por: (Deberá hacer la pila estática y dinámica para cada caso) **i-** Referencia. **ii-** Valor **iii-** Valor Resultado **iv-** Nombre **v-** Resultado. 

- Cadena estática - Referencia

|RA de Main *1|
|-|
|PR|
|LE|
|LD|
|j= ~~3~~ 5|
|m= ~~2~~ 6|
|i= ~~1~~ 5|
|Recibe|
|Dos|
|VR|

> Imprime: 5 5 6

##

|RA de Dos *2|
|-|
|PR|
|LE= *1|
|LD= *1|
|m= 5|
|VR|

> Imprime: 5 5 5

##

|RA de Recibe *3|
|-|
|PR|
|LE= *1|
|LD= *2|
|x= **apunta a i de +1**|
|y= **apunta a j de +1**|
|VR|

> Imprime: 5 5 5 5 6

##

- Cadena estática - Valor

|RA de Main *1|
|-|
|PR|
|LE|
|LD|
|j= 3|
|m= ~~2~~ 6|
|i= 1|
|Recibe|
|Dos|
|VR|

> Imprime: 1 3 6

##

|RA de Dos *2|
|-|
|PR|
|LE= *1|
|LD= *1|
|m= 5|
|VR|

> Imprime: 1 3 5

##

|RA de Recibe *3|
|-|
|PR|
|LE= *1|
|LD= *2|
|x= ~~1~~ 5|
|y= ~~3~~ 5|
|VR|

> Imprime:  5 5 1 3 6

##

- Cadena estática - Valor Resultado

|RA de Main *1|
|-|
|PR|
|LE|
|LD|
|j= ~~3~~ 5|
|m= ~~2~~ 6|
|i= ~~1~~ 5|
|Recibe|
|Dos|
|VR|

> Imprime: 5 5 6

##

|RA de Dos *2|
|-|
|PR|
|LE= *1|
|LD= *1|
|m= 5|
|VR|

> Imprime: 5 5 5

##

|RA de Recibe *3|
|-|
|PR|
|LE= *1|
|LD= *2|
|x= ~~1~~ 5|
|y= ~~3~~ 5|
|VR|

> Imprime: 5 5 1 3 6


##

- Cadena estática - Resultado

**EN LA ASIGNACION m:= m + 1 + y; DA ERROR PORQUE y NO TIENE UN VALOR ASIGNADO.  x e y son solo parámetros de salida, no tienen un valor asignado.**

3. ¿Existió algún caso que no pudo realizarlo porque saltó algún tipo de error? Diga cuál y por qué. 
	- Sí, intentando usar pasaje de parámetros por Resultado. Tanto en cadena estática como dinámica.

4. ¿Dará el mismo resultado si se trata de un lenguaje que sigue la cadena dinámica? Justifique la respuesta realizando las pilas de activación
	- No, no da el mismo resultado hacer por cadena dinámica que por estática.

## Ejercicio 5: Suponiendo que se está ejecutando un programa con el siguiente registro de activación en memoria y se llama al procedimiento rutina(iter,vec,a). Determine el tipo de parámetro que se deben utilizar en el llamado para que los resultados sean los siguientes:

1. (4,6,7),(4,6,7), 2, 2 
2. (3,5,6),(4,6,7), 2, 2 
3. (3,5,6),(5,5,6), 0, -1 <- POR VALOR

- Prueba con Valor

|*1|
|-|
|PR|
|LD|
|LE|
|Iter: true|
|Vec(1)= 3|
|Vec(2)= 5|
|Vec(3)= 6|
|a= -1|
|Rutina|
|VR|

##

|*2|
|-|
|PR|
|LD= *1|
|LE= *1|
|iteracion= ~~true~~ ~~true~~ false|
|vector(1)= ~~3~~ ~~4~~ 5|
|vector(2)= 5|
|vector(3)= 6|
|vit= ~~-1~~ ~~0~~ 0|
|VR|

> Ya me canse de hacer esto para todos, directamente voy a decir que el a es los 3 referencia el b es referencia valor referencia

## Ejercicio 6: Indique con un ejemplo el comportamiento del parámetro por nombre (en el parámetro formal) para los siguientes casos de parámetros reales:
- Un valor entero: se comporta exactamente igual que el pasaje por referencia.
- Una constante: equivalente a por valor.
- Un elemento de un arreglo: puede cambiar el suscripto entre las distintas referencias.
- Una expresión: se evalúa cada vez.
Que sucede en cada caso?

## Ejercicio 7: Realice la pila de ejecución del siguiente programa: 
a) siguiendo la cadena estática 

|RA de Uno *1|
|-|
|PR|
|LE|
|LD|
|y= ~~1~~..~~6~~ ~~1~~..~~5~~ ~~1~~ ~~2~~ ~~1~~..~~6~~ ~~1~~..~~5~~|
|z= ~~2~~ ~~3~~ 3|
|r1(1)= 2|
|r1(2)= ~~2~~ 3|
|r1(3)= 2|
|r1(4)= ~~2~~ 4|
|r1(5)= 2|
|r1(6)= 2|
|r2(1)= 1|
|r2(2)= ~~1~~ ~~2~~ ~~3~~ 4|
|r2(3)= ~~1~~ ~~3~~ 5|
|r2(4)= 1|
|r2(5)= 1|
|Proc. Dos|
|VR|

> Imprime: 2 3 2 4 2 2 1 4 5 1 1

##

|RA de Dos *2|
|-|
|PR|
|LE= *1|
|LD= *1|
|x= ↑ r1(y + r2(y))|
|t= ↑ r2(z)|
|io= apunta a **y** de *1|
|y= ~~2~~ 3|
|Proc. Dos|
|VR|

##

|RA de Dos *3|
|-|
|PR|
|LE= *2|
|LD= *2|
|t1= ↑ t|
|Proc. Tres|
|VR|

##

|RA de Tres *4|
|-|
|PR|
|LE= *3|
|LD= *3|
|VR|

b) siguiendo la cadena dinámica

