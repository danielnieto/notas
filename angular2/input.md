#Input

Para pasar datos de un componente padre a un hijo se hace por medio de Inputs.

El padre debe de pasar un un atributo al container del hijo con la propiedad:

`<inout-hijo [propiedad]="propiedadDelPadre">`

Y el hijo la recibe de dos maneras diferentes:

Usando el decorador Input:

`@Input() propiedad; //se debe importar el decorador de @angular/core`

O 

Se pueden listar los Inputs en un arreglo en los metadatos del componente hijo:

```
@Component({
		Selector….
		Template…
		Inputs:['propiedad']
	})
```
	
Si el padre usa [] significa que sera un binding (ese input con una variable del padre), el valor se actualizara cuando cambie la variable… si se quiere hacer un valor fijo solo se llama la propiedad sin []

`<inout-hijo propiedad="valor fijo string">`
	
Tambien, se puede llamar diferente la version publica del Input y la interna, por ejemplo, si quiero que la propiedad la acceda el padre como "propiedadHijo" y el hijo la reciba como "miPropiedad" se pasa el alias en el decorador como parametro o despues de dos puntos (:) en el arreglo de inputs

`inputs: ["nombreInterno:aliasPublico"]`

Y

`@Input('aliasPublico') nombreInterno:tipo;`
	

Otra manera de acceder a un atributo estatico desde el hijo, en lugar de usarlo como input se utiliza el decorador @Attribute en el constructor(fuera no sirve) de esta manera:

`constructor(@Attribute('atributo') atributo:string)`

Pero de esta manera solo puedes acceder al valor en el constructor, y aqui es donde tienes que asignarlo a otra variable para usarlo en otras partes. __(De preferencia usar Input???)__