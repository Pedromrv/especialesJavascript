# Especiales JavaScript. 

## Estructura de Código

Las declaraciones se delimitan con un punto y coma:

```javascript
alert('Hola'); alert('Mundo');
```

En general, un salto de línea también se trata como un delimitador, por lo que también funciona:

```javascript
alert('Hola') alert('Mundo')
```

Esto se llama “inserción automática de punto y coma”. A veces no funciona, por ejemplo:

```javascript
alert("Habrá un error después de este mensaje.")  [1, 2].forEach(alert)
```

La mayoría de las guías de estilo de código coinciden en que debemos poner un punto y coma después de cada declaración.

Los puntos y comas no son necesarios después de los bloques de código `{...}` y los constructores de sintaxis como los bucles:

```javascript
function f() {   // no se necesita punto y coma después de la declaración de función }  
for(;;) {   // no se necesita punto y coma después del bucle }`
```

…Pero incluso si colocásemos un punto y coma “extra” en alguna parte, eso no sería un error. Solo sería ignorado.


## Modo estricto

Para habilitar completamente todas las características de JavaScript moderno, debemos comenzar los scripts con `"use strict"`.

```javascript
'use strict';  ...
```

La directiva debe estar en la parte superior de un script o al comienzo de una función.

Sin la directiva `"use strict"` todo sigue funcionando, pero algunas características se comportan de la manera antigua y “compatible”. Generalmente preferimos el comportamiento moderno.

Algunas características modernas del lenguaje (como las clases que estudiaremos en el futuro) activan el modo estricto implícitamente.

## Variables

Se pueden declarar usando:

-   `let`
-   `const` (constante, no se puede cambiar)
-   `var` (estilo antiguo, lo veremos más tarde)

Un nombre de variable puede incluir:

-   Letras y dígitos, pero el primer carácter no puede ser un dígito.
-   Los caracteres `$` y `_` son normales, al igual que las letras.
-   Los alfabetos y jeroglíficos no latinos también están permitidos, pero comúnmente no se usan.

Las variables se escriben dinámicamente. Pueden almacenar cualquier valor:
```javascript
let x = 5; 
x = "John";
```
Hay 8 tipos de datos:

-   `number` tanto para números de punto flotante como enteros,
-   `bigint` para números enteros de largo arbitrario,
-   `string` para textos,
-   `boolean` para valores lógicos: `true/false`,
-   `null` – un tipo con el valor único `null`, que significa “vacío” o “no existe”,
-   `undefined` – un tipo con el valor único `undefined`, que significa “no asignado”,
-   `object` y `symbol` – para estructuras de datos complejas e identificadores únicos, aún no los hemos aprendido.

El operador `typeof` devuelve el tipo de un valor, con dos excepciones:

```javascript
typeof null == "object" // error del lenguaje
typeof function(){} == "function" // las funciones son tratadas especialmente`
```

## Interacción

Estamos utilizando un navegador como entorno de trabajo, por lo que las funciones básicas de la interfaz de usuario serán:

`prompt(question, [default])`

Hace una pregunta `question`, y devuelve lo que ingresó el visitante o `null` si presiona “cancelar”.

`confirm(question)`

Hace una pregunta `question`, y sugiere elegir entre Aceptar y Cancelar. La elección se devuelve como booleano `true/false`.

`alert(message)`

Muestra un `message`.

Todas estas funciones son _modales_, pausan la ejecución del código y evitan que el visitante interactúe con la página hasta que responda.

Por ejemplo:

```javascript
let userName = prompt("¿Su nombre?", "Alice"); 
let isTeaWanted = confirm("¿Quiere té?");  

alert( "Visitante: " + userName ); // Alice 
alert( "Quiere té: " + isTeaWanted ); // true
```


## Operadores

JavaScript soporta los siguientes operadores:

<b>Aritméticos</b>

Los normales: `* + - /`, también `%` para los restos y `**` para aplicar potencia de un número.

El binario más `+` concatena textos. Si uno de los operandos es un texto, el otro también se convierte en texto:
```javascript
alert( '1' + 2 ); // '12', texto 
alert( 1 + '2' ); // '12', texto
```


<b>Asignaciones</b>

Existen las asignaciones simples: `a = b` y las combinadas `a *= 2`.

Operador bit a bit

Los operadores bit a bit funcionan con enteros de 32 bits al más bajo nivel.

<b>Condicional</b>

El único operador con 3 parámetros: `cond ? resultA : resultB`. Sí `cond` es verdadera, devuelve `resultA`, de lo contrario `resultB`.

<b>Operadores Lógicos</b>

Los operadores lógicos Y `&&` y Ó `||` realizan una evaluación de circuito corto y luego devuelven el valor donde se detuvo (no necesariamente true/false). El operador lógico NOT `!` convierte el operando a tipo booleano y devuelve el valor inverso.

<b>Operador “Nullish coalescing”</b>

El operador `??` brinda una forma de elegir el primer valor “definido” de una lista de variables. El resultado de `a ?? b` es `a` salvo que esta sea `null/undefined`, en cuyo caso será `b`.

<b>Comparaciones</b>

Para verificar la igualdad `==` de valores de diferentes tipos, estos se convierten a número (excepto `null` y `undefined` que son iguales entre sí y nada más), por lo que son iguales:
```javascript
alert( 0 == false ); // true alert( 0 == '' ); // true
```

Otras comparaciones también se convierten en un número.

El operador de igualdad estricta `===` no realiza la conversión: diferentes tipos siempre significan diferentes valores.

Los valores `null` y `undefined` son especiales: son iguales `==` el uno al otro y no son iguales a nada más.

Las comparaciones mayor/menor comparan las cadenas carácter por carácter, los demás tipos de datos se convierten a número.

<b>Otros operadores</b>

Hay algunos otros, como un operador de coma.


## Bucles

-   Cubrimos 3 tipos de bucles:
    ```javascript
    // 1 
    while (condition) {   
		... 
		}  
    // 2 
    do { 
      ... 
      } while (condition);  
    // 3 
    for(let i = 0; i < 10; i++) {
       ... 
       }
    ```
    
-   La variable declarada en el bucle `for(let...)` sólo es visible dentro del bucle. Pero también podemos omitir el `let` y reutilizar una variable existente.
    
-   Directivas `break/continue` permiten salir de todo el ciclo/iteración actual. Use etiquetas para romper bucles anidados.


Más adelante estudiaremos más tipos de bucles para tratar con objetos.

## La construcción “switch”

La construcción “switch” puede reemplazar múltiples revisiones con `if`. “switch” utiliza `===` (comparación estricta).
```javascript
let age = prompt('¿Su Edad?', 18);

switch (age) {   
	case 18:      

		alert("No funciona");// el resultado de la petición es un string, no un número    
	case "18":     

		alert("¡Funciona!");
		break;

	default:
		alert("Todo valor que no sea igual a uno de arriba"); 
}
```



## Funciones

Cubrimos tres formas de crear una función en JavaScript:

1.  Declaración de función: la función en el flujo del código principal
    ```javascript
    function sum(a, b) {
       let result = a + b;
       
	    return result;
    }
    ```
    
2.  Expresión de función: la función en el contexto de una expresión
    ```javascript
    let sum = function(a, b) {   
	    let result = a + b;    
	    
	    return result;
	};
    ```
    
3.  Funciones de flecha:
    ```javascript
    // la expresión en el lado derecho 
    let sum = (a, b) => a + b;  
    
    // o sintaxis multilínea { ... }, aquí necesita return: 
    let sum = (a, b) => { 
      // ...  
     return a + b;
    } 
    
    // sin argumentos
     let sayHi = () => alert("Hello");
     
	// con un único argumento 
	let double = n => n * 2;
    ```
    

-   Las funciones pueden tener variables locales: son aquellas declaradas dentro de su cuerpo. Estas variables solo son visibles dentro de la función.
-   Los parámetros pueden tener valores predeterminados: `function sum(a = 1, b = 2) {...}`
-   Las funciones siempre devuelven algo. Si no hay `return`, entonces el resultado es `undefined`.

# La sentencia "switch"

Una sentencia `switch` puede reemplazar múltiples condiciones `if`.

Provee una mejor manera de comparar un valor con múltiples variantes.

## La sintaxis

`switch` tiene uno o mas bloques `case`y un opcional `default`.

Se ve de esta forma:
```javascript
switch(x) {   
	case 'valor1':  // if (x === 'valor1') 
	  ---
		[break] 
		   
	case 'valor2':  /* if (x === 'valor2')*/
	  ---    
		[break]   
		
	default:     
	  ---     
		[break] 
}
```

-   El valor de `x` es comparado contra el valor del primer `case` (en este caso, `valor1`), luego contra el segundo (`valor2`) y así sucesivamente, todo esto bajo una igualdad estricta.
-   Si la igualdad es encontrada, `switch` empieza a ejecutar el código iniciando por el primer `case`correspondiente, hasta el `break` más cercano (o hasta el final del `switch`).
-   Si no se cumple ningún caso entonces el código `default` es ejecutado (si existe).

## Ejemplo

Un ejemplo de `switch`:
```javascript
let a = 2 + 2;

switch (a) {
	case 3:
     alert( 'Muy pequeño' );
     break;
    case 4:     
	 alert( '¡Exacto!' );     
	 break;   
	case 5:     
	 alert( 'Muy grande' );     
	 break;   
	default:     
	 alert( "Desconozco estos valores" ); 
}
```

Aquí el `switch` inicia comparando `a` con la primera variante `case` que es `3`. La comparación falla.

Luego `4`. La comparación es exitosa, por tanto la ejecución empieza desde `case 4` hasta el `break` más cercano.

**Si no existe `break` entonces la ejecución continúa con el próximo `case` sin ninguna revisión.**

Un ejemplo sin `break`:

```javascript
let a = 2 + 2;  

switch (a) {  
	case 3:     
	 alert( 'Muy pequeño' );   
	case 4:     
	 alert( '¡Exacto!' );   
	case 5:     
	 alert( 'Muy grande' );   
	default:     
alert( "Desconozco estos valores" );
}
```


En el ejemplo anterior veremos ejecuciones de tres `alert` secuenciales:
```javascript
alert( '¡Exacto!' );
alert( 'Muy grande' );
alert( "Desconozco estos valores" );
```

Cualquier expresión puede ser un argumento `switch/case`

Ambos `switch` y `case` permiten expresiones arbitrarias.

Por ejemplo:

```javascript
let a = "1";
let b = 0;
switch (+a) {
	case b + 1:
	 alert("esto se ejecuta, porque +a es 1, exactamente igual b+1"); 
	 break;
	 
	default: 
	 alert("esto no se ejecuta"); }
```

Aquí `+a` da `1`, esto es comparado con `b + 1` en `case`, y el código correspondiente es ejecutado.

## Agrupamiento de “case”

Varias variantes de `case` los cuales comparten el mismo código pueden ser agrupadas.

Por ejemplo, si queremos que se ejecute el mismo código para `case 3` y `case 5`:
```javascript
let a = 2 + 2;  

switch (a) {   
	case 4:     
	 alert('¡Correcto!');     
break; 

	case 3:                    // (*) agrupando dos cases   
	case 5:     
	 alert('¡Incorrecto!');     
	 alert("¿Por qué no tomas una clase de matemáticas?");     
	 break;

	default:     
	 alert('El resultado es extraño. Realmente.'); }
```

Ahora ambos, `3` y `5`, muestran el mismo mensaje.

La capacidad de “agrupar” los `case` es un efecto secundario de cómo trabaja `switch/case` sin `break`. Aquí la ejecución de `case 3` inicia desde la línea `(*)` y continúa a través de `case 5`, porque no existe `break`.

## El tipo importa

Vamos a enfatizar que la comparación de igualdad es siempre estricta. Los valores deben ser del mismo tipo para coincidir.

Por ejemplo, consideremos el código:
```javascript
let arg = prompt("Ingrese un valor");
switch (arg) {
	case '0':   
	case '1':     
	 alert( 'Uno o cero' );     
	 break; 
	    
	case '2':     
	 alert( 'Dos' );     
	 break;
	     
	case 3:      
	 alert( '¡Nunca ejecuta!' );     
	 break;   
	default:     
	 alert( 'Un valor desconocido' ); }
```

1.  Para `0`, `1`, se ejecuta el primer `alert`.
2.  Para `2` se ejecuta el segundo `alert`.
3.  Pero para `3`, el resultado del `prompt` es un string `"3"`, el cual no es estrictamente igual `===` al número `3`. Por tanto ¡Tenemos un código muerto en `case 3`! La variante `default` se ejecutará.

## Ejercicios

### Reescribe el "switch" en un "if
Escribe el código utilizando `if..else` que corresponda al siguiente `switch`:
```javascript
switch (navegador) {
	case 'Edge':
	 alert( "¡Tienes Edge!" );
	 break; 

	case 'Chrome': 
	case 'Firefox': 
	case 'Safari': 
	case 'Opera': 
	 alert( 'Esta bien, soportamos estos navegadores también' ); 
	 break;

	default: 
alert( '¡Esperamos que esta página se vea bien!' );
}
```

<details><summary>Respuesta - ¡Haz Click!</summary>

Para que coincida con la funcionalidad de `switch` exactamente, el `if` debe utilizar una comparación estricta `'==='`.

Pero para strings, un simple `'=='` también funciona.
```javascript

if(navegador == 'Edge') {   alert("¡Tienes Edge!"); } else if (navegador == 'Chrome'  || navegador == 'Firefox'  || navegador == 'Safari'  || navegador == 'Opera') {   alert( 'Está bien, soportamos estos navegadores también' ); } else {   alert( '¡Esperamos que la página se vea bien!' ); }
```
Nota: la construcción `navegador == 'Chrome' || navegador == 'Firefox' …` fue separada en varias líneas para mejorar su lectura.

Pero la construcción `switch` sigue siendo más clara y descriptiva.

</details>


### Reescribe "if" en "switch
Reescribe el código debajo utilizando solo un argumento `switch`:

```javascript
let a = +prompt('a?', '');

if (a == 0) { 
	alert( 0 );
} 

if (a == 1) {
	alert( 1 );
} 

if (a == 2 || a == 3) {
	alert( '2,3' );
}
```

<details><summary>Respuesta - ¡Haz Click!</summary>

Las primeras dos validaciones se vuelven dos `case`. La tercera validación se separa en dos `case`:

```javascript
let a = +prompt('a?', '');

switch (a) {
	case 0: 
	 alert( 0 );
	 break;

	case 1: 
	 alert( 1 ); 
	 break;

	case 2:
	case 3:
	 alert( '2,3' );
	 break;
}
```

Nota: El `break` al final no es requerido. Pero lo agregamos por previsión, para preparar el código para el futuro.

Existe una probabilidad de que en el futuro queramos agregar un `case` adicional, por ejemplo `case 4`. Y si olvidamos agregar un break antes, al final de `case 3`, habrá un error. Por tanto, es una forma de auto-asegurarse.

</details>

