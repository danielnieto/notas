# Stateless Functional Components

Cuando un componente no tiene NADA mas que una funcion `render` (cuando es un componente "presentational", ese componente se puede escribir de otra manera, mas concisa, ejemplo:


```javascript
class MiClase extends React.Component{
	
	render(){
		return <h1>{this.props.saludo}</h1>
	
	}

}
```

Se convierte a

```javascript

const MiClase = (props) => {
	return <h1>{props.saludo}</h1>
}

```

Para definir los propTypes

```javascript
	MiClase.propTypes = {
		saludo: React.PropTypes.string.isRequired
	}
```