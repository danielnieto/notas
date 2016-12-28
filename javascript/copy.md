#Copiar un arreglo

Para copiar un arreglo se pueden usar los siguientes metodos:

- `var copia = aCopiar.slice();`
- `var copia = [].concat(aCopiar)`
- `var copia = [...aCopiar]` (usa spread operator de ES6)
- `var copia =  Array.from(aCopiar);` (tambien usa Array.from de ES6)

## Para copiar un objeto

Se usa:

`Object.assign({}, aCopiar)`

opcionalmente se puede pasar un tercer parametro con los valores sobreescritos (como en valores default).

Sin embargo, esta tecnica solo copia objetos con 1 nivel de profundidad:, por lo tanto **NO** copiara lo siguiente:

```
const dan = {
		name: "Daniel",
		age: 27,
		social: {
			twitter: "@danielnieto89",
			facebook: "@danielnieto89"
		}
	}
```

