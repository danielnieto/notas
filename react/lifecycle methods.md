# LifeCycle Methods

Son metodos que se llaman en ciertos puntos de la vida de un componente

Hay 3 categorias:

- Mount: Cuando el componente se monta por primera vez (solo la primer instancia)
	- `componentWillMount`: cuando el componente se va a montar (solo la primer instancia)
	- `render`: Cuando se renderiza, a partir del segundo "render"
	- `componentDidMount`: despues de que el componente se haya montado
- Update: Cuando una instancia del componente se renderiza (comenzando con el segundo render)
	- `componentWillReceiveProps`: se puede usar para comparar valores de los `props`, (este metodo tiene como parametro `nextProps`) y decidir que es lo que se va a "almacenar" o "renderizar"
	- `shouldComponentUpdate`: toma `nextProps` y `nextState` como parametros y dependiendo su valor de retorno (`true` o `false`) actualiza o no el componente. Si regresa `true` todo ocurre normal, pero si es `false` detiene la ejecucion de los demas Life Cycle events.
	- `componentWillUpdate`: recibe `nextProps` y `nextState` como parametros, en este metodo NO se puede llamar `this.setState`, sirve para interactuar con cosas fuera de React, como llamar a una API, o checar el tamaño de la ventana o algo similar.
	- `render`
	- `componentDidUpdate`: recibe `prevState` y `prevProps`, este metodo es usualmente para interactuar con cosas fuera de React, como `componentWillUpdate` pero se ejecuta despues de `render`
- Unmount: Cuando un componente se remueve del DOM. Solo hay un metodo en esta categoria
	- `componentWillUnmount`: se llama justo antes de que el componente se remueva del DOM, si el componente inicializa algo que require limpieza (como intervals) este es el lugar para limpiarlos.