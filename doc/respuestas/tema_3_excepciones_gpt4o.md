<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Excepciones". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos, Encapsulación.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# TEMA 3. Excepciones

## 1. Empecemos un tema sobre control de errores en lenguajes de programación, con algo básico. En C, donde no existen las excepciones, pongamos un ejemplo de una raíz que toma número flotante positivo. Queremos controlar el error si la función recibe un número negativo. El usuario debe ser informado pero desde fuera de la función `raiz` ¿Cómo indicamos ese error?. Enumera dos opciones diferentes de diseñar, poniendo un ejemplo de código de cada una.

### Respuesta
En C no existen excepciones como mecanismo del lenguaje, por lo que el control de errores debe diseñarse manualmente. En el caso de una función raiz que recibe un número flotante y solo acepta valores positivos, el error (recibir un número negativo) debe indicarse mediante algún mecanismo alternativo. Es importante que la función no imprima el error directamente si se desea que el control se realice desde fuera, ya que eso separa la lógica de cálculo de la lógica de presentación.

Una primera opción consiste en devolver un valor especial que indique error. Por ejemplo, se puede devolver -1 o NAN (Not A Number), y que el código que llama a la función compruebe ese valor antes de usar el resultado.

#include <stdio.h>
#include <math.h>

double raiz(double x) {
    if (x < 0) {
        return -1;  // valor especial indicando error
    }
    return sqrt(x);
}

int main() {
    double r = raiz(-4);
    if (r == -1) {
        printf("Error: número negativo\n");
    } else {
        printf("Resultado: %f\n", r);
    }
    return 0;
}

Una segunda opción consiste en devolver un código de error separado del resultado, por ejemplo usando un puntero para almacenar el resultado y devolviendo un entero que indique éxito o fallo. Este diseño es más robusto, porque no depende de valores especiales que puedan confundirse con resultados válidos.

#include <stdio.h>
#include <math.h>

int raiz(double x, double *resultado) {
    if (x < 0) {
        return 0;  // 0 indica error
    }
    *resultado = sqrt(x);
    return 1;  // 1 indica éxito
}

int main() {
    double resultado;
    if (!raiz(-4, &resultado)) {
        printf("Error: número negativo\n");
    } else {
        printf("Resultado: %f\n", resultado);
    }
    return 0;
}

En ambos casos el error se detecta dentro de la función, pero la decisión de informar al usuario se toma desde fuera, lo que permite separar responsabilidades. Sin embargo, este tipo de diseño obliga a comprobar manualmente los errores después de cada llamada, lo que puede complicar el código en programas grandes.


## 2. Brevemente ¿Qué es una **"excepción"**? ¿Con qué objetivo las usa un programador cuando implementa funciones o cuando las llama?

### Respuesta
Una excepción es un mecanismo del lenguaje que permite señalar que se ha producido una situación anómala o un error durante la ejecución de un programa. En lugar de devolver un valor especial o un código de error, como ocurre en C, el propio lenguaje permite “interrumpir” el flujo normal de ejecución cuando se detecta un problema, transfiriendo el control a otro lugar preparado para manejarlo.

El objetivo de las excepciones es separar el código normal del código de tratamiento de errores. Cuando un programador implementa una función, puede lanzar una excepción si detecta que no se cumplen ciertas condiciones (por ejemplo, recibir un número negativo al calcular una raíz cuadrada). Cuando otro programador llama a esa función, puede decidir capturar esa excepción y actuar en consecuencia, como mostrar un mensaje o intentar una solución alternativa.

De esta forma, se evita mezclar continuamente comprobaciones de error con la lógica principal del programa. Esto hace que el código sea más claro y estructurado, especialmente en programas grandes donde los errores pueden producirse en distintos niveles de llamadas.


## 3. Reescribe el mismo ejemplo de raiz, pero en Java, metiendo ese método en una clase `Calculadora` y llama a dicho método desde el método `main`, mostrando cómo se puede controlar desde fuera.

### Respuesta
En Java, el control de errores puede realizarse mediante excepciones. En el ejemplo de la raíz cuadrada, si se recibe un número negativo, el método puede lanzar una excepción en lugar de devolver un valor especial. De esta forma, el error se detecta dentro del método, pero se controla desde fuera, por ejemplo en el método main, utilizando un bloque try-catch.

A continuación se muestra una posible implementación con una clase Calculadora:

class Calculadora {

    public static double raiz(double x) {
        if (x < 0) {
            throw new IllegalArgumentException("No se puede calcular la raíz de un número negaxtivo");
        }
        return Math.sqrt(x);
    }

    public static void main(String[] args) {
        try {
            double resultado = raiz(-4);
            System.out.println("Resultado: " + resultado);
        } catch (IllegalArgumentException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}

En este diseño, el método raiz detecta el error y lanza una excepción, pero no decide cómo se informa al usuario. El método main es el encargado de capturar la excepción y mostrar el mensaje correspondiente. Esto permite separar claramente la lógica de cálculo del tratamiento del error.

A diferencia de C, no es necesario comprobar manualmente el resultado después de cada llamada. Si ocurre un problema, el flujo normal se interrumpe automáticamente y se transfiere al bloque catch, lo que hace que el código sea más limpio y estructurado.


## 4. ¿Qué es **"lanzar"** una excepción? ¿Qué es **"controlar"** o **"capturar"** una excepción? ¿Qué es que se **"propague"** una excepción? ¿Qué le va ocurriendo a las funciones en la pila de llamadas por donde se va propagando la excepción? ¿Las funciones que no la controlan se reanudan después de alguna forma? Explica con el mismo ejemplo anterior en Java de la raíz cuadrada.

### Respuesta
Lanzar una excepción significa crear un objeto excepción y señalar que se ha producido un error mediante la palabra clave throw. En ese momento, el flujo normal del programa se interrumpe y se busca un bloque catch adecuado para manejar esa excepción. Capturar o controlar una excepción consiste en utilizar un bloque try-catch para interceptarla y decidir qué hacer cuando ocurre el error.

Una excepción se propaga cuando el método que la recibe no la captura, sino que deja que continúe subiendo por la pila de llamadas (stack). Esto significa que el sistema va retrocediendo por las funciones que estaban activas en ese momento, buscando un método que tenga un catch apropiado. Si ningún método la captura, el programa termina mostrando un mensaje de error.

Cuando una excepción se va propagando, los métodos por los que pasa se interrumpen inmediatamente. No continúan ejecutando las instrucciones que estaban pendientes después del punto donde ocurrió el error. Es decir, no se reanudan después como si nada hubiera ocurrido. El flujo se corta y se transfiere completamente al manejador de la excepción.

Por ejemplo, si en el método raiz se ejecuta:

throw new IllegalArgumentException("Número negativo");

y el método llamador no lo captura, la excepción subirá hasta main. Si main tiene un bloque try-catch, allí se manejará el error. Los métodos intermedios no continúan ejecutándose después del punto donde se lanzó la excepción; su ejecución termina en ese instante debido a la propagación.


## 5. ¿Qué ventajas tiene frente a C, la **"propagación natural"** de las excepciones a través de la pila (*stack*) de llamadas?

### Respuesta

La propagación natural de las excepciones en Java ofrece ventajas importantes frente al enfoque manual de C. Una de las principales ventajas es que permite centralizar el manejo de errores, evitando que cada función tenga que comprobar valores especiales o códigos de error tras cada llamada. Esto hace que el código sea más claro, mantenible y menos propenso a errores humanos.

Otra ventaja es que las excepciones se propagan automáticamente a través de la pila de llamadas, de manera que cualquier función intermedia que no sepa cómo manejar el error no tiene que escribir código adicional para “pasarlo” a la función superior. Esto evita duplicaciones y facilita que el tratamiento de errores se realice en el lugar más adecuado.

Además, la propagación natural permite separar la lógica principal del programa de la lógica de manejo de errores. La función que detecta el problema no necesita preocuparse por cómo se va a informar al usuario o cómo se va a resolver la situación, lo que refuerza la modularidad y la claridad del código. Esto es especialmente útil en programas complejos con múltiples niveles de funciones y llamadas.


## 6. En orientación a objetos, ¿las excepciones suelen ser objetos? ¿Qué ventajas tiene esto en términos de encapsulación? ¿Podemos entonces crear excepciones personalizadas?

### Respuesta

En la programación orientada a objetos, las excepciones suelen ser objetos de clases específicas que heredan de la clase base Exception o RuntimeException en Java. Esto permite que cada excepción encapsule información sobre el error, como un mensaje descriptivo, la pila de llamadas o incluso la causa original de la excepción, manteniendo así la información organizada y accesible.

El hecho de que las excepciones sean objetos ofrece ventajas de encapsulación, ya que la información del error queda protegida dentro de la instancia de la excepción y solo se expone mediante métodos públicos como getMessage() o getCause(). Esto evita que otras partes del programa accedan o modifiquen directamente los detalles internos de la excepción, garantizando integridad y seguridad en el manejo de errores.

Además, al ser objetos, es posible crear excepciones personalizadas que representen situaciones específicas de la aplicación. Por ejemplo, se podría definir una clase RaizNegativaException para capturar exclusivamente intentos de calcular raíces de números negativos. Esto mejora la claridad del código y permite diseñar un manejo de errores más fino, específico y coherente con la lógica de la aplicación.


## 7. En relación con las ventajas de la encapsulación, comparando el ejemplo en C con Java. ¿Qué **información esencial** lleva cualquier **objeto excepción** que es muy útil tener cuando se llega a un manejador?

### Respuesta

Comparando con C, en Java las excepciones son objetos que llevan información estructurada sobre el error, lo cual es muy útil para los manejadores. La información esencial que contiene cualquier objeto excepción incluye principalmente un mensaje descriptivo (getMessage()), la pila de llamadas donde se produjo el error (getStackTrace()) y, opcionalmente, la causa original si la excepción fue generada a partir de otra (getCause()).

Esta información permite al manejador conocer qué ocurrió, dónde ocurrió y por qué ocurrió, sin necesidad de que el método que lanzó la excepción proporcione más datos manualmente. Esto facilita depuración y mantenimiento del programa, ya que los errores se pueden rastrear de manera precisa hasta la función que los originó.

Además, tener toda esta información encapsulada dentro del objeto excepción permite unificar el tratamiento de errores, porque el manejador puede consultar los métodos del objeto para decidir cómo reaccionar, mostrar mensajes al usuario o registrar eventos en un log, sin depender de variables externas ni códigos de error dispersos por el programa. Esto mejora significativamente la modularidad y la claridad frente al modelo de C.


## 8. En Java, sobre el bloque **"try-catch"**, ¿se pueden tener más de un bloque `catch`? ¿cuántos bloques `catch` se ejecutan?

### Respuesta

En Java, sí se pueden tener múltiples bloques catch asociados a un mismo bloque try. Esto permite manejar distintos tipos de excepciones de manera específica, aplicando un tratamiento diferenciado según la clase de la excepción que se haya lanzado. Cada bloque catch declara el tipo de excepción que puede capturar y se ejecuta solo si el tipo coincide o es una subclase compatible.

Solo un bloque catch se ejecuta por excepción lanzada. Cuando ocurre un error dentro del try, el flujo de ejecución se detiene y Java busca el primer catch que pueda manejar la excepción. Una vez que se ejecuta ese bloque, los demás catch asociados al mismo try se omiten, y el flujo continúa después del bloque try-catch.

Este mecanismo permite escribir código más organizado y seguro, ya que cada tipo de error puede recibir un tratamiento específico, evitando mezclas de lógica y asegurando que los errores se gestionen de forma adecuada sin duplicar comprobaciones dentro del mismo bloque try. Además, mejora la legibilidad del programa, ya que queda claro qué tipos de excepciones pueden surgir y cómo se manejan.


## 9. Si las excepciones producen rupturas en el código llamador, ¿cómo podemos garantizar que se ejecuta siempre finalmente un código necesario para cierre de ficheros, liberacion de recursos, antes de que continúe propagándose la excepción? Pon un ejemplo en Java con `finally`, tanto con `catch` como sin él.

### Respuesta

En Java, para garantizar que se ejecute siempre un código necesario, como el cierre de ficheros o la liberación de recursos, se utiliza el bloque finally. Este bloque se ejecuta siempre, tanto si ocurre una excepción como si no, y se coloca después de los bloques try y catch. Esto asegura que las operaciones críticas de limpieza se realicen, evitando fugas de recursos o bloqueos de archivos.

Por ejemplo, un archivo abierto puede cerrarse de forma segura dentro de finally:
import java.io.*;

public class EjemploFinally {
    public static void main(String[] args) {
        FileReader fr = null;
        try {
            fr = new FileReader("archivo.txt");
            int c = fr.read();
            System.out.println("Primer carácter: " + c);
        } catch (IOException e) {
            System.out.println("Error al leer el archivo: " + e.getMessage());
        } finally {
            try {
                if (fr != null) fr.close();
                System.out.println("Archivo cerrado correctamente");
            } catch (IOException e) {
                System.out.println("Error al cerrar el archivo: " + e.getMessage());
            }
        }
    }
}

Incluso si no se incluye un catch, finally se ejecuta siempre que se use:

try {
    // código que podría lanzar excepción
} finally {
    // se ejecuta siempre, para limpiar recursos
}

Esto asegura que la limpieza se realice independientemente de si se capturó la excepción o si el programa la propagó a un nivel superior, manteniendo la consistencia del programa y evitando errores por recursos abiertos o bloqueados.


## 10. En Java, el bloque `finally` puede ir sin `catch`? ¿Se ejecuta siempre tanto si ocurre como si no ocurre una excepción? ¿Y si hay un `return` en medio del `try`?

### Respuesta

Sí, en Java el bloque finally puede aparecer sin ningún bloque catch asociado a un try. Su comportamiento principal es ejecutarse siempre, independientemente de que se produzca una excepción o no dentro del try. Esto permite asegurar la ejecución de código crítico de limpieza, como liberar recursos o cerrar archivos, incluso cuando la excepción se propaga hacia arriba y no se captura localmente.

Si dentro del bloque try se encuentra un return, el bloque finally se ejecuta antes de que el método realmente devuelva el valor. Esto garantiza que la limpieza siempre se realice, aunque la función esté finalizando prematuramente. Por ejemplo:

public static int ejemplo() {
    try {
        System.out.println("Dentro del try");
        return 10;
    } finally {
        System.out.println("Dentro del finally");
    }
}

Al ejecutar este método, la salida sería:

Dentro del try
Dentro del finally

y luego se devuelve 10. Esto muestra que finally se ejecuta incluso ante un return. En resumen, finally es la forma segura de ejecutar código de limpieza, garantizando su ejecución siempre, con o sin excepción, y aunque la función salga con return.


## 11. En Java, qué son las excepciones **"controladas"** y las **"no controladas"**? ¿Qué papel juega `RuntimeException`? Pon un ejemplo de excepciones típicas controladas y no controladas que incluso nosotros mismos podríamos usar. Haz dos listas con 3 o 4 ejemplos de situación donde se suele preferir una excepción controlada y donde se suele preferir una excepción no controlada.

### Respuesta

En Java, las excepciones se clasifican en controladas (checked) y no controladas (unchecked). Las controladas son aquellas que el compilador obliga a manejar mediante try-catch o a declarar con throws en la firma del método. Suelen representar errores previsibles que el programador puede anticipar, como problemas de entrada/salida o archivos que no existen. Las no controladas, derivadas de RuntimeException, no requieren ser declaradas ni capturadas; representan errores de programación, como pasar un valor nulo o un índice fuera de rango.

RuntimeException es la clase base de las excepciones no controladas. Permite que se lancen errores de lógica sin obligar al llamador a capturarlos, manteniendo el código más limpio cuando no tiene sentido recuperarse del error. Sin embargo, todavía se puede capturar si se desea un manejo específico.

Ejemplos de excepciones controladas:

-IOException → problemas al leer o escribir archivos.

-FileNotFoundException → archivo inexistente.

-SQLException → errores en consultas a bases de datos.

-ClassNotFoundException → clase no encontrada en tiempo de ejecución.

Ejemplos de excepciones no controladas:

-NullPointerException → acceso a referencia nula.

-ArrayIndexOutOfBoundsException → acceso fuera de los límites de un array.

-IllegalArgumentException → argumentos no válidos en un método.

-ArithmeticException → operaciones matemáticas ilegales, como división por cero.

Estas categorías permiten al programador decidir cuándo es necesario capturar la excepción y cuándo se considera un error de lógica que no se puede manejar localmente, favoreciendo un diseño más claro y seguro del programa.


## 12. ¿Qué es y para qué se usa `throws`? ¿Por qué es alternativa a capturar una excepción controlada?

### Respuesta

La palabra clave throws en Java se utiliza para declarar que un método puede generar una o varias excepciones controladas durante su ejecución. Es una forma de informar al compilador y al llamador del método que debe estar preparado para manejar esas excepciones, ya sea capturándolas con un bloque try-catch o propagándolas a su vez con throws.

throws es una alternativa a capturar la excepción dentro del propio método. Cuando un método no quiere o no puede decidir cómo tratar un error, puede simplemente declararlo con throws, permitiendo que la responsabilidad del manejo recaiga en el código que llama al método. Esto mantiene el método más limpio y centrado en su lógica principal, separando el control de errores del procesamiento normal.

Por ejemplo, al abrir un fichero, puede no tener sentido cerrar o recuperar el archivo dentro del propio método, y es más claro dejar que el llamador decida cómo actuar ante un FileNotFoundException. Así, throws permite un diseño más modular y flexible, propagando las excepciones hacia el nivel adecuado donde se pueda tomar una decisión de manejo efectiva.


## 13. Pon un ejemplo en Java de firma de método que incluya `throws`, de una función que abre un fichero pero que declara que no le interesa menejar la excepción de si el fichero no existe, sino que se propague hacia arriba. Eso sí, acuérdate del `finally`.

### Respuesta

Se puede declarar un método que abra un fichero y utilice throws para indicar que no maneja directamente las excepciones controladas, dejando que estas se propaguen al llamador. Al mismo tiempo, se puede usar finally para garantizar que los recursos se liberen, como cerrar el fichero, aunque se produzca una excepción.

Un ejemplo en Java sería:

import java.io.*;

public class EjemploThrows {

    // El método declara que puede lanzar IOException
    public static void abrirArchivo(String nombreArchivo) throws IOException {
        FileReader fr = null;
        try {
            fr = new FileReader(nombreArchivo);
            int c = fr.read();
            System.out.println("Primer carácter: " + c);
        } finally {
            if (fr != null) {
                fr.close();  // se cierra siempre aunque se lance la excepción
            }
        }
    }

    public static void main(String[] args) {
        try {
            abrirArchivo("archivo.txt");
        } catch (IOException e) {
            System.out.println("Error al abrir el archivo: " + e.getMessage());
        }
    }
}

En este ejemplo:

-El método abrirArchivo no captura IOException, sino que lo declara con throws.

-El bloque finally asegura que el FileReader se cierre siempre, evitando fugas de recursos.

-El main es el que decide cómo manejar la excepción, en este caso mostrando un mensaje.

Esto muestra cómo throws permite separar la lógica de apertura de fichero del tratamiento del error, manteniendo el código más modular y claro.


## 14. ¿Podemos poner en `throws` excepciones no controladas, como `RuntimeException`? ¿Debería el método llamador entonces poner `try-catch` en ese caso? ¿Qué sentido tendría?

### Respuesta

Sí, en Java se puede poner en throws una excepción no controlada, como RuntimeException, pero no es obligatorio capturarla. Estas excepciones representan errores de programación que normalmente no se pueden recuperar, por lo que el compilador no fuerza al llamador a incluir un bloque try-catch.

Si se declara throws con una excepción no controlada, el método llamador no está obligado a capturarla, aunque puede hacerlo si se desea un manejo específico. Esto puede ser útil para documentar el comportamiento del método, advirtiendo al desarrollador de posibles errores de lógica que podrían ocurrir, como pasar argumentos inválidos o acceder a índices fuera de rango.

Por ejemplo, un método podría lanzar IllegalArgumentException y declararlo con throws para que quede explícito que ciertos argumentos no son válidos. El llamador puede optar por capturar la excepción o dejar que se propague. Declarar estas excepciones en throws no cambia el funcionamiento, pero mejora la claridad del contrato del método y sirve como guía para los desarrolladores que lo utilicen.


## 15. ¿Cuándo se recomienda usar excepciones controladas, como `IOException`, y cuándo no controladas como `IllegalArgumentException`? ¿Existen en todos los lenguajes ambas opciones? En los que sólo existe una opción, ¿cuál es la más habitual?

### Respuesta

Se recomienda usar excepciones controladas (checked), como IOException, cuando se trata de errores previsibles y recuperables, como problemas de entrada/salida, archivos inexistentes o errores de red. Estas situaciones pueden ocurrir en condiciones normales de ejecución y el programador puede anticiparlas, proporcionando un manejo adecuado mediante try-catch o propagando la excepción con throws.

Por otro lado, las excepciones no controladas (unchecked), como IllegalArgumentException o NullPointerException, se usan cuando el error representa un fallo de lógica o de programación, que normalmente no se puede recuperar durante la ejecución. Estas excepciones indican errores que deberían corregirse en el código, y no es necesario capturarlas sistemáticamente.

No todos los lenguajes orientados a objetos ofrecen ambas opciones. Por ejemplo, Python solo tiene excepciones no controladas: todas las excepciones son objetos y pueden ser capturadas, pero el compilador no obliga a hacerlo. En los lenguajes que solo tienen una opción, normalmente se utilizan excepciones no controladas, porque la verificación en tiempo de compilación no es obligatoria. Esto simplifica el flujo del código, aunque requiere que el programador sea disciplinado al manejar los posibles errores.


## 16. ¿Tiene sentido lanzar excepciones dentro del `catch`? ¿Se puede relanzar la misma excepción capturada? ¿Cuándo tendría sentido hacer esto último? Pon ejemplos de ambos casos.

### Respuesta

Sí, tiene sentido lanzar excepciones dentro de un bloque catch. Esto se hace cuando, al capturar una excepción, se detecta que no se puede resolver el problema localmente y es necesario informar a niveles superiores de la aplicación. También puede usarse para transformar una excepción en otra más apropiada, adaptada al contexto del llamador.

Es posible relanzar la misma excepción capturada usando la palabra clave throw dentro del catch. Esto permite que la excepción original continúe propagándose después de realizar tareas intermedias, como registrar información en un log o liberar ciertos recursos. Este enfoque es útil cuando se quiere agregar contexto o registrar eventos sin detener la propagación del error.

Por ejemplo:

try {
    double resultado = Calculadora.raiz(-4);
} catch (IllegalArgumentException e) {
    System.out.println("Se intentó calcular una raíz negativa");
    throw e; // relanza la misma excepción
}

También se puede lanzar una nueva excepción dentro del catch para encapsular el error:

try {
    abrirArchivo("archivo.txt");
} catch (IOException e) {
    throw new RuntimeException("Error al procesar el archivo", e); // nueva excepción con causa
}

En este segundo caso, la nueva excepción proporciona un mensaje más general o adaptado al contexto de alto nivel, mientras que la causa original (e) queda registrada para depuración.


## 17. ¿En qué consiste que una excepción sea la **"causa"** de otra excepción? Pon un ejemplo en Java, donde capturemos una excepción de bajo nivel y la encapsulemos en otra personalizada de alto nivel. Cuando una excepción sale por pantalla y tiene una causa, ¿se ve?

### Respuesta

Que una excepción sea la causa de otra significa que un error de bajo nivel se encapsula dentro de una excepción de alto nivel, preservando la información original mientras se proporciona un mensaje o contexto más adecuado al nivel superior de la aplicación. Esto es útil para abstraer detalles internos y mantener el manejo de errores consistente sin perder la trazabilidad de la causa original.

Por ejemplo, en Java se puede capturar una excepción de entrada/salida y envolverla en una excepción personalizada de nivel superior:

import java.io.*;

class ErrorProcesandoArchivoException extends Exception {
    public ErrorProcesandoArchivoException(String mensaje, Throwable causa) {
        super(mensaje, causa);
    }
}

public class EjemploCausa {
    public static void procesarArchivo(String nombre) throws ErrorProcesandoArchivoException {
        try {
            FileReader fr = new FileReader(nombre);
            // código de procesamiento...
            fr.close();
        } catch (IOException e) {
            throw new ErrorProcesandoArchivoException("Error al procesar el archivo " + nombre, e);
        }
    }

    public static void main(String[] args) {
        try {
            procesarArchivo("archivo.txt");
        } catch (ErrorProcesandoArchivoException e) {
            e.printStackTrace(); // muestra mensaje y la causa original
        }
    }
}

Al ejecutarse, la consola mostrará tanto el mensaje de la excepción de alto nivel como la traza de la causa original (IOException). Esto permite depurar eficazmente, mostrando qué ocurrió realmente y dónde, mientras el código que maneja la excepción trabaja con un nivel de abstracción más apropiado para su contexto.
