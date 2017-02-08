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
Y ni hablar si nuestra aplicación apuntara a ser un programa muy grande con muchas funciones... sería un monstruo!

## MVC
Necesitamos un orden... Así que aplicaremos un patron de diseño muy común para estos casos! El patron **MVC**!
Este patr


