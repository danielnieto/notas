# JSX

- Es una version "extendida" de Javascript, que te permite mezclar HTML y Javascript

- Un elemento JSX se ve como HTML

```javascript
	var myElement = <div>This is a JSX element</div>
```

- Para usar "multilinea" se usan `(` y `)` 

```javascript
var myDiv = (
	<div>
		<h1>Hola</h1>
		<p>
			Este es un parrafo
		</p>
	</div>
)

```


- Cada elemento JSX tiene que tener un tag "outermost" o sea, debe haber un elemento que englobe todo:

```javascript
var myDiv = (
	<div>
		<h1>Hola</h1>
		<p>
			Este es un parrafo
		</p>
	</div>
)

```

- No se puede usar `class` para los elementos JSX en su lugar, se usa 
`className`

```javascript
	var myElement = <div className="mi-clase">This is a JSX element</div>
```

- Para "inyectar" Javascript en JSX se usan las llaves `{` y `}`, la expresion que esté dentro de ellas, se evaluará.

```javascript
	var myElement = (
		<div>
			2 + 3 = {2+3}
		</div>
	)
```


- Los nombres de los atributos para eventos en elementos JSX son camelCase, por ejemplo: HTML `onclick`, seria `onClick` en JSX

```javascript
	var myElement = <button onClick={doSomething}>Click me</button>
```
