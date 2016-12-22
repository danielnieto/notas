# Templates

El binding `template` popula el elemento DOM asociado con el resultado de la renderizado de un template. 

Para usar un template:

Primero debes describir la estructura del template, esto puede ser dentro de un script (de tipo texto `type="text/html"`) y tiene que existir en el documento **ANTES** de que se aplique el binding:

```
<script type="text/html" id="nombreDeLaPlantilla">
	<!--Aqui va todo el codigo HTML de la plantilla-->
	<span data-bind="text: valorDePlantilla"></span>
</script>

```


Tambien se puede usar `<template>` en mi opinion esta opcion es mas logica, y correcta: 

```
<template id="nombreDeLaPlantilla">
	<!--Aqui va todo el codigo HTML de la plantilla-->
	<span data-bind="text: valorDePlantilla"></span>
</template>

```

Para usar el template, solo se debe hacer uso del binding `template`

```
<div data-bind="template: {name:'nombreDeLaPlantilla'}">
</div>
```

o se puede usar sin contenedor

```
<!-- ko template: {name: 'nombreDeLaPlantilla', data: $data, as: 'contextoDeLaPlantilla'}-->
<!-- /ko -->
```

###Parametros (algunos)

- `name`: es el ID de la plantilla, puede ser un `<script>` o un `<template>` o cualquier elemento HTML.

- `data`: el contexto que se pasara a la plantilla, y que sera el contexto de la plantilla, por defecto es `{data: $data}`

- `as`: el alias por el que se hara referencia a este contexto, en caso de que haya mas que puedan colisionar (que no se pueda usar `$data` en templates internas
