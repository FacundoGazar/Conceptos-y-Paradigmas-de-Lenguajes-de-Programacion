# Práctica 5

## Ejercicio 1: Explique claramente cual es la utilidad del registro de activación y que representan cada una de sus partes.(Basado en el modelo debajo detallado)

Modelo de registro de activación

|Head|
|-|
|Pto retorno|
|EE (enlace estático)|
|ED (enlace dinámico)|
|Variables...|
|...|
|Parámetros...|
|...|
|Procedimientos...|
|...|
|Funciones...|
|...|
|Valor de retorno|

## Ejercicio 2: Dado el siguiente programa escrito en Pascal-like, continuar la realización de las pilas de ejecución hasta finalizar las mismas.

a) Siguiendo la cadena estática b) Siguiendo la cadena dinámica

```Pascal
Program Main
	Var a: array[1..10] of integer;
	x,y,z:integer;
	Procedure A ()
	var y,t: integer;
	begin
		a(1):= a(1)+1;z:=z+1;
		t:=1; y:=2;
		B(); a(y):=a(y)+3; y:=y+1;
		If z=11 Then Begin
			a(z-1):=a(z-2) + 3; z:=z-4;
			a(z-y):=a(z) – a(y) + 5;
		End;
	end;
	Function t():integer
	begin
		y:=y+1; z:=z-6;
		return(y+x);
	end;
	Procedure B()
	var d:integer;
	Procedure I ()
	begin
		x:=0; x:=x+6;
	end;
	begin
		x:=x+t; d:=0;
		while x>d do begin
			I(); x:=x-1;
			d:=d + 2;
		end;
	end;
begin
	For x:=1 To 10 do a(x):=x;
	x:=5; y:=1; z:=10;
	A();
	For x:=1 To 10 do write(a(x),x);
end.
```

Nota: La forma de evaluación de este lenguaje es de izquierda a derecha

Siguiendo la cadena estática:

|*1|
|--|
|PR|
|LE= -|
|LD= -|
|a(1)= ~~1~~ 2|
|a(2)= ~~2~~ 5|
|a(3)= 3|
|a(4)= 4|
|a(5)= 5|
|a(6)= 6|
|a(7)= 7|
|a(8)= 8|
|a(9)= 9|
|a(10)= 10|
|x= ~~1..10~~ ~~5~~ ~~12~~ ~~0~~ ~~6~~ ~~5~~ ~~0~~ ~~6~~ ~~5~~ ~~0~~ ~~6~~ 5|
|y= ~~1~~ 2|
|z= ~~10~~ ~~11~~ 5|
|Proc. A|
|Fun. t|
|Proc. B|
|VR=|
##
|*2|
|-|
|PR|
|LE= *1|
|LD= *1|
|y= ~~2~~ 3|
|t= 1|
|VR= |
##
|*3|
|-|
|PR|
|LE= *1|
|LD= *2|
|d= ~~0~~ ~~2~~ ~~9~~ 6|
|Proc. I|
|VR= 7|
##
|*4|
|-|
|PR|
|LE= *1|
|LD= *3|
|VR|
##
|*5|
|-|
|PR|
|LE= *3|
|LD= *3|
|VR|
##
|*6|
|-|
|PR|
|LE= *3|
|LD= *3|
|VR|
##
|*7|
|-|
|PR|
|LE= *3|
|LD= *3|
|VR|


## Ejercicio 3: Sea el siguiente programa escrito en Pascal-like. Realice la pila de ejecución

1. Siguiendo la cadena estática
2.  Siguiendo la cadena dinámica

```Pascal
PROGRAM P1;
var
	a:integer;
	b:char;
	c: array[1..10] of integer
Procedure PP1;
var
	a:char;
	p:integer;
Function x: integer;
var
	z:integer;
begin
	a:="j";
	z=-1;
	return z;
end;

Begin
	p:=x;
	write(a);
	p:=x+3;
	c[p]=8;
	p:=x+2;
	c[p]=x;
end;
Procedure x;
var
	b:char;
Procedure PP2;
Begin
	write("para qué estoy aquí?");
end;
Begin
	a:=1;
	c[a]:=4;
	b:="a";
	write(concat(c[1],b));
	PP1();
	b:="b";
	write(concat(c[5],b));
End;
BEGIN
	a:=3;
	b:="c";
	for a:=3 to 10 do
	begin
		c[a]:=2*a;
	end;
	x;
	write(b);
	write(a);
	for a:=1 to 10 do
		write(c[a]-3);
END.
```

Siguiendo la cadena dinámica:

|*1|
|-|
|PR|
|a= ~~3~~ ~~3..10~~ ~~1~~ 1.10|
|b= c|
|c(1)= ~~4~~ -1|
|c(2)= 8|
|c(3)= 6|
|c(4)= 8|
|c(5)= 10|
|c(6)= 12|
|c(7)= 14|
|c(8)= 16|
|c(9)= 18|
|c(10)= 20|
|Proc. PP1|
|Proc. X|
|VR|
##
|*2|
|-|
|PR|
|LE= *1|
|LD= *1|
|b= ~~a~~ b|
|PP2|
|VR|
##
|*3|
|-|
|PR|
|LE= *1|
|LD= *2|
|a= ~~j~~ ~~j~~ ~~j~~ j|
|p= ~~2~~ ~~2~~ 1|
|Fun. x|
|VR= -1 -1 -1 -1|
##
|*4|
|-|
|PR|
|LE= *3|
|LD= *3|
|z= -1|
|VR|
##
|*5|
|-|
|PR|
|LE= *3|
|LD= *3|
|z= -1|
|VR|
##
|*6|
|-|
|PR|
|LE= *3|
|LD= *3|
|z= -1|
|VR|
##
|*7|
|-|
|PR|
|LE= *3|
|LD= *3|
|z= -1|
|VR|

> Imprime:
> 4a
> j
> 10b
> c
> 1
> -4
> 5
> 3
> 5
> 7
> 9
> 11
> 13
> 15
> 17

## Ejercicio 4: Sea el siguiente programa escrito en Pascal-like. Realice la pila de ejecución
1. Siguiendo la cadena estática
2. Siguiendo la cadena dinámica

```Pascal
Procedure Main;
	var x, y: integer;
	vec: array[1..7] of integer;
Function B:integer;
	var y:integer;
begin
	y:=4; 
	x:= y - 2;
	return (x);
end;
Procedure D;
	var i, x: integer;
	vec: array[1..7] of integer;
	Procedure A;
		var y:integer;
	begin
		y:=x + 5; 
		vec(i + 2):= vec(i + 2) + y;
		x:= x +B; 
		C;
	end;
	Function B:integer;
	begin
		vec(i):= y + 2; 
		i:=i+2;
		vec(i):= vec(1) * i;
		return ( vec(i)-vec(1) );
	end;
begin
	for x:= 1 to 7 do 
		vec(x):= 1;
	x:=1; 
	i:= 2;
	if y = 7 then 
		A; 
	else 
		C;
	for x:= 1 to 7 do 
		write(vec(x));
end;
Procedure C;
	var i, y: integer;
begin
	i:= 1; 
	y:= 6; 
	x:= x + B;
	vec(2):= vec(2) * x;
	while (i < y) do begin
		vec(i):= vec(i) + B - 1;
		i:= i + 3;
	end;
	y:= y - 4;
end;
begin
	for x:= 1 to 7 do 
		vec(x):= x;
	x:= 3; 
	y:= B+5; 
	D;
	if (x = 2) then begin
		vec(x):= vec(x) + 2;
		vec(x + 3):= vec(x) * 3;
	end;
	for x:= 1 to 7 do 
		write(vec(x));
end.
```

**a)** 

|*1|
|-|
|PR|
|x= ~~1..7~~ ~~3~~ ~~2~~ ~~2~~ ~~4~~ ~~2~~ ~~2~~ ~~1~~..7|
|y= 7|
|vec(1)=  ~~1~~ ~~2~~ 3|
|vec(2)=  ~~2~~ ~~8~~ 10|
|vec(3)=  3|
|vec(4)=  4|
|vec(5)=  ~~5~~ 30|
|vec(6)=  6|
|vec(7)=  7|
|Func B |
|Proc D |
|Proc C |
|VR= 2 |
##
|*2|
|-|
|PR|
|LE= *1|
|LD= *1|
|y= 4|
|VR=|
##
|*3|
|-|
|PR|
|LE= *1|
|LD= *1|
|i= ~~2~~ 4|
|x= ~~1..7~~ ~~1~~ ~~4~~ ~~1~~..7|
|vec(1)= 1|
|vec(2)= ~~1~~ 9|
|vec(3)= 1|
|vec(4)= ~~1~~ ~~7~~ 4|
|vec(5)= 1|
|vec(6)= 1|
|vec(7)= 1|
|Proc. A|
|Func B|
|VR=|
##
|*4|
|-|
|PR|
|LE= *3|
|LD= *3|
|y= 6|
|VR= 3|
##
|*5|
|-|
|PR|
|LE= *3|
|LD= *4|
|VR= |
##
|*6|
|-|
|PR|
|LE= *1|
|LD= *4|
|i= ~~1~~ ~~4~~ 7|
|y= ~~6~~ 2|
|VR= 2 2|
##
|*7|
|-|
|LE= *1|
|LD= *6|
|y= 4|
|VR= |
##
|*8|
|-|
|PR|
|LE= *1|
|LD= *6|
|y= 4|
|VR= |
##
|*9|
|-|
|PR|
|LE= *1|
|LD= *6|
|y= 4|
|VR= |

> Imprime:
> 1
> 9
> 1
> 4
> 1
> 1
> 1
> 3
> 10
> 3
> 4
> 30
> 6
> 7

## Ejercicio 5: Sea el siguiente programa escrito en Pascal-like. Realice la pila de ejecución
1. Siguiendo la cadena estática
2. Siguiendo la cadena dinámica
3. La sentencia x:= c + 5 +x, podría reemplazarse por x:= x + c + 5? Justifique la
respuesta

```Pascal
Program Main;
	Var x, y, z:integer;
	a, b: array[1..6] of integer;
Procedure B;
	var y,x: integer;
	Procedure C;
		var c:integer;
	begin
		y:= y + 2; 
		c:=2;
		a(x):=a(x)*y;
		if (y >7) then
			b(y-6)=b(4)*2+b(y-6);
		D;
	end;
begin
	x:=2; 
	y:= x + 3;
	C; 
	x:= x + 1; 
	write (x,y);
End;
Procedure D;
begin
	x:= c + 5 + x;
	y:= y + 2;
end;
Function C: integer;
begin
	b(x):= b(x) + 1;
	x:= x + 1;
	a(y):=a(y)+b(x)+3;
	a(x+2)=a(x) + 2;
	return b(x);
end
begin
	x:= 1; 
	Y:= 2;
	for z:=1 to 6 do begin
		a(z):= z;
		b(z):= z + 2;
	end;
	B;
	for z:= to 6 do 
		write (a(z), b(z));
end.
```

**b)**

|*1 Registro de activación Main|
|-|
|PR|
|x= 1|
|y= 2|
|z= ~~1..6~~  ~~1~~..6|
|a(1)= 1|
|a(2)= ~~2~~ 14|
|a(3)= 3|
|a(4)= 4|
|a(5)= 5|
|a(6)= 6|
|b(1)= 3|
|b(2)= 4|
|b(3)= 5|
|b(4)= 6|
|b(5)= 7|
|b(6)= 8|
|Proced. B|
|Proced. D|
|Func. C|
|VR|
##
|*2 Registro de activación Proced. B|
|-|
|PR|
|LE *1|
|LD *1|
|y= ~~5~~ ~~7~~ 9|
|x= ~~2~~ ~~9~~ 10|
|Prodec. C|
|VR|
##
|*3 Registro de activación Proced. C|
|-|
|PR|
|LE *2|
|LD *2|
|c= 2|
|VR|
##
|*4 Registro de activación Proced. D|
|-|
|PR|
|LE *1|
|LD *3|
|VR|


> Imprime: 
> 109
> 13
> 144
> 35
> 46
> 57
> 68
