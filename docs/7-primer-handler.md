# Vida y **Handlers** a nuestra Interfaz!
Ahora haremos que se abra una ventana de selección de archivo cuando hagamos click en el botón.  
Este tipo de cosas se resuelven con el uso de los **Handlers**.  
Los **Handlers**
##
```java
			boton.setOnAction(new EventHandler<ActionEvent>() {
			    @Override public void handle(ActionEvent e) {
			    	FileChooser selectorDeArchivo = new FileChooser();
					selectorDeArchivo.setTitle("Abri el archivo Excel");
					selectorDeArchivo.getExtensionFilters().addAll(
							new ExtensionFilter("Archivos Excel", "*.xls","*.xlsx")							
							);
					File archivoSeleccionado = selectorDeArchivo.showOpenDialog(primaryStage);
					if (archivoSeleccionado != null) {
					   cajonDeTexto.setText(archivoSeleccionado.getAbsolutePath());
					}
			    }
			});
```



```java
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
import javafx.stage.FileChooser.ExtensionFilter;
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
					selectorDeArchivo.getExtensionFilters().addAll(
							new ExtensionFilter("Archivos Excel", "*.xls","*.xlsx")							
							);
					File archivoSeleccionado = selectorDeArchivo.showOpenDialog(primaryStage);
					if (archivoSeleccionado != null) {
					   cajonDeTexto.setText(archivoSeleccionado.getAbsolutePath());
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
