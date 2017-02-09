# Buenas practicas  
En la programación tenemos siempre muchísima libertad para escribir las cosas a nuestra manera.  
Por ejemplo, hay infinitas formas de escribir la misma aplicación que estamos haciendo nosotros en esta Guía.  
Un simple ejemplo podrían ser los nombres de las variables. Yo podría declarar la variable *cajonDeTexto* de varias formas:  
```java  
TextField cajonDeTexto = new TextField();  
TextField CAJONDETEXTo = new TextField();  
TextField cAjOndEtEXto = new TextField();  
```  
## Convenciones  
Cualquiera de las formas escritas arriba funcionan perfectamente (y no son las únicas). Pero imaginemos un programa escrito con distintas combinaciones de esas para las variables.  
Funcionaría, seguro, pero sería dificil de leer, ya que los nombres no tendrían una forma de escribirse común.  
Por esto, existen "convenciones". Las convenciones son acuerdos entre los programadores, para usar un mismo estilo a la hora de programar, así todo es mas claro y se facilita la tarea de trabajar en equipo (o leer tu propio código un año despues!).  
En Java, la convención para los nombres de las variables es que sean siempre en minúscula, y se use mayúscula para el cambio de palabra.  
Entonces, la convención dice que usemos la siguiente forma:
```java
TextField cajonDeTexto = new TextField();
```

## Patrones de diseño
Pero las convenciones no se limitan a las pequeñas libertades en la escritura de nombres. También existen convenciones mas globales, para determinar la estructura general de una aplicación.  
La aplicación que estuvimos programando funciona perfectamente, pero tiene un problemita en relación al patron de diseño...  

**Todo el código está en la clase *Main.java*.**  

A primera vista no parece ser muy grave... pero imaginemos como se vería nuestro *Main.java* al final de esta guía.  
Tendría las siguientes características:
1. Sería enorme!
2. Todo el código estaría en un solo lugar! Tanto el código de la parte visual, como el de base, como el del procesamiento de los Excels, todo, todo estaría en el mismo lugar.
3. Sería un desorden.
4. Sería dificil de debuggear (se le dice *debuggear* al acto de buscar errores en el código cuando este no funciona como se espera o da algún error)  
Y ni hablar si nuestra aplicación apuntara a ser un programa muy grande con muchas funciones... sería un monstruo encerrado en una sola clase! Daría dolor de cabeza entenderlo y mantenerlo...  

## MVC
Hay infinitas formas de ordenar el código, pero hay unas pocas convenciones que son las mas aceptadas.  
Una de ellas se llama **MVC** y son las siglas de Model-View-Controller. Ese patron es muy bueno para cuando programamos con [FXML](5-programar-javafx.html).  Nos permite separar bien las clases que hacen la interfaz visual (View), las que controlan los datos (Model) y las que controlan los idas y venidas entre estos (Controllers).  

Ahora, como nosotros no estamos usando [FXML](5-programar-javafx.html), y nuestra aplicación no será muy grande, no es necesario adoptar **MVC**. Creo que en este momento es mas importante que nos enfoquemos en los fundamentos mas básicos de Java, y dejemos las "Mejores" Prácticas para después cuando ya tengas los conceptos básicos mas fuertes. 

Por que mencionamos al patrón **MVC** entonces? Para que lo tengas presente, y en tu próxima aplicación con JavaFX uses **FXML** y **MVC**. Eso ya sería de muy buen nivel!  

**Te podes guardar este tutorial para después:** [Tuto](http://code.makery.ch/library/javafx-8-tutorial/es/part1/)  
*(link de la primer página de Google bajo la búsqueda de “javafx fxml mvc tutorial”)*

## Ordenemos nuestro código!
Entonces, encontremos una forma de ordenar las cosas que no sea ni **MVC** ni un desastre total todo metido en *Main.java*.  
Encontremos un punto medio.

Recordemos lo que tenemos hasta ahora:  
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

### El Plan!  
#### Actualmente  
Tenemos una clase *Main* con:  
1. El Try/Catch.  
2. La creación del panel **HBox** *root*.  
3. La creación de los componentes en pantalla: *texto*, *cajonDeTexto* y *boton*.  
4. Las propiedades del panel *root*: **alignment** y **spacing**.  
5. El **Handler** del *boton*.  
6. La creación de la **Scene** *scene*.  
7. La configuración de la **Stage** *primaryStage*.

#### Lo que haremos  
Vamos a crear una clase **PanelSeleccionArchivo** con:  
1. La creación del panel **HBox** *root*. (En realidad, nuestra clase *PanelSeleccionArchivo* será el panel *root*. Ya veremos como.)  
2. La creación de los componentes en pantalla: *texto*, *cajonDeTexto* y *boton*.  
3. Las propiedades del panel *root*: **alignment** y **spacing**.  
4. El **Handler** del *boton*.  

La clase *Main* ahora contendría:
1. El Try/Catch.  
2. La creación del panel **PanelSeleccionArchivo**.  
3. La creación de la **Scene** *scene*.  
4. La configuración de la **Stage** *primaryStage*.  

#### Beneficios?  
Que beneficios nos da esta propuesta?  
1. No está todo en un solo archivo.  
2. Todo lo relacionado a la pantalla está en **PanelSeleccionArchivo**.  
3. Si queremos agregar otra pantalla, no seguimos llenando la clase *Main*, sino que creamos otra clase, como **PanelSeleccionArchivo**, y tendríamos ese código nuevo en un archivo independiente al resto de la aplicación.  
4. En caso de tener una aplicación grande con 15 pantallas, no tendríamos un archivo único monstruoso, sino todo ordenado en 15 archivos independientes fáciles de leer y mantener.  

### Ahora a hacerlo!  
Hay gente que arranca haciendo las clases como **PanelSeleccionArchivo**. Hay gente que arranca modificando la clase *Main*. Cada uno tiene su forma.  

A mi me gusta modificar la clase *Main* a como creo que debería quedar, y en base a eso, crear las clases necesarias. Obviamente, si después me doy cuenta de otra cosa, puedo volver y modificar *Main*.  
Básicamente, es un proceso iterativo, en donde vamos probando y acomodando todo.  
Yo ya hice eso por ustedes, así que acá va!  
#### Main  
La clase *Main* nos queda así:  
```java
package application;

import javafx.application.Application;
import javafx.scene.Scene;
import javafx.stage.Stage;

public class Main extends Application {
	@Override
	public void start(Stage primaryStage) {
		try {

			PanelSeleccionArchivo root = new PanelSeleccionArchivo(primaryStage);

			Scene scene = new Scene(root,400,400);
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
**Atención!**: Todavía no tenemos creada nuestra clase **PanelSeleccionArchivo**, por lo que seguramente el **Eclipse** nos informe que nuestra clase tiene errores. No importa, guardamos el archivo y continuamos con la otra clase!  
#### PanelSeleccionArchivo  
La clase *Main* nos queda así:  
```java
package application;

import java.io.File;

import javafx.event.ActionEvent;
import javafx.event.EventHandler;
import javafx.geometry.Pos;
import javafx.scene.control.Button;
import javafx.scene.control.Label;
import javafx.scene.control.TextField;
import javafx.scene.layout.HBox;
import javafx.stage.FileChooser;
import javafx.stage.Stage;

public class PanelSeleccionArchivo extends HBox{

	Label texto;
	TextField cajonDeTexto;
	Button boton;
	Stage primaryStage;

	public PanelSeleccionArchivo(Stage primaryStage) {
		this.primaryStage=primaryStage;
		inicializarComponentes();
		aplicarPropiedades();
		crearHandlers();
	}

	private void aplicarPropiedades() {
		setAlignment(Pos.CENTER);
		setSpacing(3);
	}

	private void inicializarComponentes() {
		texto = new Label("Excel");
		getChildren().add(texto);

		cajonDeTexto = new TextField();
		getChildren().add(cajonDeTexto);

		boton = new Button("Examinar");
		getChildren().add(boton);
	}

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
	}

}
```  
Miremos como, incluso dentro de **PanelSeleccionArchivo** podríamos haber puesto todo el choclo de código en el constructor de la clase.  
Pero no!, queremos que todo esté ordenado, así que creamos un método para cada grupo de tareas:  
1. inicializarComponentes();  
2. aplicarPropiedades();  
3. crearHandlers();  

### Conclusión  
Ahora si... tenemos todo ordenado y listo para seguir construyendo nuestra aplicación sobre una base ahora mas clara!  
Probá la aplicación. No deberíamos ver ninguna diferencia en el resultado para el usuario. Solo modificamos la organización del código, pero el producto debe ser igual.  
