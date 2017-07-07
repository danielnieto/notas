# Componentes

Se extienden de la clase React.Component

```javascript

class MiClase extends React.component{
	
	render(){
		return <h1>MiClase</h1>
	}

}

// corresponde al componente <MiClase />

```

Si se necesita usar "this" dentro de un event handler, se tiene que "bindear" el `this` a la funcion en el constructor:

```javascript
  constructor(props){
    super(props);
    this.handleClick = this.handleClick.bind(this);
  }
  
  handleClick(){
	//aqui se puede usar el "this"
  }
  
  render(){
  	return <button onClick={this.handleClick}>Click me</button>
  }
```

## Props
Son propiedades que un componente obtiene de los atributos del elemento JSX, por ejemplo

`<MiComponente nombre="daniel" />`

```javascript
class MiClase extends React.component{
	
	render(){
		//se pueden acceder a los props, por medio de this.props
		return <h1>{this.props.nombre}</h1>
	}

}

```
**Un `prop` NO debe cambiarse desde el componente, solo componentes externos deben cambiar su valor** 
#####ESTO NO SE DEBE HACER
```javascript
import React from 'react';

class Bad extends React.Component {
  render() {
    this.props.message = 'yo'; // NOOOOOOOOOOOOOO!!!
    return <h1>{this.props.message}</h1>;
  }
}
```

### Props por defecto

Se pueden asignar `prop`s por defecto, si es que no se provee un valor en el tag, usando el siguiente ejemplo

`<MiComponente nombre="daniel" />`

```javascript
class MiClase extends React.component{
	
	render(){
		//se espera el valopr de nombre
		return <h1>{this.props.nombre}</h1>
	}

}

```

Si `nombre` no se provee, se puede asignar por default de la siguiente manera:

`MiClase.defaultProps = {nombre: 'nombre por defecto'}`

Esta linea de codigo hace referencia a la clase en si, de manera estatica, por lo que debe existir AFUERA de la clase.

### PropTypes

Se pueden especificar los "tipos" de los props, para seguridad en su uso y para documentarse.

La manera de especificar los propTypes es por medio de un miembro estatico de la clase:

```javascript
	
	class MiClase extends React.Component{
		render() {
			return <h1>{this.props.mensaje}</h1>;
		}
	}
	
	MiClase.propTypes = {
		mensaje: React.PropTypes.string
	}

```

Los tipos que se pueden usar:

```javacript
Runner.propTypes = {
  message:   React.PropTypes.string.isRequired,
  style:     React.PropTypes.object.isRequired,
  isMetric:  React.PropTypes.bool.isRequired,
  miles:     React.PropTypes.number.isRequired,
  milesToKM: React.PropTypes.func.isRequired,
  races:     React.PropTypes.array.isRequired
};
```
Si se usa `.isRequired` al final del propType, esto le indica a React que ese `prop` DEBE ser provista.

- NUNCA cambiar el valor de props

## States
Los `states` son valores que se generan dentro del componente (a diferencia de los `props`) y pueden ser cambiantes, se definen en el constructor

```javascript
class Toggle extends React.Component {
  constructor(props){
    super(props);
    this.state = {color: 'green'}
  }
  
  render() {
    return (
      <div>
        Color is: {this.status.color}
      </div>
    );
  }
```
Los `states` se cambian usando la funcion `this.setState` y pasando un objeto con todas las nuevas propiedades que se van a "mergear" con el objeto `this.state` actual.

**NO se puede llamar `this.setState` dentro de la funcion `render`**

Ejemplo de uso de states:

```javascript
class Clicks extends React.Component {
  constructor(props){
    super(props);
    this.state = {clicks: 0}
    this.handleClick = this.handleClick.bind(this);
  }
  
  handleClick(){
  	this.setState({
		clicks: ++this.state.clicks  	
	})
  }
  
  render() {
    return (
      <div>
		Times clicked: {this.state.clicks}
        <button onClick={this.handleClick}>Click me</button>
      </div>
    );
  }
}
```

