- Para hacer binding de una propiedad del DOM con una propiedad de TS se usa `[]` como
`<img [src]="propiedadTS" />`

Se puede usar con cualquier propiedad, como hidden

- Para agregar una clase condicionalmente se usa:
`<div [class.laClaseCondicional]="propiedadTS" >`

- Hacer el binding de eventos se usa `()` 
`<button (click)="funcionHandler($event)" >`
`$event` es de Angular

- El two-way binding es solo para propiedades, no puedes hacerlo con funciones o nada mas que propiedades
`<input [(ngModel)]="propiedad" >`

- Para crear un service se necesita:
	- Ponerle el decorador `@Injectable`
	- Registrarlo con el Injector por medio de `"Providers"`
	- Inyectar la dependencia en el constructor de quien lo usara
