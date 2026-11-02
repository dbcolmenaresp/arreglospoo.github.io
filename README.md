# arreglospoo
Implementación y uso de arreglos con programación orientada a objetos 

https://dbcolmenaresp.github.io/arreglospoo.github.io/arreglospoo.html

Clase Teórica: Arreglos y su Implementación con Programación Orientada a Objetos

Asignatura: Programación / Estructuras de Datos
Tema: Arreglos: fundamentos e implementación con POO
Duración estimada: 2 sesiones teóricas (90–120 min)
Prerrequisitos: Variables, tipos de datos, estructuras de control iterativas, conceptos básicos de clases y objetos.

---

1. Introducción y objetivos

Los arreglos son una de las estructuras de datos más básicas y ubicuas en programación. Aunque su concepto es simple, su correcta implementación en el paradigma orientado a objetos exige comprender no solo la sintaxis, sino también los principios de encapsulamiento, responsabilidad única y gestión segura de la memoria. Esta clase aborda ambos aspectos: primero los fundamentos conceptuales y luego su integración en el diseño de clases.

Objetivos de aprendizaje:

· Definir qué es un arreglo, sus características y su representación en memoria.
· Identificar las operaciones fundamentales sobre arreglos y sus limitaciones.
· Comprender cómo se encapsula un arreglo dentro de una clase, protegiendo su integridad.
· Diseñar clases que utilicen arreglos como atributos y expongan métodos seguros para su manipulación.
· Reconocer las ventajas y desventajas de los arreglos frente a otras estructuras.

---

2. Fundamentos de los arreglos

2.1. Definición

Un arreglo (también llamado vector, array o matriz en una dimensión) es una colección finita, homogénea y ordenada de elementos. Cada elemento ocupa una posición identificada por un índice numérico que comienza en 0. El término “homogénea” significa que todos los elementos son del mismo tipo de dato (por ejemplo, todos enteros, todos cadenas, todos objetos de una misma clase).

Formalmente, un arreglo de tipo T y longitud N es una secuencia:

a_0, a_1, a_2, \dots, a_{N-1}

donde cada a_i es de tipo T. El número total de elementos N se fija en el momento de la creación y no puede modificarse durante la vida del arreglo.

2.2. Características esenciales

Característica Descripción
Homogeneidad Todos los elementos comparten el mismo tipo.
Orden Los elementos están dispuestos en una secuencia lineal; el índice define su posición.
Tamaño fijo La longitud se establece al crear el arreglo y es inmutable.
Acceso directo por índice Se puede acceder a cualquier elemento en tiempo constante O(1) mediante su índice.
Memoria contigua Los elementos se almacenan en posiciones consecutivas de memoria, lo que favorece la localidad de caché.

2.3. Tipos de arreglos según sus dimensiones

· Unidimensionales: una sola fila de elementos. Ejemplo: int[] edades = new int[10];
· Multidimensionales: arreglos de arreglos. El caso más común es el bidimensional (matriz), donde cada elemento se referencia con dos índices (fila y columna). Ejemplo: int[][] tablero = new int[3][3];

El rango de un arreglo indica cuántas dimensiones tiene. Un arreglo bidimensional con F filas y C columnas contiene F \times C elementos.

2.4. Índices y rangos válidos

Para un arreglo de longitud N, los índices válidos van de 0 a N-1. Intentar acceder a un índice fuera de este rango provoca un error en tiempo de ejecución (en Java, ArrayIndexOutOfBoundsException). Esta es una fuente frecuente de fallos en programas noveles, y su prevención es una de las razones por las que la encapsulación en POO resulta valiosa.

2.5. Representación en memoria

Un arreglo unidimensional se almacena como un bloque contiguo de memoria del tamaño necesario para contener N elementos del tipo T. La dirección del elemento i se calcula como:

\text{dir}(a_i) = \text{dirBase} + i \times \text{tamañoDe}(T)

Este cálculo directo explica el acceso en tiempo constante. En lenguajes como Java, la variable de tipo arreglo no contiene los datos directamente, sino una referencia a la ubicación en memoria dinámica donde reside el arreglo. De hecho, en Java los arreglos son objetos. Esta naturaleza de objeto es la que permite tratarlos como ciudadanos de primera clase en el paradigma orientado a objetos.

---

3. Operaciones fundamentales sobre arreglos

Independientemente del lenguaje, todo arreglo admite un conjunto básico de operaciones. Comprenderlas es esencial antes de encapsularlas.

3.1. Declaración, creación e inicialización

En Java, la sintaxis general es:

```java
tipoDeDato[] nombreArreglo = new tipoDeDato[tamaño];
```

También es posible declarar e inicializar con valores literales:

```java
int[] numeros = {10, 20, 30, 40};
```

Cuando se crea un arreglo con new, sus elementos se inicializan automáticamente con el valor por defecto del tipo: 0 para tipos numéricos, false para boolean, null para referencias a objetos.

3.2. Acceso y asignación

El acceso a un elemento se realiza mediante nombreArreglo[indice]. La asignación sigue la misma sintaxis:

```java
numeros[2] = 99;          // asigna 99 a la posición 2
int x = numeros[0];       // lee el primer elemento
```

3.3. Recorrido

El recorrido consiste en visitar cada elemento del arreglo, generalmente con un bucle. Las dos formas canónicas en Java son:

· Bucle for con índice: permite modificar los elementos y conocer la posición.
  ```java
  for (int i = 0; i < numeros.length; i++) {
      System.out.println(numeros[i]);
  }
  ```
· Bucle for-each: más legible para solo lectura.
  ```java
  for (int n : numeros) {
      System.out.println(n);
  }
  ```

El atributo público length de los arreglos en Java proporciona el tamaño. Es importante notar que length es un atributo, no un método (a diferencia de length() en las cadenas).

3.4. Búsqueda y ordenamiento

· Búsqueda lineal: recorre el arreglo hasta encontrar el valor. Complejidad O(N).
· Búsqueda binaria: requiere que el arreglo esté ordenado. Complejidad O(\log N).
· Ordenamiento: algoritmos como burbuja, selección, inserción (O(N^2)) o mergesort/quicksort (O(N \log N)) operan sobre arreglos.

3.5. Limitaciones operativas

· Tamaño fijo: no se puede insertar ni eliminar elementos sin crear un nuevo arreglo y copiar los datos.
· Costo de redimensionamiento: operaciones como “añadir al final” requieren asignar un nuevo bloque de mayor tamaño y copiar todos los elementos.
· Heterogeneidad no permitida: no se pueden mezclar tipos en un mismo arreglo (a menos que se use un tipo base común, como Object).

---

4. Ventajas y desventajas de los arreglos

4.1. Ventajas

Ventaja Explicación
Acceso rápido El acceso por índice es O(1) gracias al cálculo directo de direcciones.
Simplicidad Su uso es directo y su sintaxis es sencilla en la mayoría de lenguajes.
Eficiencia de memoria Almacenamiento contiguo sin metadatos por elemento (a diferencia de estructuras enlazadas).
Localidad de caché El acceso secuencial aprovecha la caché del procesador, lo que acelera recorridos.
Base para otras estructuras Muchas estructuras (listas dinámicas, pilas, colas, tablas hash) se implementan sobre arreglos.

4.2. Desventajas

Desventaja Explicación
Tamaño fijo No se adaptan dinámicamente al número de elementos.
Inserción y eliminación costosas Insertar o eliminar en posiciones intermedias requiere desplazar elementos (O(N)).
Desperdicio de memoria Si se sobredimensiona, se reserva espacio no utilizado.
Riesgo de desbordamiento El acceso fuera de rango es un error frecuente.
Falta de encapsulamiento nativo Un arreglo “desnudo” expone su tamaño y sus elementos a modificaciones no controladas; de ahí la necesidad de encapsularlo en POO.

---

5. Implementación de arreglos con Programación Orientada a Objetos

La POO no reemplaza a los arreglos; los integra como componentes de objetos más ricos. La idea central es encapsular el arreglo dentro de una clase que controle su acceso y garantice su integridad.

5.1. Principios de diseño aplicados

1. Encapsulamiento: El arreglo se declara como atributo private. Ningún código externo puede acceder directamente a él ni modificar su tamaño o sus elementos sin pasar por los métodos de la clase. Esto protege la invariante de la clase (por ejemplo, que el número de elementos no exceda la capacidad).
2. Composición: La clase tiene un arreglo como parte de su estado. Esto es una relación de composición: el arreglo es un componente interno del objeto.
3. Responsabilidad única: La clase se encarga exclusivamente de gestionar la colección (añadir, eliminar, buscar, recorrer). El cliente (quien usa la clase) no necesita conocer los detalles de indexación ni de redimensionamiento.
4. Interfaz pública controlada: Se exponen métodos como agregar, obtener, tamaño, recorrer, pero se oculta la representación interna. Esto permite cambiar la implementación (por ejemplo, de arreglo a lista enlazada) sin afectar a los clientes.

5.2. Estructura típica de una clase que encapsula un arreglo

```java
public class Coleccion<T> {
    private T[] elementos;        // atributo encapsulado
    private int cantidad;         // número de elementos realmente almacenados
    private static final int CAPACIDAD_INICIAL = 10;

    public Coleccion() {
        elementos = (T[]) new Object[CAPACIDAD_INICIAL];
        cantidad = 0;
    }

    public void agregar(T elemento) {
        if (cantidad == elementos.length) {
            redimensionar();
        }
        elementos[cantidad++] = elemento;
    }

    public T obtener(int indice) {
        if (indice < 0 || indice >= cantidad) {
            throw new IndexOutOfBoundsException("Índice inválido: " + indice);
        }
        return elementos[indice];
    }

    public int tamaño() {
        return cantidad;
    }

    private void redimensionar() {
        T[] nuevo = (T[]) new Object[elementos.length * 2];
        System.arraycopy(elementos, 0, nuevo, 0, cantidad);
        elementos = nuevo;
    }
}
```

Análisis del diseño:

· elementos es private: el arreglo no se expone.
· cantidad es private y lleva el control de cuántas posiciones están ocupadas, evitando que el cliente confunda “capacidad” con “tamaño lógico”.
· agregar gestiona automáticamente el redimensionamiento cuando es necesario. Aunque el arreglo subyacente tiene tamaño fijo, la clase ofrece una interfaz de tamaño variable.
· obtener valida el índice antes de acceder, previniendo errores.
· redimensionar es private porque es un detalle interno de implementación.

5.3. Arreglos de objetos

Una de las aplicaciones más potentes de la POO es el arreglo de objetos. En lugar de almacenar tipos primitivos, el arreglo contiene referencias a instancias de una clase. Por ejemplo:

```java
Estudiante[] estudiantes = new Estudiante[30];
estudiantes[0] = new Estudiante("Ana", 20);
```

Cada posición del arreglo es una referencia a un objeto Estudiante. Esto permite modelar colecciones del mundo real con toda la riqueza de la POO (métodos, herencia, polimorfismo). Al encapsular este arreglo en una clase como Curso, se obtiene una entidad coherente:

```java
public class Curso {
    private Estudiante[] alumnos;
    private int numAlumnos;

    public Curso(int capacidad) {
        alumnos = new Estudiante[capacidad];
        numAlumnos = 0;
    }

    public void inscribir(Estudiante e) {
        if (numAlumnos < alumnos.length) {
            alumnos[numAlumnos++] = e;
        }
    }

    public Estudiante obtenerAlumno(int posicion) {
        if (posicion >= 0 && posicion < numAlumnos) {
            return alumnos[posicion];
        }
        return null;
    }
}
```

Este diseño refleja el ejemplo clásico de ColeccionCirculos presente en la literatura docente, donde una clase gestiona un vector de objetos Circulo con un límite máximo, un constructor que inicializa el vector vacío y métodos consultores y modificadores que respetan la capacidad.

5.4. Composición frente a herencia

Al implementar arreglos con POO, la relación natural es la composición, no la herencia. Una clase Curso tiene un arreglo de estudiantes; no es un arreglo. La composición permite delegar la gestión del arreglo a la clase contenedora y ofrecer una interfaz adaptada al dominio del problema. La herencia de arreglos no suele estar permitida (en Java, los arreglos son objetos especiales) y, en general, sería un diseño pobre porque un arreglo es una estructura de datos, no un comportamiento.

5.5. Manejo de excepciones y validación

Una clase bien diseñada no confía en que el cliente proporcione índices válidos ni datos correctos. Debe validar y lanzar excepciones claras. Por ejemplo:

```java
public T obtener(int indice) {
    if (indice < 0 || indice >= cantidad) {
        throw new IndexOutOfBoundsException(
            "Índice " + indice + " fuera de rango [0, " + (cantidad - 1) + "]"
        );
    }
    return elementos[indice];
}
```

Esta práctica convierte errores silenciosos (como un acceso a memoria inválida en C) en excepciones controladas que el cliente puede manejar.

5.6. La interfaz List y las colecciones dinámicas

Aunque esta clase se centra en arreglos, es importante mencionar que en Java la biblioteca estándar ofrece ArrayList, una clase que encapsula internamente un arreglo y proporciona una interfaz de tamaño variable. ArrayList es el ejemplo canónico de cómo un arreglo puede ocultarse tras una API cómoda y segura. Estudiar su implementación (o simplificarla en una clase propia) es un excelente ejercicio de POO.

---

6. Ejemplo integrador: clase GestionArreglo con encapsulamiento

A continuación se presenta una clase genérica que encapsula un arreglo de enteros y ofrece operaciones básicas, con validaciones y control de capacidad.

```java
public class GestionArreglo {
    private int[] datos;
    private int cantidad;

    public GestionArreglo(int capacidadInicial) {
        if (capacidadInicial <= 0) {
            throw new IllegalArgumentException("La capacidad debe ser positiva");
        }
        datos = new int[capacidadInicial];
        cantidad = 0;
    }

    public void agregar(int valor) {
        if (cantidad == datos.length) {
            redimensionar();
        }
        datos[cantidad++] = valor;
    }

    public int obtener(int indice) {
        if (indice < 0 || indice >= cantidad) {
            throw new IndexOutOfBoundsException("Índice fuera de rango");
        }
        return datos[indice];
    }

    public void modificar(int indice, int nuevoValor) {
        if (indice < 0 || indice >= cantidad) {
            throw new IndexOutOfBoundsException("Índice fuera de rango");
        }
        datos[indice] = nuevoValor;
    }

    public int tamaño() {
        return cantidad;
    }

    public boolean contiene(int valor) {
        for (int i = 0; i < cantidad; i++) {
            if (datos[i] == valor) {
                return true;
            }
        }
        return false;
    }

    private void redimensionar() {
        int[] nuevo = new int[datos.length * 2];
        System.arraycopy(datos, 0, nuevo, 0, cantidad);
        datos = nuevo;
    }
}
```

Puntos clave del ejemplo:

· El arreglo datos es private; nadie fuera de la clase puede accederlo directamente.
· cantidad es la invariante que garantiza que solo se accede a posiciones ocupadas.
· agregar maneja el crecimiento automático sin exponer el arreglo interno.
· obtener y modificar validan el índice antes de operar.
· redimensionar es un método auxiliar privado, invisible para el cliente.

Este diseño transforma un arreglo de tamaño fijo en una estructura de tamaño lógico variable, todo ello sin que el cliente perciba la complejidad subyacente.

---

7. Errores comunes y buenas prácticas

7.1. Errores frecuentes

1. Confundir capacidad con tamaño lógico: Un arreglo de 100 posiciones no significa que las 100 estén ocupadas. La variable cantidad (o size) es indispensable.
2. Exponer el arreglo directamente: Retornar el arreglo interno con un getter rompe el encapsulamiento. Si se necesita devolver una copia, usar Arrays.copyOf.
3. No validar índices: Acceder sin comprobar el rango provoca excepciones en tiempo de ejecución.
4. Redimensionar sin copiar: Crear un nuevo arreglo y olvidar copiar los elementos existentes produce pérdida de datos.
5. Usar == para comparar objetos: En arreglos de objetos, == compara referencias, no contenido. Para contenido, usar equals.

7.2. Buenas prácticas

· Encapsular siempre el arreglo como private.
· Documentar la invariante de la clase (por ejemplo: 0 <= cantidad <= datos.length).
· Ofrecer métodos de solo lectura cuando sea necesario, devolviendo copias defensivas.
· Preferir for-each para recorridos de solo lectura.
· Utilizar System.arraycopy o Arrays.copyOf para copias eficientes.
· Considerar ArrayList cuando el tamaño dinámico sea un requisito predominante, pero comprender su implementación interna basada en arreglos.

---

8. Conclusiones

Los arreglos son una estructura fundamental que combina simplicidad conceptual con eficiencia en el acceso. Su naturaleza de tamaño fijo y su exposición directa en lenguajes como C los hacen vulnerables a errores, pero la Programación Orientada a Objetos ofrece un marco ideal para encapsularlos, protegerlos y extenderlos con una interfaz controlada. Al envolver un arreglo en una clase, se gana:

· Seguridad: validación de índices y control de capacidad.
· Mantenibilidad: la representación interna puede cambiar sin afectar a los clientes.
· Expresividad: los métodos de la clase hablan el lenguaje del dominio (inscribir, agregar, buscar) en lugar de exponer detalles de bajo nivel.

La transición desde el uso de arreglos “desnudos” hacia clases que los encapsulan es un paso crucial en la madurez como programador. Comprender este puente entre los fundamentos y la POO permite abordar estructuras más complejas (listas enlazadas, árboles, tablas hash) con una base sólida y un diseño disciplinado.

---

9. Ejercicios propuestos

1. Arreglo encapsulado de cadenas: Diseñe una clase ListaNombres que encapsule un arreglo de String. Debe permitir agregar nombres (con redimensionamiento automático), obtener un nombre por índice, eliminar la última ocurrencia de un nombre y listar todos los nombres.
2. Arreglo de objetos: Implemente una clase Inventario que contenga un arreglo de objetos Producto (con atributos como nombre, precio y cantidad). Proporcione métodos para añadir productos, buscar por nombre y calcular el valor total del inventario.
3. Matriz encapsulada: Cree una clase Matriz que encapsule un arreglo bidimensional de enteros. Debe ofrecer métodos para sumar dos matrices, multiplicar por un escalar y obtener la traspuesta. Valide que las dimensiones sean compatibles.
4. Refactorización: Analice el siguiente código que usa un arreglo “desnudo” y refactorícelo para encapsularlo en una clase con una interfaz segura:
   ```java
   int[] notas = new int[50];
   int n = 0;
   // ... código que agrega notas y accede a ellas sin control
   ```
5. Comparación crítica: Elabore un cuadro comparativo entre un arreglo primitivo y una clase que lo encapsula, considerando aspectos como seguridad, flexibilidad, costo de memoria y legibilidad.

---

Referencias y lecturas recomendadas

· Cobá Juárez Pegueros, J. P. Algoritmos y Programación Básica: Arreglos. Facultad de Ingeniería, UAEMEX. (Define arreglo como colección finita, homogénea y ordenada).
· Universidad Abierta y a Distancia de México. Programación Orientada a Objetos I, Unidad 4: Arreglos. (Aborda declaración, recorrido y operaciones en Java, y la naturaleza de objeto de los arreglos).
· UAPA. Utilerías y Clases de Uso General. (Explica la sintaxis de arreglos en Java, el atributo length y el recorrido con for-each).
· Sapena, O. Tema 1: Conceptos de Java para Estructuras de Datos. Universitat Politècnica de València. (Ejemplo de ColeccionCirculos con arreglo encapsulado y métodos consultores/modificadores).
· Materiales sobre arrays de objetos y encapsulamiento en Java (ejemplos de MusicTrack[], Estudiante[], Curso).
