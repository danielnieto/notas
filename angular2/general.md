# RxJS

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