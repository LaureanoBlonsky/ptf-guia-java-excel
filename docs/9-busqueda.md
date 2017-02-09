# Búsqueda dentro de un Excel  

Recordemos lo que nos propusimos:
1. Crear una interfaz sencilla que nos permita seleccionar un Excel que esté en nuestra computadora. **(HECHO!)**  
2. **Vamos a buscar alguna palabra o número dentro del Excel e informar su ubicación.**  
3. Vamos a reemplazar una palabra por otra dentro de uno o mas Excels.  
4. Vamos a seleccionar un Excel y hacerle todas unas modificaciones y adaptarlo para que otro programa lo pueda leer.  

Ya tenemos la ruta donde está el archivo Excel que queremos usar. Ahora nos falta que nuestro programa lo abra.  
Ojo! Como usuario del programa, no vamos a ver la planilla abierta con su contenido. Lo que la aplicación va a hacer es abrirla internamente, para poder acceder a su contenido.  
Una vez que tengamos acceso a su contenido, buscaremos en todas las celdas para ver en cual de ellas se encuentra la palabra a buscar.  

Para eso, también necesitamos que la interfaz tenga un campo de texto en donde poner la palabra a buscar, y otro boton para realizar la búsqueda.  

## Interfaz  

Vamos a hacerlo muy sensillo. A nuestra clase **PanelSeleccionArchivo** le agregamos los siguientes componentes:  
1. Un objeto de tipo **TextField** que llamaremos *cajonDeTextoABuscar*.  
2. Un objeto de tipo **Button** que llamaremos *botonBuscar*.  

Para eso, primero, en la primer parte de la clase **PanelSeleccionArchivo**, en el mismo lugar donde tenemos los demas componentes declarados, agregamos los nuevos:  
```java
public class PanelSeleccionArchivo extends HBox{

	Label texto;
	TextField cajonDeTexto;
	Button boton;
	Stage primaryStage;
	TextField cajonDeTextoABuscar;
	Button botonBuscar;
  .
  .
  .
```  

Luego, los inicializamos y agregamos al panel. Hacemos esto en el método *inicializarComponentes* que habíamos escrito:  
```java
	private void inicializarComponentes() {
		texto = new Label("Excel");
		getChildren().add(texto);

		cajonDeTexto = new TextField();
		getChildren().add(cajonDeTexto);

		boton = new Button("Examinar");
		getChildren().add(boton);
		
		cajonDeTextoABuscar = new TextField();
		getChildren().add(cajonDeTextoABuscar);
		
		botonBuscar = new Button("Buscar");
		getChildren().add(botonBuscar);
	}
```  
Ejecutamos la aplicación y si nos salió todo perfecto, ya veríamos los nuevos controles:  
![Foto](images/nuevos_controles.png)  
Puede que la aplicación no sea muy atractiva todavía. Incluso puede ser que las palabras de los botones aparezcan recortadas. No le vamos a dar bola a eso por ahora.  
Mas adelante nos vamos a preocupar por mejorar la estética!  

## Abrir el Excel  

Listo! Ahora ya podemos abrir el excel y hacer la búsqueda.  
Haremos que cuando uno haga click en el botón de Buscar, se abra el Excel y se haga la búsqueda.  
Entonces, arranquemos con el **Handler**!  

### Handler de búsqueda  

Debemos agregar el código del **Handler** para el nuevo *botonBuscar*. Lo haremos en el método *crearHandlers* de la clase **PanelSeleccionadoArchivo** que ya tenemos hecho:  

Pero lo haremos de una forma distinta al anterior. Usaremos algo que se llama "expresión Lambda". Estas expresiones sirven para hacer el código mas córto.  

Comparemos como es el código del **Handler** que habíamos escrito para *boton* y como es el del *botonBuscar* que agregamos ahora:  

```java
	private void crearHandlers() {
		boton.setOnAction(new EventHandler<ActionEvent>() {
		    @Override public void handle(ActionEvent e) {
		    	FileChooser selectorDeArchivo = new FileChooser();
				selectorDeArchivo.setTitle("Abri el archivo Excel");

				File archivoSeleccionado = selectorDeArchivo.showOpenDialog(primaryStage);

				if (archivoSeleccionado != null) {
					String ruta = archivoSeleccionado.getAbsolutePath();
					cajonDeTexto.setText(ruta);
				}
		    }
		});

		botonBuscar.setOnAction(e -> buscar());
		
	}
```  

Que significa? Que cuando uno haga click en el *botonBuscar*, la acción que se disparará será ejecutar el método llamado *buscar*.  
