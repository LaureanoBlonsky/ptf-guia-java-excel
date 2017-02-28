# Buscar y reemplazar!

Recordemos lo que nos propusimos:  
1. Crear una interfaz sencilla que nos permita seleccionar un Excel que esté en nuestra computadora. **(HECHO!)**  
2. Vamos a buscar alguna palabra o número dentro del Excel e informar su ubicación. **(HECHO!)**  
3. **Vamos a reemplazar una palabra por otra dentro de uno o mas Excels.**  
4. Vamos a seleccionar un Excel y hacerle todas unas modificaciones y adaptarlo para que otro programa lo pueda leer.  

Ahora vamos por el punto 3!  

## Creamos **PanelBuscarYReemplazar**  

Entonces creemos un nuevo panel, que hará este nuevo trabajo.  

Para eso creamos la clase **PanelBuscarYReemplazar**:

```java  
package application;

import java.io.File;
import java.io.IOException;
import java.util.List;

import javafx.geometry.Pos;
import javafx.scene.control.Button;
import javafx.scene.control.Label;
import javafx.scene.control.TableColumn;
import javafx.scene.control.TableRow;
import javafx.scene.control.TableView;
import javafx.scene.control.TextField;
import javafx.scene.control.cell.PropertyValueFactory;
import javafx.scene.layout.BorderPane;
import javafx.scene.layout.HBox;
import javafx.scene.layout.Priority;
import javafx.stage.FileChooser;
import javafx.stage.FileChooser.ExtensionFilter;
import javafx.stage.Stage;

public class PanelBuscarYReemplazar extends BorderPane{

}
```  

Esos son los *imports* que vamos a necesitar. Mas adelante veremos como hacer cuando no sepamos cuales imports necesitaremos de antemano (como en realidad siempre nos sucede en la vida real).  

Notar que la clase *extiende* de **BorderPane**. Eso significa que nuestra clase va a ser un panel con todas las características de un **BorderPane**, mas las características y código que nosotros sumemos.  

En los próximos pasos veremos mas sobre el **BorderPane** y todo lo que nos facilita.  

## Cambiamos el **Main**  

Ahora vamos a modificar nuestra clase **Main** de la siguiente forma, para que en vez de tomar el **PanelBusqueda** anterior que habíamos hecho, use el nuevo que acabamos de hacer:  

```java  
package application;

import javafx.application.Application;
import javafx.scene.Scene;
import javafx.stage.Stage;

public class Main extends Application {
	@Override
	public void start(Stage primaryStage) {
		try {

			PanelBuscarYReemplazar root = new PanelBuscarYReemplazar(primaryStage);

			Scene scene = new Scene(root);
			scene.getStylesheets().add(getClass().getResource("application.css").toExternalForm());

			primaryStage.setTitle("ExcelPTF - Utilidad para Excels!");
			primaryStage.setScene(root.getScene());
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

Al final de este tutorial crearemos una pantalla con pestañas, para que todas las pantallas que creamos puedan coexistir en la misma aplicación!  

## Diseñamos el **PanelBuscarYReemplazar**  

Crearemos la siguiente interfaz:  
![ima](images/panelbuscaryreemplazar.png)  

En la parte superior está el botón que nos permitirá agregar Excels a nuestra tabla de Excels.  

Como decíamos antes, esta pantalla nos permitirá reemplazar palabras en uno o mas Excels. Será útil si tenemos muchos archivos y queremos cambiar algo por otra cosa, en todos a la vez, sin tener que entrar uno por uno.  

En el medio hay una tabla con dos columnas. La columna *Archivo* tendrá las rutas de los archivos que vayamos agregando. En la columna *Reemplazos* se marcará la cantidad de reemplazos que se hicieron en cada archivo.  

Luego, en la parte inferior, tenemos dos cajones de texto. En el primero escribiremos el texto a buscar, y en el segundo, el texto nuevo a reemplazar.  

Con el botón *Reemplazar* pasamos a realizar la operación.  

### **BorderPane**  

Como dijimos, vamos a basar nuestro panel en el **BorderPane**. Antes habíamos basado el panel **PanelBusqueda** en el tipo **HBox**.  
El **HBox** sirve para poner componentes en pantalla, y todos se dispongan uno al lado del otro, horizontalmente.  

Pero en nuestro caso tenemos una interfaz un poco mas complicada. Solo con componentes uno al lado de otro no la podemos lograr.  

Es por esto que acudimos al **BorderPane**. Tiene la siguiente estructura y disposición de elementos:  

![im](images/borderpane.png)  

Que significa eso? Que, cuando agreguemos elementos al panel, le indicaremos en que zona queremos que se agreguen.  

Entonces, al boton de *Agregar Excel* lo pondremos en la zona *Top*.  
A la tabla la pondremos en la zona *Center*.  
Al botón *Reemplazar* y los cajones de texto, en *Bottom*.  
Las zonas *Left* y *Right* las dejaremos vacías.  

### Y **VBox**?...  
