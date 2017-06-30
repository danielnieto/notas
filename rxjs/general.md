# RxJS

## Generalidades

### Observable

Se crea por medio Rx.Observable.create() y toma 1 funcion como parametro, que es la que se va a ejecutar cuando alguien se suscriba al Observable.

Por ejemplo, emite un 'hi' cada segundo: 

```javascript

	var observable = Rx.Observable.create(function subscribe(observer) {
	  var id = setInterval(() => {
	    observer.next('hi')
	  }, 1000);
});

```

Cada "subscriptor" obtiene una "instancia" nueva del Observable, o sea, al subscribirse se ejecuta la funcion "subscribe", de tal forma que los subscriptores **NO** comparten el observable.

### Cancelar Subscripcion

La subscripcion se puede cancel al llamar al metodo `unsubscribe` de la subscripcion

```javascript

var observable = Rx.Observable.from([10, 20, 30]);
var subscription = observable.subscribe(x => console.log(x));
...
subscription.unsubscribe();

```

Se puede personalizar el comportamiento de la 'desubscripcion' regresando una funcion al momento de crear el Observable, por ejemplo, para cancelar timers, o liberar variables o recursos, se hace de la siguiente manera

```javascript

var observable = Rx.Observable.create(function subscribe(observer) {
  // Keep track of the interval resource
  var intervalID = setInterval(() => {
    observer.next('hi');
  }, 1000);

  // Provide a way of canceling and disposing the interval resource
  return function unsubscribe() {
    clearInterval(intervalID);
  };
});


```

### Observer
Un objeto `observer` es el consumidor de los "valores" emitidos por un `Observable`. Son simplemente un set de callbacks, uno por cada tipo de notificacion (`next`,`error`, `complete`) que manda el Observable. Ejemplo de un Objeto Observer

```javascript

var observer = {
  next: x => console.log('Observer got a next value: ' + x),
  error: err => console.error('Observer got an error: ' + err),
  complete: () => console.log('Observer got a complete notification'),
};

```

Para usar el `Observer` se pasa a la funcion de subscribe

```
observable.subscribe(observer);
```

Si no se usa un objeto `Observer` para la funcion `subscribe`, esta lo crea automaticamente tomando los parametros de la funcion como los valores del objeto.

```
observable.subscribe(
	x => console.log('Observer got a next value: ' + x),
	err => console.error('Observer got an error: ' + err),	() => console.log('Observer got a complete notification')
);
```

## Metodos

### subscribe 

Tiene 3 parametros, 
- onValue: la funcion que se se ejecuta con cada nuevo valor
- onError: la funcion que se ejecuta cuando hay un error en el stream
- onFinish: la funcion que se ejecuta cuando el stream termina

```
	stream.subscribe(onValue, onError, onFinish)
```

### take
Toma solo los primeros 'n' valores de un stream.

```
stream.take(n)
```

### skip
Salta los primeros 'n' valores de un stream.

```
stream.skip(n)
```

### interval

Emite un valor cada determinado tiempo

```
Rx.Observable.interval(n)
``` 

### map
Realiza acciones sobre cada valor del stream

```
//multiplica cada valor del stream por 10
stream.map(val => val*10)
```

### concat
Concatena dos streams en uno solo, espera a que termine el primer stream y adjunta el segundo al final.

```
streamA.concat(streamB)
```

### merge
Combina dos stream en uno solo

```
streamA.merge(streamB)
```

### combineLatest
Combina los ultimos valores de dos streams

```
// suma los ultimos valores de dos streams
Rx.Observable.combineLatest(streamA, streamB, (a,b) => a + b)
```

### do
No hace nada sobre el valor, pero permite ejecutar codigo con el valor, por ejemplo, imprimirlo

```
stream.do(val => console.log(val))
```