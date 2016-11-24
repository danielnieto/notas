#Hello world con Electron

1. Crear la carpeta del proyecto
2. Ir a la carpeta desde la terminal
3. Dentro de la carpeta ejecutar `npm init` y llenar los datos requeridos
4. Instalar electron: `npm install electron --save`
5. Crear un `index.html` con el contenido de la app (este archivo no necesariamente debe llamarse index, puede llamarse de cualquier manera)
6. Crear un archivo `main.js` (de igual manera, puede llamarse como sea)
7. Agregar el siguiente codigo en `main.js`

	```javascript
		const {app, BrowserWindow} = require("electron");

		app.on("ready", ()=>{
		
		    let mainWindow = new BrowserWindow();
		
		    mainWindow.loadURL(`file://${__dirname}/index.html`);
		
		});
	``` 
	
	Lo unico que hace este codigo es crear una nueva ventana, y carga el archivo `index.html` en ella

8.	Modificar en el archivo `package.json` el atributo `main` para que apunte al archivo JS principal (`main.js` que es nuestro punto de entrada a la app)

	```
	...
	"main": "main.js",
	...
	```
	
9. Para ejecutar la app desde la consola ejecutar `electron .`