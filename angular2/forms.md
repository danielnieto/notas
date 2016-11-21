#Forms

Para crear forms primero como esta en proceso de deprecacion la vieja API hay que agregar que inyectar en el bootstrap:
	
```
//aparte de las otras lineas de codigo en main.ts
	import {disableDeprecatedForms, provideForms} from "@angular/forms";

	bootstrap(App, [disableDeprecatedForms(), provideForms()])
	
```
	
Ahora, el componente que sera el form, debe agregar:

`import {NgForm} from "@angular/forms"`
	
	
Para usar [(ngModel)] con forms es necesario poner un "name" a los inputs.

Para saber si un input es valido o no, o es pristino, se hace por medio del ngModel, y para poder acceder al ngModel de un elemento, se usa:

`<input … #referencia="ngModel">`

Y luego se puede usar:
```
	//se oculta si es valido o es prsitino
	<div [hidden]="referencia.valid || referencia.pristine">
```
	
De igual manera, se puede saber si un form es valido o no, haciendo referencia al form:

`<form (ngSubmit)="onSubmit()" #referenciaAlForm="ngForm">`
	
Y se puede hacer el binding para habilitar/deshabilitar un boton para hacer el submit:

`
<button type="submit" [disabled]="!referenciaAlForm.form.valid">Submit</button>
`

Cuando se hace el submit, puedes acceder al modelo tal cual que se definio con el two-way data binding.
