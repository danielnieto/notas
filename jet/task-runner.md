#Task Runner

Para lanzar la aplicacion utiliza

`grunt build`

y despues

`grunt serve`


los puertos default para `serve` son `8000` para el servidor y `35729` para el livereload, para tener mas de una aplicacion JET corriendo al mismo tiempo se deben modificar los puertos default a otro puerto libre para que dos `serve` no compitan por el mismo puerto.

```
grunt serve --server-port=8000 -livereload-port=35729
```