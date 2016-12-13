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

Los binding `enable` y `disable` pueden habilitar o desabilitar un input element:

`<input type="text" data-bind="enable: estaHabilitado">`

De igual manera, se puede usar el binding `hasFocus` para asignar (o desasignar) el foco a un elemento

`<input type="text" data-bind="hasFocus: tieneFoco">`

##Subscripcion

Te puede subscribir a un `observable` y cuando su valor cambia, se `notificara` a los subscriptores por medio de un callback:

```
	observable.subscribe(function(newValue){
		console.log(newValue);
	});

```

##Inputs

###Input text
Para hacer el binding a un input text simple solo necesitas usar el binding `value` este se actualiza cuando cambia el foco del input

`<input type="text" data-bind="value: propiedad">`

Con el binding `textInput` la actualizacion se hace inmediatamente despues de teclear una letra, o pegar un texto en el input, para elementos HTML input text simples, es recomendable usar este binding.

`<input type="text" data-bind="textInput: propiedad">`

###Select
El binding se hace indicando un arreglo de opciones, y el `observable` que contendra la opcion seleccionada

```
<select data-bind="options: ['uno', 'dos', 'tres'], value: opcionSeleccionada"></select>
```

se puede usar `optionsCaption` para mostrar el "titulo" del select (que no "valga" como opcion)

Para hacer el binding con un arreglo de objetos:

```
<select data-bind="options: arregloDeObjetos, optionsText: 'propiedadDelObjetoParaSerElTextoDeLaOpcion', optionsValue: 'propiedadDelObjetoParaSerElValorDeLaOpcion', value: observableQueTieneElValorSeleccionado"></select>
```

Para tener mayor control sobre las opciones a seleccionar o para obtener el objeto seleccionado (en lugar de solo un valor) se usa de la siguiente manera:


```
<select data-bind="options: arregloDeObjetos, optionsText: function(i){return i.stringDeLaOpcion}, value: opcionSeleccionada"></select>
```

Cabe resaltar que `optionsText` en este caso es una funcion que itera sobre el arreglo de elementos, y en este ejemplo tiene una funcion que toma el valor actual siendo iterado, y obtiene una propiedad que es la que se mostara dentro de `<option>`

###Multiselect 
Es muy similar al select normal, solo se debe hacer uso del `selectedOptions` binding

`<select multiple="multiple" data-bind="options: arrayDeOpciones, selectedOptions: observableArrayQueContendraLasOpciones"></select>`

###Checkbox

Se usa el binding `checked`:

`<input type="checkbox" data-bind="checked: estaSeleccionado">`