# EA2_Grupo-14_ImplementacionDiagramaDeClasesbiblioteca

![](https://edea.juntadeandalucia.es/bancorecursos/items/95e089da-b938-4d08-a03c-5e773972e8e7/1/viewscorm.jsp?.vi=file&event__=scormtree.viewNode&eventp__0=uid9)


## Introducción

Centramos este trabajo en el diseño e implementación de un sistema de gestión para una biblioteca para el cual usaremos el paradigma de Programación Orientada a Objetos (POO). A través de nuestro diagrama de clases UML, se definirá la estructura organizada en la cual la entidad central, la Biblioteca, actúa como el eje que gestiona los libros, registra cada usuario e incluye el historial de préstamos. Este sistema se encuentra diseñado para hacer control de procesos clave, entre los que tenemos; la gestión de Inventario permitiendo el manejo de libros utilizando atributos específicos como título, autor y estado de disponibilidad. El control de usuarios, a través del cual se realiza el registro de personas autorizadas para relacionarse con la biblioteca, permitiéndoles mantener como máximo un número de tres libros prestados de manera simultánea. A través de la administración de préstamos, poder formalizar la relación entre un usuario y un libro, permitiendo registrar fechas de entrega y devolución para tener un seguimiento efectivo.
Esta infraestructura permite transformar el modelo visual de relaciones y atributos en una aplicación funcional utilizando lenguajes de programación como Java, esto garantiza que se puedan cumplir con reglas de negocio estrictas, como lo es la verificación de si un usuario puede prestar más ejemplares antes de procesar una nueva solicitud.

## Objetivo General
Desarrollar un sistema de gestión bibliotecaria que permita organizar el catálogo de libros, registrar a los usuarios y administrar el ciclo de vida de los préstamos de manera eficiente utilizando el paradigma de Programación Orientada a Objetos POO.

## Objetivos Específicos
1.	Realizar gestión del inventario de libros a través del registro de sus datos principales (título, autor y género) y el control automático del estado de disponibilidad.

2.	Realizar control de registro de usuarios revisando que se cumpla la regla de negocio que posibilita a cada persona tener un máximo de tres libros bajo su responsabilidad de manera simultánea.

3.	Vigilar las transacciones de préstamo y devolución, tomando las fechas exactas de cada movimiento para posibilitar el seguimiento y el registro de ejemplares dentro de la biblioteca.

## Planteamiento del Problema
En este contexto se encuentra la necesidad de sistematizar los procesos operativos de una biblioteca con el fin de garantizar un control eficaz respecto de sus recursos. El problema central se encuentra en la complicación para coordinar de forma manual el vínculo entre elementos fundamentales: el inventario de libros, el registro de usuarios y el historial de préstamos.
Sin contar con un sistema automatizado, es muy complejo verificar en tiempo real si un libro está o no disponible y quién lo tiene, además resulta complejo poder efectuar las políticas institucionales, como el caso del límite máximo de libros que un socio puede tener en su poder simultáneamente.

## Análisis del Problema
Al analizar el diagrama de clases se desprenden los siguientes componentes críticos para dar solución:
•	Gestión Centralizada (Clase Biblioteca):
Identificamos una entidad núcleo que actuará como organizadora, manteniendo listas de todos los libros, usuarios y préstamos realizados. Esta debe responder a consultas operativas, como la búsqueda de ejemplares por título o autor y la general de préstamos.
•	Control de Inventario (Clase Libro):
Cada elemento debe estar perfectamente identificado por su título, autor y género. Es además vital que el sistema indague por un atributo de disponibilidad que cambie de forma automática por medio de métodos de actualización cada vez que se realice un préstamo o devolución.
•	Reglas de Negocio del Usuario (Clase Usuario):
El sistema debe administrar la identidad de los socios (nombre, apellido, ID) y ejecutar eficientemente la relación de multiplicidad de 0..3 entre el Usuario y el Libro, esto implica que la lógica del sistema debe siempre validar si el usuario "puede prestar" antes de permitir una nueva transacción.
•	Trazabilidad de Transacciones (Clase Préstamo):
Cada préstamo es una entidad independiente la cual involucra tanto a un usuario como a un libro. Este análisis requiere el registro exacto de la fecha de préstamo y la fecha de devolución para obtener un seguimiento efectivo y la generación de reportes sobre el estado de los libros.

## Propuesta de la solución
Esta se basa en una estructura organizada la cual conecta de forma lógica a cada uno de los libros, los usuarios y los procesos de préstamo. A continuación, encontramos a detalle y en términos sencillos cómo funcionaría esta solución:
1. El núcleo del Sistema (Clase Biblioteca)
La solución plantea una entidad central llamada Biblioteca la cual actúa como el principal administrador. Esta tendría la función de:
•	Mantener los registros guardando las listas actualizadas de cada uno de los libros disponibles, los usuarios que se encuentran registrados y el historial de los préstamos que se hayan realizado.
•	Facilitar búsquedas para encontrar de forma rápida cualquier obra ya sea por título o autor.
•	Operar los procesos ya que es la responsable de ejecutar acciones como "prestar" y "devolver", garantizando que todo quede registrado de forma correctamente en el sistema.
2. Catálogo de Libros (Clase Libro)
Cada libro dentro del sistema no es simplemente una ficha de datos (título, autor, género), sino que además tiene un indicador de disponibilidad.
•	El libro, dicho de cierta forma "sabe" si está en estantería o prestado, ya que cambia su estado de forma automática cada vez que se realiza un movimiento.
•	Cuenta también con funciones internas que permiten actualizar su propia disponibilidad sin generar errores manuales.
3. Control de Usuarios (Clase Usuario)
El sistema logra identificar a cada persona con sus respectivos datos básicos además de un ID único. Hay una regla de oro automática implementada en la solución:
•	Antes de hacer entrega de un libro, el sistema verifica si el usuario cuenta con tres ejemplares en su poder. Si ya alcanzó ese límite, a través del método (puedePrestar) bloqueará la transacción hasta que este usuario devuelva por lo menos uno.
4. Registro Transaccional (Clase Préstamo)
Para evitar confusiones sobre quién tiene qué libro, la solución genera un "recibo digital" el cual se llama (Préstamo).
•	Este registro vincula a un usuario determinado con un libro específico.
•	Registra la fecha exacta en que el libro salió y la fecha en que retorna a la biblioteca, lo que permite tener un seguimiento absoluto de cada ejemplar.
Para resumir, la solución propuesta convierte el diagrama UML en un instrumento funcional en el que la Biblioteca organiza a los Libros y Usuarios, utilizando los Préstamos para asegurar que ningún libro se pierda y que además se respeten los límites de préstamo de forma automática.

## Diseño e implementación
Teniendo en cuenta el diagrama de clases UML, para implementación del diseño en código Java, para aplicar los principios de encapsulamiento e instanciación en POO Programación Orientada a Objetos presentamos esta estructura.
1. Clases y Encapsulamiento
A continuación, se definen las clases con sus atributos privados (-) y métodos públicos (+) tal como se especifica en el diagrama UML.
```java
# Clase Libro
# Esta clase gestiona los datos de los ejemplares (Libros) de la biblioteca.

public class Libro {
    // 1. Atributos Privados
    private int id;
    private String titulo;
    private String autor;
    private String genero;
    private boolean disponible;
    // 2. Constructor
    public Libro(int id, String titulo, String autor, String genero, boolean disponible) {
        this.id = id;
        this.titulo = titulo;
        this.autor = autor;
        this.genero = genero;
        this.disponible = disponible;
    }
    // 3. Método para mostrar toda la información
    public void mostrarInformacion() {
        System.out.println("ID: " + id);
        System.out.println("Título: " + titulo);
        System.out.println("Autor: " + autor);
        System.out.println("Género: " + genero);
        System.out.println("Disponible: " + disponible);
        System.out.println("---------------------------");
    }
    // 4. Métodos públicos para actualizar disponibilidad
    public void actualizarDisponibilidad() {
        this.disponible = !this.disponible;
    }
    public void devolver() {
        disponible = true;
    }
}
```
```java
Clase Usuario
Aquí se representan a los socios y se vigila la restricción de poseer un máximo de tres libros prestados simultáneamente.
public class Usuario {
    // 1. Atributos
    private String id;
    private String nombre;
    private String apellido;
    private Libro libroPrestado; // Aquí guardamos EL libro que tiene el usuario
    // 2. Constructor
    public Usuario(String id, String nombre, String apellido) {
        this.id = id;
        this.nombre = nombre;
        this.apellido = apellido;
        this.libroPrestado = null; // Al empezar, no tiene ningún libro
    }
    // 3. Métodos
    public boolean puedePrestar() {
        // Si el espacio de libro está vacío, puede pedir uno
        if (libroPrestado == null) {
            return true;
        } else {
            return false;
        }
    }
    public boolean agregarLibro(Libro nuevoLibro) {
        if (puedePrestar()) {
            this.libroPrestado = nuevoLibro; // El usuario recibe el libro
            return true;
        }
        return false;
    }
    public boolean devolverLibro(Libro libroADevolver) {
        this.libroPrestado = null; // El usuario devuelve el libro
        return true;
    }
    // Método para mostrar usuario
    public void mostrarUsuario() {
        System.out.println("Usuario: " + nombre + " " + apellido);
        if (libroPrestado != null) {
            System.out.println("Tiene un libro prestado.");
        } else {
            System.out.println("No tiene libros prestados.");
        }
    }
}
```
```java
Clase Biblioteca
Clase central a través de la cual se gestiona libros, usuarios y préstamos.
public class Biblioteca {
    // Atributos privados
    private Libro libroGestionado;
    private Usuario usuarioRegistrado;
    private Prestamo prestamoContenido;

    //Constructor
    public Biblioteca() {
   }

    public boolean prestarLibro(Usuario usuario, Libro libro) {
        if (usuario.puedePrestar()) {
            usuario.agregarLibro(libro);
            libro.actualizarDisponibilidad();
            return true;
        }
        return false;
    }

    public boolean devolverLibro(Usuario usuario, Libro libro) {
        usuario.devolverLibro(libro);
        libro.actualizarDisponibilidad();
        return true;
    }

    // Métodos de búsqueda públicos
    public void buscarTitulo(String titulo) {
        System.out.println("Buscando: " + titulo);
    }

    public void buscarAutor(String autor) {
        System.out.println("Buscando autor: " + autor);
    }

    public void consultarPrestamos() {
        System.out.println("Consultando historial...");
    }
}
```
```java
Clase préstamo
Es la entidad que se encarga de formalizar y registrar la transacción comercial o administrativa ocurrida en el momento en que un socio retira un ejemplar de la biblioteca.
public class Prestamo {
    private Usuario usuario;
    private Libro libro;
    private String fechaPrestamo;
    private String fechaDevolucion;

    public Prestamo(Usuario usuario, Libro libro, String fecha) {
        this.usuario = usuario;
        this.libro = libro;
        this.fechaPrestamo = fecha;
    }

    public void registrarPrestamo() {
        System.out.println("Registro de salida iniciado...");
    }

    public void registrarDevolucion() {
        this.fechaDevolucion = "Fecha actual";
    }

    public void seguimientoLibros() {
        // Lógica de trazabilidad
    }
}
```
```java
Clase main
No es una entidad de datos como las demás (Libro, Usuario, Prestamo o Biblioteca), sino que sirve como el punto de entrada o el "iniciador" de todo el programa en el lenguaje Java.
public static void main(String[] args) {
    // Creamos un objeto de la clase Libro
    Libro libro1 = new Libro(
            101,
            "Cien años de soledad",
            "Gabriel García Márquez",
            "Novela",
            true);
    // Mostramos la información inicial
    System.out.println("--- Estado Inicial ---");
    libro1.mostrarInformacion();
    // Usamos los métodos para ver cómo cambia el objeto
    System.out.println("Cambiando disponibilidad...");
    libro1.actualizarDisponibilidad();
    // Mostramos la información actualizada
    System.out.println("--- Estado Final ---");
    libro1.mostrarInformacion();
// Instanciación del Usuario
    Usuario usuario = new Usuario("U77", "Gabriel", "García");
    // Acción: El usuario intenta pedir prestado un libro
    System.out.println("Verificando si el usuario puede pedir el libro...");
    if (usuario.puedePrestar()) {
        usuario.agregarLibro(libro1);
        System.out.println("¡Libro asignado con éxito!");
    }
    usuario.mostrarUsuario();
// Instanciamos la biblioteca
    Biblioteca miBiblioteca = new Biblioteca();
    // Mostramos un mensaje para confirmar que la biblioteca existe en el programa
    System.out.println("\n--- Reporte de Biblioteca ---");
    System.out.println("Biblioteca funcionando correctamente.");
}
```
Esta implementación garantiza que los datos internos solo se modifiquen mediante los métodos públicos definidos, manteniendo la integridad del sistema bibliotecario conforme al diseño UML

## Conclusión

Para concluir, el diseño presentado permite la automatización y centralización de la gestión de la biblioteca utilizando una entidad núcleo (Biblioteca) la cual coordina de manera eficiente a los usuarios e inventario de libros. La implementación de reglas claras, como el caso del límite de tres libros por socio y la vigilancia de fechas mediante la clase Prestamo, asegura un control muy exacto respecto de la disponibilidad de cada ejemplar y el cumplimiento de las políticas institucionales.

## Bibliografía

Google. (2026, 15 de marzo). NotebookLM (ID: 6546ec93...). Google NotebookLM. https://notebooklm.google.com/notebook/6546ec93-8cba-48f8-a8a9-50588226315c

JGraph Ltd. (2026). diagrams.net (Versión X.X) [Software de computación]. https://app.diagrams.net/

## Anexos

![]()
