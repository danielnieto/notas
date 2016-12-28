# Fetch

`Fetch` es una alternativa a `XMLHttpRequest`, `fetch` regresa una promesa, y esta promesa resuelve un Response, que puedes convertir a JSON (despues de resolver otra promesa):

```javascript

var endpoint = "URL del endpoint";
var fetchResult = {};

fetch(endpoint).then(function(response){
	return response.json();	
}).then(function(json){
	fetchResult = json;
});

//Esto tambien se puede hacer de esta manera usando ES6

fetch(endpoint)
	.then(response => response.json())
	.then(json => fetchResult = json);

```