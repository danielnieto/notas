# RxJS

## Definiciones

- **Observable**: representa la idea de valores invocables futuros o eventos
- **Observer**: es una coleccion de callbacks que saben como "escuchar' valores entregados por el `Observable`
- **Subscription**: representa la ejecucion de un `Observable`, primordialmente se usa para cancelar su ejecucion
- **Operators**: son funciones puras que permiten un estilo de programacion funcional para manejar colecciones como `map`, `filter`, `concat`, `flatMap`, etc.
- **Subject**: es el equivalente a un `EventEmitter`, y la unica manera de enviar valores a multiples `Observers`
- **Schedulers**: son despachadores centralizados de control de concurrencia, que permiten coordinar cuando ocurre la "computacion", por ejemplo `setTimeout` o `requestAnimationFrame`.


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

### Subscription

Es un objeto que representa un recurso "desechable", como la ejecucion de un observable. Una subscripcion tiene un metodo importante `unsubscribe` que no tiene argumentos y solamente desecha los recursos de la subscripcion. 

```javascript

var observable = Rx.Observable.interval(1000);
var subscription = observable.subscribe(x => console.log(x));
// Later:
// This cancels the ongoing Observable execution which
// was started by calling subscribe with an Observer.
subscription.unsubscribe();

```
Se puede hacer que al cancelar una subscripcion, se cancelen mas automaticamente, "agregando" subscripciones "hijas" a otras, ejemplo:

```javascript

var observable1 = Rx.Observable.interval(400);
var observable2 = Rx.Observable.interval(300);

var subscription = observable1.subscribe(x => console.log('first: ' + x));
var childSubscription = observable2.subscribe(x => console.log('second: ' + x));

subscription.add(childSubscription);

setTimeout(() => {
  // Unsubscribes BOTH subscription and childSubscription
  subscription.unsubscribe();
}, 1000);

```

Para eliminar una subscripcion "hija" se usa `subscription.remove(otherSubscription)`

### Subject

Un `Subject` es un tipo especial de `observable` que permite valores ser enviados a muchos `Observers`, mientras que un `observable` normal son unicast (o sea que cada Observer suscrito es dueño de una ejecucion independiente del observable).

__Todo `Subject` es un `Observable`__, se puede subscribir con un `Observer` y este comenzara a recibir los valores normalmente, no hay forma de saber desde el punto de vista del Observer, si los valores provienen de un subject, o de un observable "normal".

__Todo `Subject` es un `Observer`__, por lo tanto tiene los metodos `next`, `error` y `complete`, se puede usar el metodo `.next` para emitir un valor a todos los observers subscritos.

```javascript

	var subject = new Rx.Subject();

	subject.subscribe({
	  next: (v) => console.log('observerA: ' + v)
	});
	subject.subscribe({
	  next: (v) => console.log('observerB: ' + v)
	});
	
	subject.next(1);
	subject.next(2);

```

imprime

```
observerA: 1
observerB: 1
observerA: 2
observerB: 2

```

Se puede usar un `subject` para poder hacer broadcasting de un `observable` de la siguiente manera

```javascript

var subject = new Rx.Subject();

subject.subscribe({
  next: (v) => console.log('observerA: ' + v)
});
subject.subscribe({
  next: (v) => console.log('observerB: ' + v)
});

var observable = Rx.Observable.from([1, 2, 3]);

observable.subscribe(subject); // You can subscribe providing a Subject

```

y tiene el siguiente resultado

```
observerA: 1
observerB: 1
observerA: 2
observerB: 2
observerA: 3
observerB: 3

```

### Multicasted Observables

Los `observables "multicasted"` pasan las notificaciones por un `subject` que puede tener muchos suscriptores, a diferencia de los `observables "unicast"` que solo envian notificaciones a un solo `observer`

Un `observable "multicasted"` usa un `subject` internamente para hacer que varios `observers` compartan la misma ejecucion del `observable`

Internamente, de esta manera es como el operador `multicast` funciona: los `observers` se suscriben al `subject` interno, y ese `subject` se suscribe al `observable` fuente.

```javascript

var source = Rx.Observable.from([1, 2, 3]);
var subject = new Rx.Subject();
var multicasted = source.multicast(subject);
	
// These are, under the hood, `subject.subscribe({...})`:
multicasted.subscribe({
  next: (v) => console.log('observerA: ' + v)
});
multicasted.subscribe({
  next: (v) => console.log('observerB: ' + v)
});
	
// This is, under the hood, `source.subscribe(subject)`:
multicasted.connect();

```

El metodo `connect()` del objeto `multicasted` ejecuta el `observable` y regresa una subscripcion

### Conteo de Referencias

Para evitar llamar `connect()` y manejar la subscripcion manualmente, podemos usar el metodo `refCount()`, el cual regresa un `observable` que mantiene cuantos suscriptores tiene, cuando el numero de suscriptores incrementa de 0 a 1, llama el metodo `connect()`, que inicia la ejecucion compartida, solo cuando el numero de suscriptores baja de 1 a 0 se va a cancelar la suscripcion.

En pocas palabras, `refCount` hace que el `observable "multiscast"` automaticamente comience su ejecucion cuando ocurre la primera subscripcion, y para la ejecucion cuando la ultima subscripcion se cancela.

Ejemplo:

```javascript

var source = Rx.Observable.interval(500);
var subject = new Rx.Subject();
var refCounted = source.multicast(subject).refCount();
var subscription1, subscription2, subscriptionConnect;

// This calls `connect()`, because
// it is the first subscriber to `refCounted`
console.log('observerA subscribed');
subscription1 = refCounted.subscribe({
  next: (v) => console.log('observerA: ' + v)
});

setTimeout(() => {
  console.log('observerB subscribed');
  subscription2 = refCounted.subscribe({
    next: (v) => console.log('observerB: ' + v)
  });
}, 600);

setTimeout(() => {
  console.log('observerA unsubscribed');
  subscription1.unsubscribe();
}, 1200);

// This is when the shared Observable execution will stop, because
// `refCounted` would have no more subscribers after this
setTimeout(() => {
  console.log('observerB unsubscribed');
  subscription2.unsubscribe();
}, 2000);


```
Y tiene como resultado:

```
observerA subscribed
observerA: 0
observerB subscribed
observerA: 1
observerB: 1
observerA unsubscribed
observerB: 2
observerB unsubscribed

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