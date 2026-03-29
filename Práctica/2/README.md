# Práctica 2

## Sintaxis

### Ejercicio 1: Complete el siguiente cuadro

| Meta símbolos utilizados por |  | Símbolo utilizado en Diagramas sintacticos|Significado  |
|--|--|--|--|
| BNF | EBNF | ||
| terminal|palabra terminal | ovalo|Definición de un elemento terminal|
|`< >` |`< >` | Rectangulo |Definición de un elemento no terminal|
|::=|::=| diagrama con rectángulos, óvalos y flechas|Meta-símbolo de definición que indica que el elemento a su izquierda se puede definir según el esquema de la derecha
|`|`|`(|)`|flecha que se divide en dos o más caminos| Selección de una alternativa
|`<p><p1>`|{}||Repetición
||*|*el que se ve en la explicacion practica*|Repetición de 0 o más veces
||+|*el que se ve en la explicacion practica*|Repetición de 1 o más veces
||[]|*el que se ve en la explicacion practica*|Opcional, está presente o no lo está

Nota: p y p1 son producciones simbólicas

### Ejercicio 2: ¿Cuál es la importancia de la sintaxis para un lenguaje? ¿Cuáles son sus elementos?

La sintaxis es el conjunto de reglas que definen cómo componer letras, dígitos y otros caracteres para formar los programas. Esta permite escribir programas correctos y válidos sintácticamente. Establece reglas para combinar componentes básicas, llamadas word y formar sentencias y programas. Es fundamental ya que dicta las reglas y estructuras que deben seguirse para escribir instrucciones válidas en el código fuente, es decir, establece las reglas para que el programador se comunique con el procesador de forma correcta sintácticamente.

Elementos que la componen: 
- alfabeto o conjunto de caracteres 
-  identificadores 
- operadores 
- palabra clave y palabra reservada 
- comentarios y uso de blancos

### Ejercicio 3: ¿Explique a qué se denomina regla lexicográfica y regla sintáctica?

 - **Reglas Léxicas**: conjunto de reglas para formar las “word”, a partir de los caracteres del alfabeto. Por ej. diferencias entre mayúsculas y minúsculas, símbolo de distinto != o <>.
 - **Reglas sintácticas**: conjunto de reglas que definen cómo son las sentencias y expresiones. Por ej. En C el if no lleva then, pero en Pascal sí

### Ejercicio 4: ¿En la definición de un lenguaje, a qué se llama palabra reservadas? ¿A qué son equivalentes en la definición de una gramática? De un ejemplo de palabra reservada en el lenguaje que más conoce. (Ada,C,Ruby,Python,..)

 - Palabra reservada: son palabras claves (palabras que tienen un significado dentro de un contexto) que además no pueden ser usadas por el programador como identificador de otra entidad.
 Equivale al conjunto de símbolos terminales de la gramática.
Por ejemplo en java: public, int, double, static, true, false, etc.

### Ejercicio 5: Dada la siguiente grámatica escrita en BNF:

- G = (N, T, S, P)
- N = `{<numero_entero>, <digito>}`
- T = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9}
- S = `<numero_entero>`
- P = {
    - `<numero_entero> ::= <digito><numero_entero> | <numero_entero><digito> | <digito>`
    - `<digito> ::= 0|...|9`

}

a- Identifique las componentes de la misma

 - G = 4-tupla de conjunto de reglas finitas que define un conjunto infinito de sentencias válidas en el lenguaje.
 - N = conjunto de símbolos no terminales.
 - T = conjunto de símbolos terminales.
 - S = símbolo distinguido de la gramática que pertenece a N.
 - P = conjunto de producciones.

b- Indique porqué es ambigua y corríjala

Es ambigua por `<digito><numero_entero> | <numero_entero><digito>`
La asociativa es por la izquierda o por la derecha, en este caso se estarían generando dos arboles de derivación.

***Corrección***
- G = {N, T, S, P}
- N = {`<digito><numero_entero>`}
- T = {0,1,2,3,4,5,6,7,8,9}
- S = `<numero_entero>`
- P = {
	- `<numero_entero> ::= <digito> |<digito><numero_entero>`
	- `<digito> ::= 0|...|9`
   
}

### Ejercicio 6: Defina en BNF (Gramática de contexto libre desarrollada por Backus- Naur) la gramática para la definición de una palabra cualquiera.

- G = (N, T, S, P)
- N = `{<palabra><letraMin><letraMay>`}
- T = {a,..., z, A,..., Z}
- S = `<palabra>`
- P = {
	- `<palabra> ::= <letraMin> | <letraMay> | <letraMay><palabra> | <letraMin><palabra>`
	- `<letraMin> ::= a | ... | z`
	- `<letraMay> ::= A | ... | Z`

}

### Ejercicio 7: Defina en EBNF la gramática para la definición de números reales. Inténtelo desarrollar para BNF y explique las diferencias con la utilización de la gramática EBNF.

EBNF:

- G = (N, T, S, P)
- N = {`<real><digito>`}
- T = {0,1,2,3,4,5,6,7,8,9,**,**}
- S = `<real>`
- P = {
	- `<real> ::= [-]{<digito>}+[,{<digito>}+]`

}

BNF: ***CONSULTAR***

- G = (N, T, S, P)
- N = {`<real><digito><signo><decimal><entero>`}
- T = {0,1,2,3,4,5,6,7,8,9,+,-,**,**}
- S = `<real>`
- P = {
	- `<real> ::= <digito> |<signo><digito> | <signo><digito><real> | <digito><real> |  <digito><decimal> | <signo><digito><decimal>`
	- `<decimal> ::= ,<entero>`
	- `<entero> ::= <digito> | <digito><entero>`
	- `<digito> ::= 0 | ... | 9`
	- `<signo> ::= + | -`
	- `<coma> ::= ,`

}

La diferencia radica en la complejidad de formar expresiones complejas, EBNF provee metasimbolos que simplifican la tarea de definir la gramatica. Por ejemplo con la repetición y opcionales.

### Ejercicio 8: Utilizando la gramática que desarrolló en los puntos 6 y 7, escriba el árbol sintáctico de:

a. Conceptos 
b. Programación 
c. 1255869 
d. 854,26 
e. Conceptos de lenguajes

**a.**

	<palabra>
	├── <letraMay>
	│   └── C
	└── <palabra>
	    ├── <letraMin>
	    │   └── o
	    └── <palabra>
	        ├── <letraMin>
	        │   └── n
	        └── <palabra>
	            ├── <letraMin>
	            │   └── c
	            └── <palabra>
	                ├── <letraMin>
	                │   └── e
	                └── <palabra>
	                    ├── <letraMin>
	                    │   └── p
	                    └── <palabra>
	                        ├── <letraMin>
	                        │   └── t
	                        └── <palabra>
	                            ├── <letraMin>
	                            │   └── o
	                            └── <palabra>
	                                └── <letraMin>
	                                    └── s

No hago la b y la c porque es obvio

**d.**

	<real>
	├── <digito>
	│   └── 8
	└── <real>
	    ├── <digito>
	    │   └── 5
	    └── <real>
	        ├── <digito>
	        │   └── 4
	        └── <decimal>
	            ├── ,
	            └── <entero>
	                ├── <digito>
	                │   └── 2
	                └── <entero>
	                    └── <digito>
	                        └── 6

La ***e*** no se puede hacer porque con las gramáticas definidas no se puede representar una cadena de texto, sino palabras individuales.

### Ejercicio 9: Defina utilizando diagramas sintácticos la gramática para la definición de un identificador de un lenguaje de programación. Tenga presente como regla que un identificador no puede comenzar con números.

***subido como imagen***

### Ejercicio 10:
a) Defina con EBNF la gramática para una expresión numérica, dónde intervienen variables y
números. Considerar los operadores +, -, * y / sin orden de prioridad. No considerar el uso de
paréntesis.

- G = (N, T, S, P)
- N = {`<exp><numero><op><digito>`}
- T = {0,...9,"+", "-", "*", "/"}
- S = `<exp>`
- P = {
	- `<exp> ::= (<var>|<numero>){<op>(<var>|<numero>)}+`
	- `<numero> ::= [(+|-)]{<digito>}+`
	- `<var> ::= <letra>{(<letra>|<digito>)}+`
	- `<digito> ::= 0 | ... | 9`
	- `<letra> ::= "a" | ... | "z" | "A" | ... | "Z"` 
	- `<op> ::= "+" | "-" | "*" | "/"`

}


b) A la gramática definida en el ejercicio anterior agregarle prioridad de operadores.
c) Describa con sus palabras los pasos y decisiones que tomó para agregarle prioridad de operadores al ejercicio anterior.

### Ejercicio 11: La siguiente gramática intenta describir sintácticamente la sentencia for de ADA, indique cuál/cuáles son los errores justificando la respuesta.

### Ejercicio 12: Realice en EBNF la gramática para la definición un tag div en html 5. (Puede ayudarse con el siguiente enlace (https://developer.mozilla.org/es/docs/Web/HTML/Elemento/div)

- G = (N, T, S, P)
- N = {`<div><palabra><source><letra>`}
- T = {`ASCII, ".jpg", "<div class=""", """<img src=""", """alt=""", """<p>""","""</p></div>""`}
- S = `<div>`
- P = {
	- `<div> ::= "<div class=""<palabra>>""<img src=""<source>""alt=""<palabra>""<p>""<palabra>""</p></div>"`
	- `<palabra> ::= {<letra>}+`
	- `<source> ::= <palabra>".jpg"`
	- `<letra> ::= ASCII (no se como poner todos)`

}

### Ejercicio 13: Defina en EBNF una gramática para la construcción de números primos.¿Qué debería agregar a la gramática para completar el ejercicio?

### Ejercicio 14: Sobre un lenguaje de su preferencia escriba en EBNF la gramática para la definición de funciones o métodos o procedimientos (considere los parámetros en caso de ser necesario)

JAVA

- G = (N, T, S, P)
- N = {`<metodo><firma><bloque><parametros><palabra><letra><tipo_retorno>`}
- T = {"a", ..., "z", "A", ..., "Z", "void", "int", "double", "String", ..., "Object"}
- S = `<metodo>`
- P = {
	- `<metodo> ::= <firma>[<bloque>]`
	- `<firma> ::= <scope>["static"]<tipo_retorno><palabra>"("[{<parametros>}*]")"`
	- `<parametros> ::= {<tipo><palabra>}*`
	- `<bloque> ::= [{<palabra>}*]["return"<tipo_retorno>]`
	- `<palabra> ::= {letra}*`
	- `<letra> ::= a | ... | z | A | ... | Z`
	- `<tipo_retorno> ::= "void" | int | double | String | ... | Object `

}


Python

- G = (N, T, S, P)
- N = {`<funcion><firma><bloque><palabra><letra>`}
- T = {"a", ..., "z", "A", ..., "Z"}
- S = `<funcion>`
- P = {
	- `<funcion> ::= <firma><bloque>`
	- `<firma> ::= "def("[{<parametros>}*]")"`
	- `<bloque> ::= [{<palabra>}*]`
	- `<palabra> ::= {<letra>}*`
	- `<letra> ::= a | ... | z | A | ... | Z`

}
