<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Encapsulación". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# TEMA 2. Encapsulación

## 1. En Programación Orientada a Objetos (POO), ¿Qué buscan la **encapsulación** y **la ocultación** de información? Enumera brevemente algunas ventajas de la ocultación de información.

Respuesta

En Programación Orientada a Objetos, la encapsulación y la ocultación de información buscan separar claramente lo que un objeto hace de cómo lo hace internamente. Es decir, se pretende que desde el exterior solo se pueda acceder a los datos y comportamientos que la clase decide exponer, mientras que los detalles internos de implementación permanecen protegidos. De esta manera, el objeto controla su propio estado y evita modificaciones directas no deseadas.

La encapsulación agrupa datos (atributos) y funciones (métodos) dentro de una misma unidad, la clase. La ocultación de información, por su parte, limita el acceso directo a los atributos internos, obligando a interactuar con el objeto a través de métodos definidos para ello. Esto impide que otras partes del programa modifiquen el estado del objeto de forma incorrecta o inconsistente.

Algunas ventajas de la ocultación de información son:

1. Mayor seguridad y control, ya que se evita que el estado interno sea modificado arbitrariamente.

2. Menor acoplamiento, porque otras partes del programa no dependen de los detalles internos de la clase.

3. Facilidad de mantenimiento, dado que se pueden cambiar detalles internos sin afectar al código externo.

4. Mayor claridad y organización, al obligar a definir una interfaz clara para interactuar con el objeto.


## 2. ¿Qué se entiende por la **interfaz pública** de un objeto o clase en POO? Describe brevemente cómo se relaciona con la ocultación de información.

Respuesta

La interfaz pública de una clase en Programación Orientada a Objetos es el conjunto de métodos y atributos que pueden ser utilizados desde fuera de la clase. Es decir, define qué operaciones están disponibles para que otros objetos o partes del programa interactúen con ella. En lenguajes como Java, esta interfaz pública está formada principalmente por los métodos declarados con el modificador public.

La interfaz pública actúa como un contrato: especifica qué se puede hacer con un objeto, pero no explica cómo está implementado internamente. Desde el exterior solo se conocen los nombres de los métodos, sus parámetros y qué tipo de valor devuelven, pero no los detalles internos del código ni cómo se gestionan los datos dentro de la clase.

Esta idea está directamente relacionada con la ocultación de información, ya que los detalles internos (atributos privados, métodos auxiliares, estructuras internas) permanecen ocultos. De este modo, se protege el estado interno del objeto y se permite modificar la implementación interna sin afectar al código que utiliza la clase, siempre que la interfaz pública se mantenga estable.


## 3. Brevemente: ¿Por qué hay que ser conscientes y diseñar con cuidado la **interfaz pública** de una clase? ¿Es fácil cambiarla?

Respuesta

La interfaz pública de una clase debe diseñarse con cuidado porque representa el punto de contacto entre esa clase y el resto del programa. Una vez que otros módulos comienzan a utilizar sus métodos públicos, estos pasan a formar parte de un contrato implícito. Si la interfaz no está bien pensada, puede exponer más información de la necesaria o permitir usos incorrectos del objeto, generando dependencias innecesarias y aumentando el riesgo de errores.


## 4. ¿Qué son las **invariantes de clase** y por qué la ocultación de información nos ayuda?

Respuesta

Las invariantes de clase son condiciones o reglas que siempre deben cumplirse para que un objeto se considere válido durante toda su existencia. Por ejemplo, en una clase CuentaBancaria, una invariante podría ser que el saldo nunca sea negativo. Estas condiciones definen el estado correcto del objeto y ayudan a garantizar la coherencia y fiabilidad del sistema.

La ocultación de información contribuye directamente a mantener estas invariantes, porque impide que otras partes del programa modifiquen los atributos internos de manera directa e inapropiada. Al acceder a los datos únicamente a través de métodos controlados (getters, setters o funciones especializadas), la clase puede validar los cambios y asegurarse de que no se rompen las reglas internas.

De esta manera, la combinación de invariantes y ocultación de información proporciona seguridad y consistencia, permitiendo que los objetos mantengan un estado válido incluso cuando interactúan con otras partes del programa. Esto reduce errores y facilita el mantenimiento y la extensión de la clase.


## 5. Pon un ejemplo de una clase `Punto` en `Java`, con dos coordenadas, `x` e `y`, de tipo `double`, con un método `calcularDistanciaAOrigen`, y que haga uso de la ocultación de información. ¿Cuál es la interfaz pública de la clase `Punto`? ¿Qué significa `public` y `private`?

Respuesta

En Java, se puede crear una clase Punto usando ocultación de información declarando los atributos como private y proporcionando métodos públicos para interactuar con ellos. Esto garantiza que el estado interno del objeto no pueda modificarse directamente desde fuera, protegiendo invariantes o reglas de la clase.

Ejemplo:
class Punto {
    private double x;
    private double y;

    // Constructor
    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    // Métodos de acceso (getters)
    public double getX() {
        return x;
    }

    public double getY() {
        return y;
    }

    // Método público que calcula la distancia al origen
    public double calcularDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }
}



## 6. En Java, ¿A quiénes se pueden aplicar los modificadores `public` o `private`?

Respuesta

En Java, los modificadores de acceso public y private se pueden aplicar principalmente a atributos, métodos y constructores dentro de una clase. Al declararlos, se controla quién puede ver o usar esos elementos desde fuera de la clase. Por ejemplo, un atributo private solo puede ser accedido desde métodos de la misma clase, mientras que un método public puede ser invocado desde cualquier otra clase.

Además, se pueden aplicar a clases en ciertos casos. Una clase puede ser public, lo que significa que puede ser utilizada desde cualquier otro paquete. Sin embargo, una clase no puede ser private a nivel de paquete, salvo que sea una clase interna definida dentro de otra clase.

Por lo tanto, los modificadores de acceso permiten controlar la visibilidad de los elementos de una clase, protegiendo datos y asegurando que se utilicen solo a través de la interfaz pública diseñada por el programador. Esto refuerza la encapsulación y mantiene la coherencia del objeto.


## 7. En POO, la visibilidad puede ser pública o privada, pero ¿existen más tipos de visibilidad? ¿Qué ocurre en Java? ¿Y en otros lenguajes?

Respuesta

Sí, en Programación Orientada a Objetos existen más tipos de visibilidad además de public y private. En Java, además de estos dos, existen protected y la visibilidad por defecto (también llamada package-private).

Protected permite que el atributo o método sea accesible dentro de la misma clase, en sus subclases (incluso en otros paquetes si se hereda) y dentro del mismo paquete.
Visibilidad por defecto (sin modificador explícito) hace que el elemento sea accesible únicamente dentro del mismo paquete.

En otros lenguajes orientados a objetos, la visibilidad puede variar:
En C++, existen public, private y protected, con reglas muy similares a Java. Además, C++ permite especificar visibilidad distinta para secciones completas de la clase, no solo por miembro.
En Python, no hay modificadores estrictos. Se usa una convención de nombres (_atributo para “protegido” y __atributo para “privado”), pero el acceso se puede forzar.
Otros lenguajes como C# incluyen más niveles, como internal (solo accesible dentro del ensamblado) o protected internal.

En general, estos mecanismos permiten controlar qué partes del código pueden interactuar con cada elemento, fortaleciendo la encapsulación y evitando modificaciones indebidas del estado interno de los objetos.


## 8. Responde: Los miembros de instancia privados de un objeto están ocultos para (a) otras clases o (b) otras instancias, aunque sean de la misma clase. Pon un ejemplo añadiendo un método `calcularDistanciaAPunto(Punto otro)` y explica la respuesta.

En Java, los miembros de instancia privados de un objeto están ocultos para otras clases, pero no para otras instancias de la misma clase. Esto significa que dentro de los métodos de la propia clase se puede acceder a los atributos privados de cualquier objeto de esa misma clase, aunque sea un objeto distinto del que invoca el método.

Por ejemplo, podemos añadir un método calcularDistanciaAPunto(Punto otro) a la clase Punto:
class Punto {
    private double x;
    private double y;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    public double calcularDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }

    // Nuevo método
    public double calcularDistanciaAPunto(Punto otro) {
        // Accede directamente a los atributos privados de 'otro'
        double dx = this.x - otro.x;
        double dy = this.y - otro.y;
        return Math.sqrt(dx * dx + dy * dy);
    }
}


## 9. ¿Qué son los métodos "getter" y "setter" en los lenguajes orientados a objetos?

Respuesta

En los lenguajes orientados a objetos, los métodos getter y setter son funciones que permiten acceder y modificar atributos privados de un objeto de forma controlada. Los getters devuelven el valor de un atributo, mientras que los setters permiten asignar un nuevo valor, generalmente realizando comprobaciones o validaciones antes de modificarlo.

Este mecanismo refuerza la encapsulación, ya que los atributos permanecen privados y solo se puede interactuar con ellos a través de métodos que respetan las reglas de la clase. Por ejemplo, en una clase Punto, un setter podría impedir asignar valores inválidos a las coordenadas, manteniendo la coherencia del objeto.

## 10. Cuando nos referimos a que la ocultación de información mejora la "seguridad" del programa, ¿nos referimos a que no pueda ser "hackeado"?

Respuesta

No, cuando se dice que la ocultación de información mejora la seguridad del programa en POO, no se refiere a protección frente a ataques externos o “hackeos”. Se trata de seguridad a nivel de programación, es decir, garantizar que los datos internos de un objeto solo puedan modificarse de la manera prevista por su clase.

Al mantener los atributos privados y controlar su acceso mediante métodos públicos (getters y setters), se evita que otras partes del código cambien valores de forma incorrecta o inconsistente. Esto protege las invariantes de clase y asegura que los objetos siempre estén en un estado válido, evitando errores lógicos y fallos inesperados en el programa.

En otras palabras, la “seguridad” aquí es integridad y consistencia de los datos, no seguridad frente a ataques externos. Esto permite que el software sea más fiable y fácil de mantener, y reduce la probabilidad de errores causados por modificaciones indebidas de los atributos internos de los objetos.


## 11. ¿Qué diferencia hay entre **miembro de instancia** y **miembro de clase**? ¿Los miembros de clase también se pueden ocultar?

Respuesta

Un miembro de instancia es un atributo o método que pertenece a cada objeto individual de una clase. Cada instancia mantiene su propio valor de esos atributos, y los métodos de instancia actúan sobre los datos de ese objeto concreto. Por ejemplo, en una clase Punto, x e y serían miembros de instancia: cada objeto Punto tiene sus propias coordenadas.

En cambio, un miembro de clase (también llamado estático, declarado con static en Java) pertenece a la clase en sí, no a sus objetos. Esto significa que todos los objetos de la clase comparten el mismo valor de ese miembro. Por ejemplo, un contador de cuántos objetos Punto se han creado podría ser un miembro de clase.

Sí, los miembros de clase también se pueden ocultar usando modificadores de acceso como private. Un atributo o método estático private solo puede ser accedido dentro de la propia clase, y su visibilidad fuera de la clase está controlada por la interfaz pública de la clase, igual que ocurre con los miembros de instancia. Esto permite proteger datos compartidos y controlar cómo se accede a ellos.


## 12. Brevemente: ¿Tiene sentido que los constructores sean privados?

Respuesta

Sí, en ciertos casos tiene sentido que los constructores sean privados. Esto se utiliza principalmente para controlar la creación de objetos y evitar que se instancien directamente desde fuera de la clase. Por ejemplo, se aplica en clases de utilidades que no necesitan instancias, o en patrones de diseño como el Singleton, donde se quiere garantizar que solo exista un objeto de esa clase.

Cuando un constructor es privado, la clase puede proporcionar métodos públicos que creen y devuelvan instancias de forma controlada, asegurando que se cumplan invariantes o restricciones específicas. Esto refuerza la ocultación de información y el control del estado interno, evitando usos incorrectos del objeto.


## 13. ¿Cómo se indican los **miembros de clase** en Java? Pon un ejemplo, en la clase `Punto` definida anteriormente, para que incluya miembros de clase que permitan saber cuáles son los valores `x` e `y` máximos que se han establecido en todos los puntos que se hayan creado hasta el momento.

Respuesta

En Java, los miembros de clase se indican con la palabra clave static. Esto aplica tanto a atributos como a métodos, y significa que pertenecen a la clase en sí, no a cada objeto individual. Todos los objetos de la clase comparten estos miembros y pueden acceder a ellos mediante Clase.miembro o desde métodos estáticos de la propia clase.

En el ejemplo de la clase Punto, se puede añadir un atributo estático para registrar los valores máximos de x e y que se hayan asignado a cualquier punto creado:
class Punto {
    private double x;
    private double y;

    // Miembros de clase (estáticos)
    private static double maxX = Double.NEGATIVE_INFINITY;
    private static double maxY = Double.NEGATIVE_INFINITY;

    // Constructor
    public Punto(double x, double y) {
        this.x = x;
        this.y = y;

        // Actualizar los valores máximos de clase
        if (x > maxX) {
            maxX = x;
        }
        if (y > maxY) {
            maxY = y;
        }
    }

    public double calcularDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }

    // Métodos para acceder a los máximos
    public static double getMaxX() {
        return maxX;
    }

    public static double getMaxY() {
        return maxY;
    }
}



## 14. Como sería un método factoría dentro de la clase `Punto` para construir un `Punto` a partir de dos coordenadas, pero que las redondee al entero más cercano. Escribe sólo el código del método, no toda la clase ¿Has usado `static`? 

Sí, un método factoría normalmente se declara como static, porque se invoca desde la clase, no desde un objeto existente, y devuelve un nuevo objeto Punto.

Ejemplo de método factoría que redondea las coordenadas al entero más cercano:
public static Punto crearPuntoRedondeado(double x, double y) {
    int xRedondeado = (int) Math.round(x);
    int yRedondeado = (int) Math.round(y);
    return new Punto(xRedondeado, yRedondeado);
}

Sí, se ha usado static porque no necesitamos un Punto previo para crear uno nuevo.

El método devuelve un nuevo objeto Punto con las coordenadas redondeadas.

Se puede llamar así: Punto p = Punto.crearPuntoRedondeado(3.7, 4.2);


## 15. Cambia la implementación de `Punto`. En vez de dos `double`, emplea un array interno de dos posiciones, intentando no modificar la interfaz pública de la clase.

class Punto {
    // Array interno para guardar x e y
    private double[] coords = new double[2];

    // Miembros de clase para máximos
    private static double maxX = Double.NEGATIVE_INFINITY;
    private static double maxY = Double.NEGATIVE_INFINITY;

    // Constructor
    public Punto(double x, double y) {
        coords[0] = x;
        coords[1] = y;

        // Actualizar máximos
        if (x > maxX) maxX = x;
        if (y > maxY) maxY = y;
    }

    // Getters
    public double getX() {
        return coords[0];
    }

    public double getY() {
        return coords[1];
    }

    // Setters
    public void setX(double x) {
        coords[0] = x;
        if (x > maxX) maxX = x;
    }

    public void setY(double y) {
        coords[1] = y;
        if (y > maxY) maxY = y;
    }

    // Distancia al origen
    public double calcularDistanciaAOrigen() {
        return Math.sqrt(coords[0] * coords[0] + coords[1] * coords[1]);
    }

    // Distancia a otro punto
    public double calcularDistanciaAPunto(Punto otro) {
        double dx = this.coords[0] - otro.coords[0];
        double dy = this.coords[1] - otro.coords[1];
        return Math.sqrt(dx * dx + dy * dy);
    }

    // Métodos de clase para máximos
    public static double getMaxX() { return maxX; }
    public static double getMaxY() { return maxY; }

    // Método factoría para redondear coordenadas
    public static Punto crearPuntoRedondeado(double x, double y) {
        int xRedondeado = (int) Math.round(x);
        int yRedondeado = (int) Math.round(y);
        return new Punto(xRedondeado, yRedondeado);
    }
}

Los atributos x e y ya no existen separados; se usan coords[0] y coords[1].

La interfaz pública no cambia: los métodos getX(), getY(), setX(), setY(), calcularDistanciaAOrigen() y calcularDistanciaAPunto() siguen funcionando igual.

Los métodos de clase getMaxX() y getMaxY() también funcionan igual que antes.

Se mantiene el método factoría crearPuntoRedondeado y sigue siendo static.

De este modo, los usuarios de la clase no se enteran de que ahora usamos un array, cumpliendo con la idea de encapsulación.


## 16. Si un atributo va a tener un método "getter" y "setter" públicos, ¿no es mejor declararlo público? ¿Cuál es la convención más habitual sobre los atributos, que sean públicos o privados? ¿Tiene esto algo que ver con las "invariantes de clase"?

Respuesta

Aunque un atributo tenga getter y setter públicos, no es recomendable declararlo público. La razón es que los métodos permiten controlar el acceso al atributo, realizar validaciones y proteger invariantes de la clase, mientras que un atributo público se podría modificar directamente desde cualquier parte del programa sin restricciones.

La convención más habitual en Java y otros lenguajes orientados a objetos es declarar los atributos como private y proporcionar métodos públicos para acceder y modificar sus valores cuando sea necesario. Esto garantiza que los objetos mantengan un estado consistente y que cualquier cambio pase por la lógica de la clase, evitando errores.

Esto tiene relación directa con las invariantes de clase, porque estas invariantes son condiciones que deben cumplirse siempre para que un objeto sea válido. Al mantener los atributos privados y controlarlos mediante getters y setters, se asegura que no se rompan estas invariantes al modificar los datos del objeto, protegiendo así la integridad y coherencia de la clase.


## 17. ¿Qué significa que una clase sea **inmutable**? ¿qué es un método modificador? ¿Un método modificador es siempre un "setter"? ¿Tiene ventajas que una clase sea inmutable?

Respuesta

Una clase se considera inmutable cuando sus objetos no pueden cambiar su estado después de haber sido creados. Es decir, una vez que se asignan los valores a sus atributos mediante el constructor, no se pueden modificar. Para lograr esto, todos los atributos suelen declararse como private y final, y no se proporcionan métodos que alteren directamente sus valores.

Un método modificador es cualquier método que cambia el estado interno de un objeto, es decir, que altera alguno de sus atributos. No todos los métodos modificadores son setters, aunque los setters son el ejemplo más común. También pueden ser métodos que cambien varios atributos a la vez, calculen un nuevo estado o transformen el objeto de alguna manera.

Las clases inmutables tienen varias ventajas:

-Seguridad y consistencia: los objetos no pueden modificarse de forma accidental, lo que reduce errores.

-Facilidad para compartir y reutilizar: se pueden pasar referencias a los objetos sin riesgo de que otro código los modifique.

-Simplificación en concurrencia: en programas multihilo no es necesario sincronizar el acceso a objetos inmutables, porque su estado nunca cambia.

En resumen, la inmutabilidad refuerza la integridad de los objetos, y los métodos modificadores son los que romperían esta inmutabilidad si existieran en la clase.


## 18. ¿Es recomendable incluir métodos "setter" siempre y como convención?

Respuesta

No, no es recomendable incluir métodos setter siempre por defecto. La decisión depende del diseño de la clase y de las invariantes que se quieran mantener. Incluir un setter innecesario puede permitir que cualquier código externo modifique atributos de manera que rompa la coherencia del objeto.

La convención habitual es declarar los atributos como private y crear setters solo cuando realmente se necesita modificar el valor de un atributo desde fuera de la clase. Si un atributo no debe cambiar después de la creación del objeto, lo mejor es no proporcionar setter y mantenerlo inmutable, reforzando la seguridad y la consistencia de la clase.

En otras palabras, los setters son herramientas útiles, pero su uso debe ser selectivo y justificado, no automático. Esto también está relacionado con las invariantes de clase, ya que cada setter debería asegurar que estas invariantes se mantienen al modificar el estado del objeto.


## 19. ¿La clase `String` en Java es mutable o inmutable? ¿Qué ocurre al concatenar dos cadenas? ¿Qué debemos hacer si vamos a hacer una operación que implique concatenar muchas veces para construir paso a paso una cadena muy larga?

Respuesta

En Java, la clase String es inmutable, lo que significa que una vez creado un objeto String, su contenido no puede cambiar. Cada operación que parece modificar la cadena, como la concatenación, en realidad crea un nuevo objeto String con el resultado, dejando intacto el original. Por ejemplo:

String a = "Hola";
String b = a + " Mundo"; // se crea un nuevo objeto, 'a' sigue siendo "Hola"

Esto tiene implicaciones importantes: si se concatenan muchas cadenas dentro de un bucle, cada concatenación genera un nuevo objeto, lo que puede ser muy ineficiente en memoria y tiempo de ejecución.

Para operaciones que impliquen construir una cadena larga paso a paso, se recomienda usar StringBuilder o StringBuffer. Estas clases son mutables, permiten añadir, insertar o modificar caracteres sin crear un nuevo objeto en cada operación, y luego se puede convertir a String al final usando toString(). Ejemplo:

StringBuilder sb = new StringBuilder();
for (int i = 0; i < 1000; i++) {
    sb.append("Texto ");
}
String resultado = sb.toString();



## 20. En POO ¿Cómo se comparan objetos de una misma clase? ¿Por su contenido o por su identidad? ¿Qué es el método equals en Java? ¿Qué hace por defecto? ¿Cómo se deben comparar dos cadenas en Java? 

Respuesta

En Programación Orientada a Objetos, los objetos de una misma clase pueden compararse por su identidad o por su contenido, dependiendo de la intención del programa. Por identidad se entiende si dos variables apuntan al mismo objeto en memoria, mientras que por contenido se compara si los atributos o estado interno de los objetos son equivalentes.

En Java, el método equals() se utiliza para comparar objetos por contenido. Por defecto, el método equals() heredado de la clase Object compara la identidad, es decir, devuelve true solo si ambas referencias apuntan al mismo objeto en memoria. Para que equals() compare el contenido real de un objeto, normalmente se debe sobrescribir (override) en la clase correspondiente, definiendo qué atributos deben considerarse para la igualdad.

En el caso de las cadenas de texto (String), no se debe usar ==, porque esto compara identidad y no el contenido. En su lugar, se usa:

String s1 = "hola";
String s2 = new String("hola");

if (s1.equals(s2)) {
    System.out.println("Son iguales por contenido");
}


Aquí, equals() devuelve true porque compara los caracteres dentro de la cadena, no las referencias. Esta es la forma correcta de comparar cadenas en Java para asegurar que se evalúa el contenido y no simplemente si son el mismo objeto.


## 21. ¿Qué son las clases "wrapper" en un lenguaje de programación orientado a objetos? ¿Cómo se hace? ¿Es un proceso automático? ¿Qué ventajas tienen? ¿Todos los lenguajes orientados a objetos tienen tipos primitivos y necesitan wrappers? 

Respuesta

En los lenguajes orientados a objetos, las clases “wrapper” son clases que envuelven tipos primitivos para poder tratarlos como objetos. Por ejemplo, en Java, los tipos primitivos como int, double o boolean no son objetos, pero existen clases wrapper como Integer, Double o Boolean que permiten usarlos en contextos donde se requieren objetos, como colecciones (ArrayList, HashMap, etc.).

En Java, la conversión entre un tipo primitivo y su wrapper puede hacerse de forma manual o de manera automática mediante autoboxing/unboxing.

Las ventajas de los wrappers son:

-Permiten usar tipos primitivos en estructuras de datos que solo aceptan objetos.

-Proporcionan métodos útiles para conversión, comparación o manipulación de valores (por ejemplo, Integer.parseInt() o Double.toString()).

-Facilitan la interoperabilidad con APIs que requieren objetos y no primitivos.

No todos los lenguajes orientados a objetos necesitan wrappers: algunos lenguajes, como Python, tratan todos los valores como objetos desde el inicio, por lo que no existe distinción entre primitivo y objeto. En otros, como Java o C#, los tipos primitivos existen y los wrappers son necesarios para aprovechar las ventajas de la POO en ciertos contextos.


## 22. ¿En POO qué es un **tipo de dato enumerado**? ¿En Java, un tipo de dato enumerado es una clase? ¿Qué ventajas tienen en términos de encapsulación los enumerados en Java?

Respuesta

Un tipo de dato enumerado (o enum) en Programación Orientada a Objetos es un tipo especial que define un conjunto limitado y fijo de valores posibles. Se utiliza cuando una variable solo puede tomar ciertos valores predefinidos, como los días de la semana, los meses del año o los estados de un proceso. Esto ayuda a evitar errores al restringir las asignaciones a valores válidos.

En Java, un tipo enumerado es en realidad una clase especial. Cada valor definido en el enum se trata como un objeto inmutable de esa clase. Por ejemplo:

enum Dia {
    LUNES, MARTES, MIERCOLES, JUEVES, VIERNES
}


Aquí, LUNES, MARTES, etc., son instancias de la clase Dia.

Los enumerados en Java tienen ventajas de encapsulación, porque los valores posibles están ocultos y controlados dentro del enum. No se puede crear un valor “inventado” fuera del conjunto definido, y cada objeto enum puede tener métodos y atributos propios, pero su estado permanece consistente y seguro. Esto permite que las variables que usan el enum solo puedan contener valores válidos, reforzando la coherencia y la integridad del programa.


## 23. Crea un tipo enumerado en Java que se llame `Mes`, con doce posibles instancias y que además proporcione métodos para obtener cuántos días tiene ese mes, el ordinal de ese mes en el año (1-12), empleando atributos privados y constructores del tipo enumerado.

Respuesta

En Java, un enum puede tener atributos privados, constructores y métodos, manteniendo la ocultación de información y controlando el estado de cada instancia. Aquí tienes un ejemplo completo del enum Mes:

public enum Mes {
    ENERO(31),
    FEBRERO(28),
    MARZO(31),
    ABRIL(30),
    MAYO(31),
    JUNIO(30),
    JULIO(31),
    AGOSTO(31),
    SEPTIEMBRE(30),
    OCTUBRE(31),
    NOVIEMBRE(30),
    DICIEMBRE(31);

    // Atributos privados
    private final int dias;

    // Constructor privado del enum
    private Mes(int dias) {
        this.dias = dias;
    }

    // Método público para obtener los días del mes
    public int getDias() {
        return dias;
    }

    // Método público para obtener el ordinal (1-12)
    public int getOrdinal() {
        return this.ordinal() + 1; // ordinal() empieza en 0
    }
}

 Explicación

Cada valor (ENERO, FEBRERO, etc.) es una instancia inmutable del enum Mes.

El atributo dias es privado, lo que protege la información interna.

El constructor del enum también es privado, asegurando que no se puedan crear más instancias fuera de las definidas.

Los métodos getDias() y getOrdinal() constituyen la interfaz pública, permitiendo acceder a la información de forma controlada.

Así, los enums en Java combinan tipos limitados, encapsulación y métodos en un único objeto seguro y coherente.


## 24. Añade a la clase `Mes` del ejercicio anterior cuatro métodos para devolver si ese mes tiene algunos días de invierno, primavera, verano u otoño, indicando con un booleano el hemisferio (norte o sur, parámetro `enHemisferioNorte`). Es decir: `esDePrimavera(boolean esHemisferioNorte)`, `esDeVerano(boolean esHemisferioNorte)`, `esDeOtoño(boolean esHemisferioNorte)`, `esDeInvierno(boolean esHemisferioNorte)`

Respuesta

Mantendremos los atributos privados y la interfaz pública, agregando cuatro métodos booleanos que reciben un parámetro enHemisferioNorte.

public enum Mes {
    ENERO(31),
    FEBRERO(28),
    MARZO(31),
    ABRIL(30),
    MAYO(31),
    JUNIO(30),
    JULIO(31),
    AGOSTO(31),
    SEPTIEMBRE(30),
    OCTUBRE(31),
    NOVIEMBRE(30),
    DICIEMBRE(31);

    private final int dias;

    private Mes(int dias) {
        this.dias = dias;
    }

    public int getDias() {
        return dias;
    }

    public int getOrdinal() {
        return this.ordinal() + 1;
    }

    // Métodos para determinar la estación según hemisferio
    public boolean esDePrimavera(boolean enHemisferioNorte) {
        if (enHemisferioNorte) {
            return this == MARZO || this == ABRIL || this == MAYO;
        } else {
            return this == SEPTIEMBRE || this == OCTUBRE || this == NOVIEMBRE;
        }
    }

    public boolean esDeVerano(boolean enHemisferioNorte) {
        if (enHemisferioNorte) {
            return this == JUNIO || this == JULIO || this == AGOSTO;
        } else {
            return this == DICIEMBRE || this == ENERO || this == FEBRERO;
        }
    }

    public boolean esDeOtoño(boolean enHemisferioNorte) {
        if (enHemisferioNorte) {
            return this == SEPTIEMBRE || this == OCTUBRE || this == NOVIEMBRE;
        } else {
            return this == MARZO || this == ABRIL || this == MAYO;
        }
    }

    public boolean esDeInvierno(boolean enHemisferioNorte) {
        if (enHemisferioNorte) {
            return this == DICIEMBRE || this == ENERO || this == FEBRERO;
        } else {
            return this == JUNIO || this == JULIO || this == AGOSTO;
        }
    }
}

 Explicación

Cada método recibe un parámetro enHemisferioNorte para ajustar las estaciones según el hemisferio.

Se compara this con los meses correspondientes para cada estación.

Se mantiene la encapsulación, ya que la lógica interna de la estación está dentro del enum y el usuario solo obtiene un boolean al consultarlo.

La interfaz pública se amplía sin exponer los detalles internos de los meses ni sus días.
