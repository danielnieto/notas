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
-  `oj-size-flex-nowrap`: asigna la propiedad `flex-wrap: nowrap`