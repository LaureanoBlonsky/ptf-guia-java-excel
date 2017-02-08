# Dos formas de programar con JavaFX

 Como decíamos antes, JavaFX es una librería que sirve para crear la interfaz, o sea  la parte visual de nuestra aplicación. Es decir, las ventanas, títulos, botones, cajones de texto, tablas con información, etc., etc.

 Ahora, existen dos formas de programar esas interfaces:

**Usando código Java puro**: de esta manera, nosotros, con código java puro, usamos JavaFX de la misma forma que programamos la aplicación entera y programamos la interface.

**FXML**: JavaFX introduce una forma de crear la interfaz que es muy similar a HTML. En vez de codificar en Java, se crean archivos separados, similares al HTML, en donde se especifican únicamente los componentes de pantalla. En otro archivo Java, se introduce el código que va a ejecutar o estar asignado a cada componente en pantalla. Lo útil de esto es que separamos la Interfaz de su funcionalidad, por lo que es mas cómodo y ordenado.

 La aplicación final terminada no tiene diferencias para el usuario, haya sido hecha en el método que sea. Antes de compilar la aplicación final, el compilador va a pasar todos los archivos de FXML a Java puro, por lo que el resultado es el mismo. FXML es entonces una ayuda para el desarrollo, no una característica final de cara al usuario del programa.

 En este tutorial vamos a usar el método de Java puro por los siguientes motivos:
- Seguramente sea tu primer aplicación con Java. Tratemos de aprender bien primero como funciona Java puro.
- Como se dice, el que mas abarca menos aprieta. Así que como primer vez, mejor usemos la menor cantidad de cosas posible.
- Para un programa no muy grande, como el que vamos a hacer, el uso de FXML no trae mayores ventajas.
- Confío en que en el próximo programa que hagas con Java aprendas FXML! Te será mucho mas facil ya sabiendo como es el tema con Java puro.


## La estructura de JavaFX
 Todas las aplicaciones con JavaFX, ya sean hechas diréctamente en Java puro, o con FXML, tienen la siguiente estructura:
![Imagen new javafxproject](https://laureanoblonsky.github.io/ptf-guia-java-excel/docs/images/stage-scene-pane.png)  
**Stage (escenario)**: como en una obra de teatro, el Stage es el escenario. Es el contenedor principal. Es la ventana con los botones tradicionales para Maximizar, minimizar y cerrar. Es nuestro marco para dentro armar la aplicación. Dentro, siempre va a haber una única Scene a la vez, y la misma se puede cambiar por otra cuando lo dispongamos.  

**Scene (escena)**: como en una obra de teatro, uno puede llegar a tener muchas escenas que formen la obra. Siempre habrá una escena a la vez, y la misma se puede cambiar siempre que se quiera. Entonces, podríamos tener una primer escena que dice “Bienvenido a la aplicación. Presione el siguiente boton para iniciar”. Y al precionar el boton, cambiaríamos la Scene por otra, con otros elementos.  

**Root Pane (panel raíz)**: cada Scene va a tener un Panel Raíz, que no es mas que un panel de base donde se pondrán todos los elementos: cajas de texto, botones, etc. Hay distintos tipos de Root Pane. Los distintos tipos sirven para indicarle a JavaFX de que forma se van a disponer los elementos visuales. Por ejemplo, si usamos VBox, todos los elementos que pongamos en pantalla se posicionarán uno debajo del otro. Si usamos HBox, cada elemento se pondrá al lado del otro, de forma horizontal.  

![Imagen new javafxproject](https://laureanoblonsky.github.io/ptf-guia-java-excel/docs/images/layouts.png)  
