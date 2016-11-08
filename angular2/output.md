#Output

Es similar a como funciona Input… pero cada salida depende de un evento que se emite desde el hijo hacia el padre.
Primero se tiene que importar el decorador Output y EventEmitter de @angular/core y se decora una instancia nueva de EventEmitter que sera el evento que se disparara al exterior:
	
`@Output("nombrePublico") evento = new EventEmitter();`

(el nombre publico es opcional)

Y el padre debe suscribirse a este evento:

`<hijo (eventoDelHijo)="manejarEsteEventoEnPadre($event)">`

Y el hijo puede en cualquier momento lanzar el evento:

`this.evento.emit({propiedad1:"valor"});`

Al hacer esto, el padre que esta suscrito a este evento recibira los datos enviados por meddio de $event.propiedad1

Al igual que con @Input, en lugar de usar decoradores se puede utilizar el array outputs en el decorador del componente hijo

```
@Component({
	Selector: …..
	Template:….
	Outputs:['evento:nombrePublico']
})
```

Y en la clase solo se instancia una propiedad (publica?) 

```
export class Hijo{
	public evento = new EventEmitter(); 
```