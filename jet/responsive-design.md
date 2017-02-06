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

