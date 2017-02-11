#Diseño Responsivo en Oracle JET

JET soporta los siquientes media queries
 
<table>
	<tr>
		<th>Ancho</th>
		<th>Rango Predeterminado (px)</th>
		<th>Ejemplo de dispositivo</th>
	</tr>
	<tr>
		<td>small</td>
		<td>0-767</td>
		<td>telefonos</td>
	</tr>
	<tr>
		<td>medium</td>
		<td>768-1023</td>
		<td>tablet vertical</td>
	</tr>
	<tr>
		<td>large</td>
		<td>1024-1280</td>
		<td>tablet horizontal, escritorio</td>
	</tr>
	<tr>
		<td>extra large</td>
		<td>1281+</td>
		<td>escritorio grande</td>
	</tr>
</table>

##Oracle JET Flex, Grid and Helper Classes

Cada clase de JET tiene el siguiente formato:

`oj-size-function-[1-12]columns``size` puede ser uno de `sm, md, lg, xl` (correspondientes a los media queries)

JET aplica el estilo del tamano especificado y tamanos mas grandes a menos que `function` sea definida como `only` for ejemplo:

- `oj-lg-hide` oculta contenido en pantallas `large` y `extra-large`
- `oj-md-only-hide` oculta contenido **SOLO** en pantallas `medium`, no tiene efecto en otros tamaños.

##Flex 
Oracle JET tiene dos clases para hacer uso de Flexbox de CSS, `oj-flex` para el contenedor padre y `oj-flex-item` para los hijos:

```html
<div class="oj-flex">
    <div class="oj-flex-item">1</div>
    <div class="oj-flex-item">2</div>
    <div class="oj-flex-item">3</div>
    <div class="oj-flex-item">4</div>
    <div class="oj-flex-item">5</div>
</div>
```

Normalmente JET usa la propiedad `flex` con su valor en `auto`, que permite a los elementos crecer y encogerse, sin embargo, la propiedad de CSS nativo original tiene un valor de `initial`, el cual permite a un elemento encogerse, pero no crecer.

Para poder usar flex de esta manera, se pueden utilizar dos clases mas, `oj-sm-flex-items-initial` para el contenedor (se le aplica a todos los hijos) o agregar `oj-sm-flex-initial` a un hijo
## Clases Miscelanea 

- `oj-flex-items-pad`: agrega padding horizontal(10px) a los flex items
-  `oj-size-flex-items-1` : donde size es (sm, md, lg, xl), asigna la propiedad `flex:1` de todos los items hijos de un contenedor.
-  `oj-size-flex-1`: asigna la propiedad `flex: 1` a este item.
-  `oj-size-flex-nowrap`: asigna la propiedad `flex-wrap: nowrap`, (por defecto, JET usa `flex-wrap: wrap` para todos los `oj-flex`)

##Grid

JET usa un sistema similar a bootstrap con 12 columnas, la manera de asignar tamanos a elementos es por medio de 

`oj-size-columns`

Por ejemplo, un layout podria ser

```html
<div class="oj-flex">	<div class="oj-md-6 oj-lg-2 oj-xl-8 oj-flex-item">A</div>
	<div class="oj-md-3 oj-lg-4 oj-xl-2 oj-flex-item">B</div>
	<div class="oj-md-3 oj-lg-6 oj-xl-2 oj-flex-item">C</div></div>
```
El container debe ser un `oj-flex`

### Clases de Conveniencia

- `oj-size-odd-cols-numberofcolumns`: En lugar de asignar una clase a cada item, puedes asignar esta clase al padre, de tal manera que todas los elementos de las columnas **impar** tomaran `numberofcolumns` columnas por ejemplo:

```html
<div class="oj-md-odd-cols-4">
    <div class="oj-flex">
        <div class="oj-flex-item">col 1</div>
        <div class="oj-flex-item">col 2</div>
    </div>
    <div class="oj-flex">
        <div class="oj-flex-item">col 1</div>
        <div class="oj-flex-item">col 2</div>
    </div>
    <div class="oj-flex">
        <div class="oj-flex-item">col 1</div>
        <div class="oj-flex-item">col 2</div>
    </div>
</div>
```
Solo la primer columna tomara 4 espacios, la segunda tomara el restante

- `oj-size-even-cols-numberofcolumns`: Lo mismo que el anterior pero esta sirve para asignar el ancho de las columnas **pares**

Se pueden (deberian) utilizar ambas clases en un mismo contenedor para controlar el tamano de cada una de las columnas (par e impar)

##Layout Responsivo

Utiliza las siguientes clases para hacer apps responsivas

- `oj-hybrid-applayout-*`
- `oj-web-applayout-*`

##Forms

- `oj-form`: Se pone en el padre de los controles del form para darle espacio entre controles

- `oj-form-control-group`: agrupa controles y les da espacio con otros grupos

- `oj-form-cols` y `oj-form-cols-labels-inline`: controla el layout de los controles dependiendo del tamaño de la pantalla. (ver usos en [cookbook](http://www.oracle.com/webfolder/technetwork/jet/jetCookbook.html?component=forms&demo=formvertical))

- `oj-size-label-inline`: muestra el label inline.

- `oj-size-labels-inline`: muestra todos los labels inline, se pone en el parent

- `oj-size-label-nowrap`: `nowrap` en el label, el texto se trunca si es muy grande.

- `oj-size-labels-nowrap`:`nowrap` en todos los labels, el texto se trunca si es muy grande, se pone en el parent.