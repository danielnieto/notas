KnockoutJS es MVVM (Model View ViewModel)

- Model: Los datos guardados de la aplicacion. Estos datos representan objetos y operaciones en el dominio del negocio (por ejemplo cuentas de banco que pueden transferir dinero) y son independientes de cualquier UI. Cuando se usa Knockout, normalmente se hacen llamadas Ajax a algun servidor para leer y escribir los datos del modelo guardado.

- ViewModel: representacion de los datos y operaciones en la UI. Por ejemplo, si estas implementando un editor de lista, tu `view model` seria un objeto que contiene toda la lista de elementos y expone los metodos para agregar o quitar items.
	
	>Nota que `view model` no es la UI por si misma: no tiene ningun concepton de botones o de estilos. Tampoco es el modelo de datos persistente, si no que mantiene los datos "sin guardar" (en el servidor) con los que el usuario esta trabajando. Cuando se usa KO, tus `view model`s son objetos Javascript que no tienen conocimiento alguno de HTML. Manteniendo el `view model` abstracto de esta manera permite que sea simple, asi que puedes implementar comportamientos mas complejos sin perderte.

- View: visible e interactiva UI representando el estado de `view model`. Muestra informacion del `view model`, manda comandos al `view model` (por ejemplo, cuando el usuario hace clickea botones), y se actualiza cuando el estado del `view model` cambia.

Cuando usas KO, tu `view` es simplemente un documento HTML con bindings declarativos para enlazarlo con el `view model`. Alternativamente, puedes usar templates que generan HTML usando datos de tu `view model`

Para crear un `view model`, solo tienes que declarar cualquier objeto Javascript. Por ejemplo:


```
var myViewModel = {
    personName: 'Bob',
    personAge: 123
};
```

Y en el `view` tienes el siguiente html

```
The name is <span data-bind="text: personName"></span>
```
para "activar" el binding de KO, tienes que llamar la funcion applyBindings:

`ko.applyBindings(myViewModel);`

>este codigo debe llamarse despues de que el DOM se ha cargado, o sea, incluir el script al final del body o usar "onready"

Para incluir Knockout solo se necesita hacer referencia al script desde el archivo html (normalmente el index.html):

`<script src="http://cdnjs.cloudflare.com/ajax/libs/knockout/3.3.0/knockout-min.js"></script>`