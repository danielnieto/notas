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


