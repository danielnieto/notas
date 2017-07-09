# Styling

## Inline style

Se pueden pasar "object literals" al atributo `style` de los elementos JSX:

`<h1 style={{background: 'lightblue'}}>`

Se usan doble llaves por que se usan unas llaves para inyectar javascript en JSX y las otras son parte del objeto en si.

Se pueden crear objetos de estilos y pasarlos al atributo `style` tambien:

```javascript
const styles = {
  background: 'lightblue',
  color:      'darkred'
}

const styleMe = <h1 style={styles}>Estilizame</h1>;
```

En Javascript regular los nombres son en minusulas y con guiones:

```javascript
const styles = {
  'margin-top':       "20px",
  'background-color': "green"
};
```

En cambio, en React. los nombres son en camelCase

```javascript
const styles = {
  marginTop:       "20px",
  backgroundColor: "green"
};
```
React asume que los valores numericos son en "px" (en la mayoria de los casos)

```javascript
const styles = {
  background: 'lightblue',
  color:      'darkred',
  marginTop: 100,
  fontSize: 50
}
```