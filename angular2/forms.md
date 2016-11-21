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

##Usando FormBuilder

Para crear forms primero como esta en proceso de deprecacion la vieja API hay que agregar que inyectar en el bootstrap:
	
```
//aparte de las otras lineas de codigo en main.ts
import {disableDeprecatedForms, provideForms} from "@angular/forms";

bootstrap(App, [disableDeprecatedForms(), provideForms()])
```

Ahora, el componente debe importar los siguientes:
`
import {
  FORM_DIRECTIVES,
  REACTIVE_FORM_DIRECTIVES,
  FormBuilder,
  FormGroup,
  Validators,
  AbstractControl
} from '@angular/forms';
`

E inyectamos el formBuilder en el constructor:

`constructor(private fb: FormBuilder){`

Ya que tenemos referencia al FormBuilder podemos crear un formGroup con:

```
//myForm se define en el componente para poder usarlo desde cualquier parte
myForm: FormGroup;

//esto va en el constructor
this.myForm = fb.group({
            'sku':["defecto"]
        });
```

El HTML se ve asi:

```
<form [formGroup]="myForm">
    <input type="text" name="sku" ngModel>
```

De esta manera, Angular automaticamente asigna el form creado con el FormBuilder al html, y el input se bindea con el FormControl correcto, SOLO SI SE USA name y ngModel

Otra manera de hacer el binding manualmente es:

`<input type="text" [formControl]="myForm.controls['sku']">`

Para validar se ponen los validators en el formBuilder:

```
this.myForm = fb.group({
            'sku':["", Validators.required]
        });
```

Y para mas de un validador o un validador custom:

```
this.myForm = fb.group({
            'sku':["", Validators.compose([Validators.required, skuValidator])],
        });
```
        
Y este ejemplo es del validador de skuValidator:

```
function skuValidator(control: FormControl): { [s: string]: boolean } {
      if (!control.value.match(/^123/)) {
        return {invalidSku: true};
      }
    }
```  
 
Para poder verificar si un campo es valido se tiene que crear una variable desde la clase del componente:

```
//esto es abajo del formBuilder, en el constructor

this.sku = this.myForm.controls['sku'];
```

Y despues se puede verificar asi:

`<div *ngIf="sku.hasError('required')">`

