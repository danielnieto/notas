#Componentes de Oracle JET


JET utiliza un `custom binding` de knockout para hacer referencia y usar modulos dentro de la aplicacion, por ejemplo un modulo puede ser un header, o una lista de nombres, o cualquier cosa que sea html.

Para utilizar un modulo se usa el binding `ojModule` por ejemplo:

```html
<header data-bind="ojModule: {name: 'header'}"></header>
```

`ojModule` puede usarse de 3 maneras,

1. Para cargar un `view` y `viewModel`, por ejemplo, si se pasa el parametro `name: 'mi-componente'` el binding cargara una vista localizada en `js/views/mi-componente.html` y el `viewModel` correspondiente localizado en `js/viewModels/mi-componente.js` y aplicara los bindings.

```html
<header data-bind="ojModule: {name: 'mi-componente'}"></header>
```

2. Si solo se require carga un `view`, se utiliza el parametro `viewName: 'mi-componente'` esto solo cargara la vista localizada en `js/views/mi-componente.html`.

```html
<header data-bind="ojModule: {viewName: 'mi-componente'}"></header>
```

3. Utilizando el `Router` de JET, para cargar el modulo cuando sea necesario.

```html
<div data-bind="ojModule: router.moduleConfig">
```


