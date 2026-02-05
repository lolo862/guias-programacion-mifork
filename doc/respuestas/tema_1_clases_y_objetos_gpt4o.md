<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Clases y Objetos". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: ninguno.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->

# TEMA 1. Clases y objetos

## 1. ¿Cuáles son las cuatro características básicas de la programación orientada a objetos? Describe brevemente cada una

Respuesta

La programación orientada a objetos (POO) se basa en cuatro características principales: abstracción, encapsulamiento, herencia y polimorfismo. La abstracción consiste en representar conceptos del mundo real mediante clases y objetos, destacando únicamente los detalles relevantes y ocultando los innecesarios. Esto permite modelar sistemas complejos de forma más clara.

El encapsulamiento es el mecanismo que protege los datos de un objeto y controla el acceso a ellos mediante métodos o funciones, evitando que sean modificados directamente desde fuera de la clase. La herencia permite que una clase derive de otra, reutilizando atributos y métodos existentes y facilitando la extensión y especialización de comportamientos. Por último, el polimorfismo permite que un mismo método pueda comportarse de manera distinta según el tipo de objeto que lo invoque, aumentando la flexibilidad del código.

## 2. Cita cuatro lenguajes populares que permitan la programación orientada a objetos

Respuesta

Algunos lenguajes populares que implementan programación orientada a objetos son Java, C++, Python y C#. Cada uno ofrece mecanismos de clases, objetos y métodos, aunque difieren en la sintaxis y algunas características específicas como gestión de memoria o herencia múltiple.

Otros lenguajes, como Ruby o Swift, también se orientan a objetos, pero destacan por su sintaxis más moderna y facilidades para ciertos patrones de diseño. En todos estos lenguajes, la POO permite organizar el código en torno a objetos que combinan datos y funciones.

## 3. Los paradigmas anteriores a la POO, ¿Qué es la **programación estructurada**? y, todavía mejor, ¿Qué es la **programación modular**?

Respuesta

La programación estructurada es un paradigma basado en el uso de estructuras de control (secuencias, decisiones y bucles) y evita el uso de saltos incondicionales como goto. El objetivo es que el flujo de ejecución sea claro y predecible, facilitando la comprensión y el mantenimiento del código.

La programación modular extiende la estructurada dividiendo el programa en módulos o unidades independientes, cada uno con una funcionalidad concreta. Cada módulo puede definirse en un archivo separado y reutilizarse en distintos contextos. Esto reduce la duplicación de código y facilita la colaboración entre varios programadores.

## 4. ¿Qué tres elementos definen a un objeto en programación orientada a objetos?

Respuesta

Un objeto en POO se define principalmente por tres elementos: estado, comportamiento e identidad. El estado se representa mediante atributos o variables que contienen información sobre el objeto en un momento dado.

El comportamiento se refleja mediante métodos o funciones que permiten al objeto realizar acciones o modificar su estado. La identidad distingue a un objeto de otro, incluso si tienen el mismo estado o comportamiento, y permite referirse a él de manera única dentro del programa.

## 5. ¿Qué es una clase? ¿Es lo mismo que un objeto? ¿Qué es una instancia? ¿Todos los lenguajes orientados a objetos manejan el concepto de clase?

Respuesta

Una clase es una plantilla o molde que define los atributos y métodos que tendrán los objetos de ese tipo. No es lo mismo que un objeto, ya que la clase es la definición y el objeto es un ejemplar concreto de esa definición.

Una instancia es un objeto creado a partir de una clase. Por ejemplo, si Punto es una clase, p1 puede ser una instancia de esa clase. No todos los lenguajes orientados a objetos manejan clases explícitamente; por ejemplo, en JavaScript los objetos pueden crearse directamente sin necesidad de definir una clase.


## 6. ¿Dónde se almacenan en memoria los objetos? ¿Es igual en todos los lenguajes? ¿Qué es la **recolección de basura**? 

Respuesta

En Java, los objetos se almacenan generalmente en el heap, una zona de memoria dinámica, mientras que las referencias a ellos pueden residir en la stack. En C++ es posible almacenar objetos tanto en el stack como en el heap, según cómo se creen.

No todos los lenguajes gestionan la memoria de la misma manera. Java y Python incluyen recolección de basura, un mecanismo automático que libera memoria de objetos que ya no son accesibles, evitando fugas de memoria. En C++, la gestión de memoria suele ser manual, usando delete para liberar objetos creados en el heap.


## 7. ¿Qué es un método? ¿Qué es la **sobrecarga de métodos**? 

Respuesta

Un método es una función definida dentro de una clase que describe un comportamiento del objeto. Permite modificar el estado del objeto o realizar acciones relacionadas con él.

La sobrecarga de métodos consiste en definir varios métodos con el mismo nombre pero con diferentes parámetros dentro de la misma clase. Esto permite utilizar un mismo concepto de método para distintos tipos o cantidades de datos, aumentando la flexibilidad del código.


## 8. Ejemplo mínimo de clase en Java, que se llame Punto, con dos atributos, x e y, con un método que se llame `calculaDistanciaAOrigen`, que calcule la distancia a la posición 0,0. Por sencillez, los atributos deben tener visibilidad por defecto. Crea además un ejemplo de uso con una instancia y uso del método

class Punto {
    double x;
    double y;

    double calculaDistanciaAOrigen() {
        return Math.sqrt(x*x + y*y);
    }
}

public class Test {
    public static void main(String[] args) {
        Punto p = new Punto();
        p.x = 3;
        p.y = 4;
        System.out.println(p.calculaDistanciaAOrigen()); // Imprime 5.0
    }
}
Este ejemplo crea la clase Punto con dos atributos x e y y un método que calcula la distancia al origen. Luego se instancia un objeto p y se llama al método para obtener la distancia.


## 9. ¿Cuál es el punto de entrada en un programa en Java? ¿Qué es `static` y para qué vale? ¿Sólo se emplea para ese método `main`? ¿Para qué se combina con `final`?

Respuesta

El punto de entrada en un programa Java es el método main, que debe tener la firma public static void main(String[] args). Este método se ejecuta al iniciar el programa.

La palabra clave static indica que un atributo o método pertenece a la clase y no a una instancia concreta. Por eso main es static: se puede ejecutar sin crear objetos. static se puede usar en cualquier método o atributo de clase, no solo en main.

La combinación con final indica que la variable o referencia no puede cambiar su valor después de inicializarse. Por ejemplo, static final double PI = 3.1416; define una constante de clase.

## 10. Intenta ejecutar un poco de Java de forma básica, con los comandos `javac` y `java`. ¿Cómo podemos compilar el programa y ejecutarlo desde linea de comandos? ¿Java es compilado? ¿Qué es la **máquina virtual**? ¿Qué es el *byte-code* y los ficheros `.class`?

Respuesta

Java es un lenguaje compilado, pero no se ejecuta directamente en la CPU. Primero se compila con javac NombreArchivo.java, lo que genera un archivo .class que contiene byte-code, un código intermedio independiente de la plataforma.

Luego, se ejecuta con el comando java NombreArchivo, que interpreta el byte-code en la Java Virtual Machine (JVM). La JVM es un programa que simula una máquina real y permite que el mismo byte-code se ejecute en distintos sistemas operativos.

Los ficheros .class contienen el byte-code generado por el compilador y representan la versión ejecutable de la clase en la JVM.


## 11. En el código anterior de la clase `Punto` ¿Qué es `new`? ¿Qué es un **constructor**? Pon un ejemplo de constructor en una clase `Empleado` que tenga DNI, nombre y apellidos

Respuesta

La palabra clave new se utiliza para crear un nuevo objeto en memoria y devuelve una referencia a él. Al crear un objeto con new, se invoca automáticamente un constructor, que es un método especial de la clase que inicializa los atributos del objeto.

class Empleado {
    String dni;
    String nombre;
    String apellidos;

    Empleado(String dni, String nombre, String apellidos) {
        this.dni = dni;
        this.nombre = nombre;
        this.apellidos = apellidos;
    }
}

Aquí, al hacer Empleado e = new Empleado("1234X", "Juan", "Pérez");, se crea un objeto Empleado inicializando sus atributos.


## 12. ¿Qué es la referencia `this`? ¿Se llama igual en todos los lenguajes? Pon un ejemplo del uso de `this` en la clase `Punto`

Respuesta

La referencia this apunta al propio objeto que está ejecutando un método. Se utiliza para diferenciar atributos de parámetros locales cuando tienen el mismo nombre.

No todos los lenguajes usan el mismo nombre. Por ejemplo, en Python se utiliza self.

Ejemplo en Punto:
class Punto {
    double x, y;

    Punto(double x, double y) {
        this.x = x; // this.x es el atributo, x es el parámetro
        this.y = y;
    }
}



## 13. Añade ahora otro nuevo método que se llame `distanciaA`, que reciba un `Punto` como parámetro y calcule la distancia entre `this` y el punto proporcionado

double distanciaA(Punto p) {
    double dx = this.x - p.x;
    double dy = this.y - p.y;
    return Math.sqrt(dx*dx + dy*dy);
}

Este método calcula la distancia entre el objeto actual (this) y otro objeto Punto pasado como parámetro.


## 14. El paso del `Punto` como parámetro a un método, es **por copia** o **por referencia**, es decir, si se cambia el valor de algún atributo del punto pasado como parámetro, dichos cambios afectan al objeto fuera del método? ¿Qué ocurre si en vez de un `Punto`, se recibiese un entero (`int`) y dicho entero se modificase dentro de la función? 

Respuesta

En Java, los objetos se pasan por referencia a nivel de la referencia. Esto significa que si se modifica un atributo del objeto pasado como parámetro, esos cambios afectan al objeto original.

En cambio, los tipos primitivos, como int, se pasan por valor, por lo que cualquier cambio dentro del método no afecta al valor original fuera del método.


## 15. ¿Qué es el método `toString()` en Java? ¿Existe en otros lenguajes? Pon un ejemplo de `toString()` en la clase `Punto` en Java

Respuesta

El método toString() devuelve una representación en texto del objeto, útil para imprimirlo o depurarlo. Es un método de la clase base Object que todas las clases heredan.

Otros lenguajes orientados a objetos también tienen métodos similares, por ejemplo __str__() en Python o toString() en C#.

Ejemplo en Punto:
@Override
public String toString() {
    return "(" + x + ", " + y + ")";
}

Luego, System.out.println(p); imprime (3.0, 4.0) si p.x = 3 y p.y = 4.


## 16. Reflexiona: ¿una clase es como un `struct` en C? ¿Qué le falta al `struct` para ser como una clase y las variables de ese tipo ser instancias?


Respuesta

Un struct en C es similar a una clase en que puede almacenar varios datos bajo un mismo nombre, pero no puede contener métodos ni control de acceso a los datos.

Para que un struct se comporte como una clase, necesitaría poder definir funciones dentro de él, soportar constructores, y permitir herencia y encapsulamiento, de modo que cada variable de ese tipo sea una instancia con su propio estado y comportamiento asociado.


## 17. Quitemos un poco de magia a todo esto: ¿Como se podría “emular”, con `struct` en C, la clase `Punto`, con su función para calcular la distancia al origen? ¿Qué ha pasado con `this`?

Respuesta

En C se podría emular la clase Punto usando un struct y una función externa:

#include <stdio.h>
#include <math.h>

typedef struct {
    double x;
    double y;
} Punto;

double calculaDistanciaAOrigen(Punto *p) {
    return sqrt(p->x*p->x + p->y*p->y);
}

int main() {
    Punto p = {3, 4};
    printf("%f\n", calculaDistanciaAOrigen(&p));
    return 0;
}

Aquí, el parámetro Punto *p actúa como this en Java, ya que la función necesita la dirección del struct para acceder a sus atributos. En C no existe una referencia automática como this; debe pasarse explícitamente.
