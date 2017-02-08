# Vida y **Handlers** a nuestra Interfaz!
Ahora haremos que se abra una ventana de selección de archivo cuando hagamos click en el *boton*, y se escriba la ruta del archivo seleccionado en *cajonDeTexto*.  
Este tipo de cosas se resuelven con el uso de los **Handlers**.  
Los **Handlers** son objetos que están asociados a otro objeto y un **evento**.  
Los **eventos** son situaciones que ocurren, acciones que genera el usuario, que disparan consecuencias.  
En nuestro caso, tenemos al objeto *boton*, y al evento *onAction*. Para el *boton*, el *onAction* es el click en el botón.  
Entonces, si nosotros creamos un **Handler** propio, y se lo asignamos al evento *onAction* del *boton*, cuando alguien haga click en el boton, se ejecutará el código de nuestro **handler**.

## Creando el Handler
Después de la creación del botón en nuestro código, creamos el EventHandler y se lo asignamos al boton:
```java
			Button boton = new Button("Examinar");
			boton.setOnAction(   new EventHandler<ActionEvent>() {}   );
```
## Creando el método
Ya tenemos nuestro EventHandler creado y asignado al boton, mediante el método **setOnAction**.
Ahora, nuestro EventHandler tiene que tener un método, que es el que se ejecutará en el momento del click sobre el botón.
```java
		boton.setOnAction(   new EventHandler<ActionEvent>() {
			@Override public void handle(ActionEvent e) {

			}
		});
```
## Programamos lo que el Handler hará
Ahora solo queda llenar el método *handle* con lo que queremos que haga la aplicación al hacer click en el botón.
### FileChooser
Queremos que nuestra aplicación abra una ventana donde nos permita seleccionar el archivo desde nuestra computadora.  
JavaFX tiene una clase que se llama **FileChooser**. Esta clase nos permite crear el objeto que hace de ventana para la búsqueda de los archivos en disco.  
Lo creamos y lo llamamos *selectorDeArchivo*.  
Luego le cambiamos el título que tendra la ventana por "Abrí el archivo Excel".
```java
		boton.setOnAction(new EventHandler<ActionEvent>() {
			@Override public void handle(ActionEvent e) {
				FileChooser selectorDeArchivo = new FileChooser();
				selectorDeArchivo.setTitle("Abri el archivo Excel");				
			}
		});
```
### File
Ahora, a nosotros nos intereza que el **FileChooser** nos de la información del archivo que el usuario escoge al abrirse la ventana.  
**FileChooser** devuelve esa información cuando le indicamos que se active con el método **showOpenDialog**.  
Entonces, igualamos esa llamáda al método a una variable del tipo **File** y la llamamos *archivoSeleccionado*:


```java
				FileChooser selectorDeArchivo = new FileChooser();
				selectorDeArchivo.setTitle("Abri el archivo Excel");
				
				File archivoSeleccionado = selectorDeArchivo.showOpenDialog(primaryStage);
```
### Ruta del archivo
Listo! solo nos falta obtener la ruta del archivo y escribirla en el *cajonDeTexto*.  
Para esto creamos una variable de tipo **String**, la llamamos *ruta* y le asignamos el valor de la ruta absoluta del archivo, llamando al método **getAbsolutePath** de *archivoSeleccionado*.  
Luego, asignamos la ruta al *cajonDeTexto* llamando a su método **setText**.  
Por las dudas, antes de hacerlo, verificamos que el *archivoSeleccionado* no sea *null*. Eso significaría que fuese nulo. Por ejemplo, si la persona no encuentra el archivo y hace click en Cancelar, no vamos a tener ningún archivo, por lo que el método **getAbsolutePath** fallaría. Si antes chequeamos que no sea nulo, prevenimos al programa de esa posibilidad y nunca fallará.
```java
				FileChooser selectorDeArchivo = new FileChooser();
				selectorDeArchivo.setTitle("Abri el archivo Excel");
				
				File archivoSeleccionado = selectorDeArchivo.showOpenDialog(primaryStage);			
				
				if (archivoSeleccionado != null) {
					String ruta = archivoSeleccionado.getAbsolutePath()
					cajonDeTexto.setText(ruta);
				}
```
## El código completo


```java
package application;

import java.io.File;

import javafx.application.Application;
import javafx.event.ActionEvent;
import javafx.event.EventHandler;
import javafx.geometry.Pos;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.control.Label;
import javafx.scene.control.TextField;
import javafx.scene.layout.HBox;
import javafx.stage.FileChooser;
import javafx.stage.Stage;

public class Main extends Application {
	@Override
	public void start(Stage primaryStage) {
		try {
			HBox root = new HBox();

			Label texto = new Label("Excel");
			TextField cajonDeTexto = new TextField();
			Button boton = new Button("Examinar");

			root.getChildren().add(texto);
			root.getChildren().add(cajonDeTexto);
			root.getChildren().add(boton);

			root.setAlignment(Pos.CENTER);
			root.setSpacing(3);

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

			Scene scene = new Scene(root,400,400);
			scene.getStylesheets().add(getClass().getResource("application.css").toExternalForm());
			
			primaryStage.setTitle("ExcelPTF - Utilidad para Excels!");
			primaryStage.setScene(scene);
			primaryStage.show();

		} catch(Exception e) {
			e.printStackTrace();
		}
	}

	public static void main(String[] args) {
		launch(args);
	}
}

```





