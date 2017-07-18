# React QuickTips

## Parametrizar Handlers

Para mandar parametros a un handler por ejemplo de click, se envuelve el handler con otra funcion:

```javacript
	
	<div onClick={(e)=>{this.handler('parametro')}} > 
```

O se puede enlazar el handler con el parametro

```javacript
	
	<div onClick={this.handler.bind(this,'parametro')} > 
```

O se se usa un `data-`:


```html
	
	<div data-parametro='el valor del parametro' onClick={this.handler} > 
	
```
y luego

```javascript
handler(e){
	var parametro = e.currentTarget.dataset.parametro;
}
```

## Acceder a hijos de un componente

Para acceder a los hijos de un componente se hace por medio de `props.children`, si es un solo "hijo" entonces `props.children` lo contendra, si hay varios hijos, entonces `props.children` se convierte en un array.

```html
	<Componente>
		<Hijo />
	</Componente>
```

para acceder al hijo: 

```javascript
	//contiene <Hijo />
	this.props.children 
```	

Y para cuando son varios hijos

```html
	<Componente>
		<Hijo1 />
		<Hijo2 />
	</Componente>
```

para acceder a los hijos:

```javascript
	//contiene <Hijo1 />
	this.props.children[0]
	//contiene <Hijo2 />
	this.props.children[1]

```	


