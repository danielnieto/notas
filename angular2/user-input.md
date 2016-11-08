#User Input

Se puede hacer referencia a un elemento del DOM con "Template Reference Variables", solo se debe poner un atributo precedido de # y con ese nombre se puede referenciar el elemento:

`<input #box (keyup)="manejador(box.value)">`
	
	Estas variables tambien pueden usarse para acceder a Directives dentro de un template, por ejemplo el ngModel de un input. Se hace asi:
	
`#referencia="ngModel"`


Para escuchar a una tecla en especifico se pueden utilizar pseudoeventos:

`<input #box (keyup.enter)="values=box.value">`

En ese ejemplo, solo se ejecuta el la asignacion si la tecla que se presiono fue Enter.