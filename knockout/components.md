#Componentes Knockout

##Definir un componente
Para crear un componente se debe registrar de la siguiente manera:

Se llama la funcion `ko.components.register` con dos parametros, el primero es el nombre del componente, y el segundo es un objeto que define el `viewModel` del componente y el `template` que usara:

```javascript 
ko.components.register("mi-componente", 
{viewModel: MiComponenteViewModel,
template: "HTML de mi componente"}
```
En su forma mas sencilla un componente puede ser:

```javascript 
ko.components.register("mi-componente", 
{viewModel: {},
template: "HTML de mi componente"}
```

El `view model` es solo un objeto, en este caso vacio, sin embargo, normalmente todas las propiedades del VM se aplicaran al `template`:

```javascript 

function MiComponenteViewModel(parametros){
	this.valorParametrizado = parametros.valorParametrizado;
	this.tituloDeMiComponente = "Este es mi componente";
}

ko.components.register("mi-componente", 
{viewModel: MiComponenteViewModel,
template: "<h1 data-bind='tituloDeMiComponente'></h1>"}
```

Idealmente, si se usa un module loader como `requirejs`, se puede cargar el template desde un archivo externo (recomendable)

Es importante mencionar que cada vez que un componente se "usa" se crea una nueva instancia del `ViewModel` por eso se debe hacer en forma de funcion (o clase).

##Usar un componente

Se utiliza el binding `component`

```html
<div data-bind="component: 'nombreDelComponente'"></div>
```

o se puede usar como un custom element: 

```html
<nombredelcomponente></nombredelcomponente>
```
Con esto Knockout automaticamente instanciará un nuevo `ViewModel` del componente y clonará el DOM necesario del `template` y aplicara los bindings.

Si se desean pasar parametros al componente es necesario especificar un objeto de configuracion al binding:

```html
<div data-bind="component: {name: 'nombreDelComponente', params: {paramUno: 'un parametro', paramDos: 'otro parametro'}"></div>
```
ó con custom element:

```html
<nombredelcomponente params="paramUno: 'un parametro', paramDos: 'otro parametro'"></nombredelcomponente>
```
