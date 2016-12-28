#Array Functions

##Filter

Filter itera por todo el arreglo y regresa otro arreglo con los items que "pasaron" el filtro, el filtro es un "callback" y para "pasar" se tiene que regresar un valor `truthy`

```
    var inventors = [
      { first: 'Albert', last: 'Einstein', year: 1879, passed: 1955 },
      { first: 'Isaac', last: 'Newton', year: 1643, passed: 1727 },
      { first: 'Galileo', last: 'Galilei', year: 1564, passed: 1642 },
      { first: 'Marie', last: 'Curie', year: 1867, passed: 1934 },
      { first: 'Johannes', last: 'Kepler', year: 1571, passed: 1630 },
      { first: 'Nicolaus', last: 'Copernicus', year: 1473, passed: 1543 },
      { first: 'Max', last: 'Planck', year: 1858, passed: 1947 }
    ];
    
    //bornIn1500s es un nuevo arreglo que contiene solo los objetos que cumplieron con la regla (nacio en 1500's)

var bornIn1500s = inventors.filter(inventor => inventor.year >= 1500 && inventor.year < 1600);

```

##Map
Map regresa un arreglo del mismo tamano que el array original, cada item del arreglo se pasa a una funcion "callback" y esta funcion "procesa" el item en cada iteracion y agrega el resultado de dicho procesamiento al nuevo array:

```
	var inventors = [
      { first: 'Albert', last: 'Einstein', year: 1879, passed: 1955 },
      { first: 'Isaac', last: 'Newton', year: 1643, passed: 1727 },
      { first: 'Galileo', last: 'Galilei', year: 1564, passed: 1642 },
      { first: 'Marie', last: 'Curie', year: 1867, passed: 1934 },
      { first: 'Johannes', last: 'Kepler', year: 1571, passed: 1630 },
      { first: 'Nicolaus', last: 'Copernicus', year: 1473, passed: 1543 },
      { first: 'Max', last: 'Planck', year: 1858, passed: 1947 }
    ];
    
	// firstAndLast es un nuevo arreglo solo con la propiedad first y last de cada item
	
	var firstAndLast = inventors.map(inventor => inventor.first + " " + inventor.last);
```

##Reduce

`Reduce` reduce un array a un solo valor, este valor se va pasando entre iteraciones, se puede utilizar para acumulaciones:

```

var sum = [1, 2, 3].reduce(
  function(total, num){ return total + num }
  , 0);
  
```

> Nota: reduce toma 2 parametros, callback y valor inicial de la variable que se pasara entre iteraciones, el primer parametro del callback es la variable que se pasara entre iteraciones, el segundo parametro del callback es el item iterado


## Sort

Sort regresa un arreglo ordenado, el criterio de ordenacion lo dicta una funcion "callback"

```
	
	const inventors = [
      { first: 'Albert', last: 'Einstein', year: 1879, passed: 1955 },
      { first: 'Isaac', last: 'Newton', year: 1643, passed: 1727 },
      { first: 'Galileo', last: 'Galilei', year: 1564, passed: 1642 },
      { first: 'Marie', last: 'Curie', year: 1867, passed: 1934 },
      { first: 'Johannes', last: 'Kepler', year: 1571, passed: 1630 },
      { first: 'Nicolaus', last: 'Copernicus', year: 1473, passed: 1543 },
      { first: 'Max', last: 'Planck', year: 1858, passed: 1947 }
    ];
	
	//ordena el arreglo por anyo de nacimiento, de mayor a menor
	
	var ordered = inventors.sort((a,b) => a.year < b.year ? 1: -1);

```

Si el "primer" elemento (`a`) es menor que el segundo (`b`) (los parametros de la funcion de ordenamiento `a` y `b`) la funcion de ordenamiento debera regresar `-1`

En cambio si el "primer" elemento (`a`) es mayor que el "segundo" (`b`), la funcion debera regresar `1`

Si son iguales la funcion debera regresar `0`

## Some

Regresa `true` si al menos 1 elemento del arreglo cumple con la condicion, la condicion es un "callback":

```
//si alguna persona es mayor de 18 años
var algunAdulto = personas.some(persona => new Date().getFullYear() - persona.ano >= 18);

```

## Every

Muy similar a `some`. Regresa `true` si TODOS los elementos cumplen con la condicion.

```
//si alguna persona es mayor de 18 años
var todosAdultos = personas.every(persona => new Date().getFullYear() - persona.ano >= 18);

```

## Find

Regresa el primer elemento que cumple con la condicion, la condicion es un "callback":

```
	var comentario = comentarios.find(comentario => comentario.id === 823423); 
```

## FindIndex

Regresa la posicion dentro del arreglo del primer elemento que cumpla con la condicion:

```
	var indice = comentarios.findIndex(comentario => comentario.id === 823423); 
```

