# Práctica 6

## Ejercicio 4: Sea el siguiente programa escrito en Pascal-like


- Arme el árbol de anidamiento sintáctico y el registro de activación de cada una de las unidades.

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

- Decir qué imprime el programa suponiendo que para todas las variables que se pasan el pasaje de parámetros es por: (Deberá hacer la pila estática y dinámica para cada caso) **i-** Referencia. **ii-** Valor **iii-** Valor Resultado **iv-** Nombre **v-** Resultado. 

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
|LE|
|LD|
|m= 5|
|VR|

> Imprime: 5 5 5

##

|RA de Recibe *3|
|-|
|PR|
|LE|
|LD|
|x= **apunta a i de +1**|
|y= **apunta a j de +1**|
|VR|

> Imprime; 5 5 5 5 6

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

> Imprime;  5 5 1 3 6

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

> Imprime; 5 5 1 3 6


##

- Cadena estática - Resultado

**EN LA ASIGNACION m:= m + 1 + y; DA ERROR PORQUE y NO TIENE UN VALOR ASIGNADO.  x e y son solo parámetros de salida, no tienen un valor asignado.**

- ¿Existió algún caso que no pudo realizarlo porque saltó algún tipo de error? Diga cuál y por qué. 
	- Sí, intentando usar pasaje de parámetros por Resultado. Tanto en cadena estática como dinámica.

-  ¿Dará el mismo resultado si se trata de un lenguaje que sigue la cadena dinámica? Justifique la respuesta realizando las pilas de activación
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

> Ya me canse de hacer esto para todos, directamente voy a decir que el a es los 3 referencia el el b es referencia valor referencia

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
|x= <- r1(y + r2(y))|
|t= <- r2(z)|
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
|t1= <- t|
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

