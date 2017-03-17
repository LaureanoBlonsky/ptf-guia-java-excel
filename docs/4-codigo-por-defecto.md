(3. Creación del esqueleto del programa) [<- Atrás](3-creacion-programa.md) || [Siguiente ->](5-programar_javafx.md) (5. Programar con JavaFX)  

# 4. Código Base del programa  
Cuando creamos el proyecto, se nos creó un código y estructura base con una ventana vacía, lista para que le agreguemos los componentes que queramos.   

Lo principal lo encontramos en la clase **Main.java**.
## Clase Main
```java
package application;
	
import javafx.application.Application;
import javafx.stage.Stage;
import javafx.scene.Scene;
import javafx.scene.layout.BorderPane;

public class Main extends Application {
	@Override
	public void start(Stage primaryStage) {
		try {
			BorderPane root = new BorderPane();
			Scene scene = new Scene(root,400,400);
			scene.getStylesheets().add(getClass().getResource("application.css").toExternalForm());
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
### Package
En la primer linea, simplemente se indica el package al cual la clase (Main) pertenece. (Mas de esto en un rato).  
```java
package application;
```
### Imports
Lineas 3 a 6: en esas lineas, se hacen los “import”. Cuando tenemos una librería que queremos usar en nuestra aplicación, como la de JavaFX en nuestro caso, necesitamos indicarle al compilador de Java que las queremos. La forma de hacer esto es “importando” las clases de dichas librerías. Entonces, para nuestra base de la aplicación, es necesario Importar las clases Application, Stage, Scene y BorderPane, todas pertenecientes a la librería JavaFX. Por ejemplo, si no importáramos la clase BorderPane en la linea 6, la linea 12 fallaría, por no poder encontrar de donde sacar el tipo de clase BorderPane.  
```java
import javafx.application.Application;
import javafx.stage.Stage;
import javafx.scene.Scene;
import javafx.scene.layout.BorderPane;
```
### Declaración de la clase Main
Linea 8: es la declaración de la clase Main. Nuestro archivo se llama “Main.java” porque dentro contiene a la clase Main. La forma de declararla es como está en la linea 8, en donde se dice que Main es una clase (class) publica (public) que extiende (extends) de la clase Application.
 No es el objetivo de esta Guía profundizar en los conceptos de programación orientada a objetos o de la sintaxis de Java. Revisá con tu mentor estas bases si lo necesitás!  
 ```java
public class Main extends Application {
	
}
```
### Método *start*
Se define el método *start*. Es el método que se va a ejecutar cuando la aplicación se inicie y contiene el principio de nuestro código.  
El *Override* significa que reemplaza al método *start* que exista en la clase que extiende ésta. Esta clase *Main* extiende de la clase *Application*.  
Entonces, al usar *Override*, le decimos al compilador que reemplace el método *start* de la clase *Application* por el nuestro.
```java
	@Override
	public void start(Stage primaryStage) {

	}
```

### Try / Catch
Los bloques Try/Catch sirven para indicarle a la computadora que ejecute todo lo que está “dentro del Try” (es decir, las lineas 12 a 16), y si algo falla, que ejecute lo que está “dentro del Catch”. Esto sirve para asegurarse de que si algo falla, siempre se ejecute lo que "está dentro del catch", que es la encargada de mostrar el error.
```java
		try {
			//dentro del Try
		} catch(Exception e) {
			//dentro del Catch
		}
```


### Border Pane
Se declara y crea el objeto con nombre “root”, que es de tipo **BorderPane**. Entonces, root es nuestro **[RootPane](programar_javafx.html)**.  
Es el panel en donde se van a poner los distintos elementos visuales.
```java
			BorderPane root = new BorderPane();
```

### Scene
Se declara y crea el objeto de nombre “scene”, que es del tipo **Scene**. Es nuestra primer **[Scene](programar_javafx.html)**(escena). En el constructor se le pasa dos veces 400, para indicar que es de tamaño 400px de alto y 400px de ancho, y se le pasa también el objeto “root”, para indicarle que ése será su RootPane.
```java
			Scene scene = new Scene(root,400,400);
			scene.getStylesheets().add(getClass().getResource("application.css").toExternalForm());
```
Mediante el método **getStylessheets().add()**, se le agrega la hoja de estilos **application.css** al objeto **scene**. Las hojas de estilos sirven para definir estilos y efectos visuales para la interfaz. Por ejemplo, en la hoja de estilos podemos poner que las letras de los textos sean de color rojo.

### Asignación del *scene* creado
Al objeto **primaryStage**, que es nuestra **[stage](programar_javafx.html)** (escenario) se le asigna, mediante el método setScene, la escena “scene”.
```java
			primaryStage.setScene(scene);
			primaryStage.show();
```
Se llama al método show del objeto **primaryStage**. Es en este momento en donde la aplicación aparece en pantalla, mostrando la ventana (por el momento vacía).
### **Catch**, por si algo sale mal...
Declaración del bloque Catch.
Si dentro de las sentencias del bloque **Try** sucede algún error, se ejecuta el método **printStackTrace** del objeto **e**, que hace que se muestre el error por la salida de texto del aplicativo.
```java
		catch(Exception e) {
			e.printStackTrace();
		}
```

### El método **main**
Declaración del método main. Es el primer método que se ejecuta al iniciar la aplicación.

```java
	public static void main(String[] args) {
		launch(args);
	}
```
Se ejecuta el método “launch”. Éste método dispara toda una serie de tareas internas de Java para preparar toda la aplicaicón, que terminan llamando y ejecutando al método “start” de la linea 10, en el cual nosotros comenzamos a armar la aplicación con el código dentro de ese método. 

# [Indice](../README.md#indice)  
(3. Creación del esqueleto del programa) [<- Atrás](3-creacion-programa.md) || [Siguiente ->](5-programar_javafx.md) (5. Programar con JavaFX)    
