#Data Bindings
##Texto
Para texto simple:

`data-bind="text: propiedad"`

##Iteracion
Para iterar sobre un arreglo y mostrar un elemento por cada item del array

```
	<ul data-bind="foreach: arreglo">
		<!-- propiedadDelItem deberia ser algo que sea accesible de la forma arreglo[i].propiedadDelItem -->
		<li data-bind="text: propiedadDelItem"></li>
	</ul>
```

Para usar el contenido de un arreglo como en `arreglo = ['uno', 'dos', 'tres']` utiliza `$data` en el binding de los objetos iterados:

```
	<ul data-bind="foreach: arreglo">
		<!-- $data contiene arreglo[i] -->
		<li data-bind="text: $data"></li>
	</ul>
```

##Estilos

Puedes asignar estilos en linea basados en una condicion

`<tr data-bind="style:{'font-weight': condicion === true ? 'bold' : 'normal'}">`

Para poner o quitar una clase

`<div data-bind="css:{'clase-css': condicion === true}">`

##Atributos

Para asignar un atributo como `title` puedes usar 

`<td data-bind="attr:{title: someProperty}"></td>`

Tambien se puede usar para asignar el `href` de un `<a>`

##Subscripcion

Te puede subscribir a un `observable` y cuando su valor cambia, se `notificara` a los subscriptores por medio de un callback:

```
	observable.subscribe(function(newValue){
		console.log(newValue);
	});

```