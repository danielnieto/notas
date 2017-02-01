#Oracle JET

##General

Oracle JET soporta el patron de diseño Modelo-Vista-VistaModelo (Model-View-ViewModel) o MVVM.

En MVVM, el `Model` representa los datos de la aplicacion, y el `View` es la presentacion de los datos. El `ViewModel` expone los `model` al `view` y mantiene el estado de la aplicacion.

The Oracle JET Common Model and Collection Application Programming Interface (API) implements the model layer. The API includes the following JavaScript objects:

El Oracle JET Common Model and Collection API implementa la capa de modelo. El API incluye los siguientes objetos:
- `oj.Model`: Representa un los datos de un solo registro de un servicio de datos (como un RESTful web service)- `oj.Collection`: Representa un set de registros, y es una lista de objetos `oj.Model` del mismo tipo.- `oj.Events`: Provee metodos para manejo de eventos- `oj.KnockoutUtils`: Provee metodos para mapear atributos de un `oj.Model` o una `oj.Collection` a un observable de Knockout

## Instalacion

Usar el generador yeoman para hacer scaffolding del proyecto

## Configuracion

Hay un archivo llamado `oraclejetconfig.json` en donde puedes customizar 