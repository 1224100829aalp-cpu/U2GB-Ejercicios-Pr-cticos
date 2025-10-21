# U2GB-Ejercicios-Practicos
## Actividad 01: Manipulación de Lista Enlazada
### Nodo
```javascript
package Actividad1;

/**
 *
 * @author angellunaperez
 * Esta clase representa un nodo individual 
 * la lista enlazada simple.
 */
public class Nodo {
    public int dato;
    public Nodo siguiente;

    /**
     * Constructor para crear un nuevo nodo.
    */
    public Nodo(int dato) {
        this.dato = dato;
        this.siguiente = null; // no apunta a ningún otro nodo
    }
}
```
### ListaEnlazada Metodos
```javascript
package Actividad1;
import java.util.Random;
import java.util.Scanner;
/**
 *
 * @author angellunaperez
 * Esta clase mplementa las operaciones 
 * sobre la lista enlazada simple de
 * enteros positivos.

 */

public class ListaEnlazadaSimple {
    private Nodo cabeza;

    public ListaEnlazadaSimple() {
        this.cabeza = null; // La lista comienza vacía
    }

    // 1: Crear la lista enlazada ---

    /**
     * Inserta un nuevo nodo al final de la lista.
     * @param dato El número entero positivo a insertar.
     */
    public void insertarAlFinal(int dato) {
        Nodo nuevoNodo = new Nodo(dato);
        
        // Caso 1: La lista está vacía
        if (this.cabeza == null) {
            this.cabeza = nuevoNodo;
            return;
        }
        
        // Caso 2: Recorrer hasta el último nodo
        Nodo actual = this.cabeza;
        while (actual.siguiente != null) {
            actual = actual.siguiente;
        }
        
        // El último nodo apunta al nuevo nodo
        actual.siguiente = nuevoNodo;
    }

    /**
     * Genera números aleatorios e inserta al final de la lista.
     * @param cantidad Cantidad de números a generar.
     * @param min Valor mínimo para la generación.
     * @param max Valor máximo para la generación.
     */
    public void generarYCrear(int cantidad, int min, int max) {
        Random random = new Random();
        System.out.println("Generando e insertando " + cantidad + " números al azar (entre " + min + " y " + max + ")...");
        for (int i = 0; i < cantidad; i++) {
            int numero = random.nextInt(max - min + 1) + min;
            insertarAlFinal(numero);
        }
        System.out.println("Lista creada.");
    }

    // --- Tarea 2: Recorrer la lista ---

    /**
     * Recorre la lista, visitando nodo por nodo hasta llegar a null, y muestra sus elementos.
     */
    public void recorrerYMostrar() {
        if (this.cabeza == null) {
            System.out.println("La lista esta vacia");
            return;
        }

        System.out.println("\nRecorrido de la lista:");
        Nodo actual = this.cabeza;
        StringBuilder sb = new StringBuilder();
        
        // El recorrido visita nodo por nodo hasta que 'actual' es null
        while (actual != null) { 
            sb.append(actual.dato);
            if (actual.siguiente != null) {
                sb.append(" -> ");
            }
            actual = actual.siguiente;
        }
        System.out.println(sb.toString());
    }

    // --- Tarea 3: Eliminar nodos mayores a un valor dado ---

    /**
     * Elimina todos los nodos cuyo campo dato sea MAYOR al valor límite ingresado.
     * @param valorLimite El valor de referencia para la eliminación.
     */
    public void eliminarMayoresA(int valorLimite) {
        if (this.cabeza == null) {
            System.out.println(" La lista está vacía, no hay nada que eliminar.");
            return;
        }

        int nodosEliminados = 0;

        // Caso 1: Eliminar nodos en la CABEZA que sean mayores al límite
        while (this.cabeza != null && this.cabeza.dato > valorLimite) {
            this.cabeza = this.cabeza.siguiente; // La cabeza se mueve al siguiente (el nodo anterior se elimina)
            nodosEliminados++;
        }
        
        // Si la lista se vació, terminamos
        if (this.cabeza == null) {
            System.out.println("\n Se eliminaron " + nodosEliminados + " nodos, la lista quedó vacía.");
            return;
        }

        // caso 2: Recorrer y eliminar nodos INTERMEDIOS
        Nodo actual = this.cabeza;
        
        // Se detiene cuando no hay un siguiente nodo para evaluar (el actual puede ser el último)
        while (actual.siguiente != null) {
            // Si el *siguiente* nodo debe ser eliminado
            if (actual.siguiente.dato > valorLimite) {
                // Ajustar el enlace: 'actual.siguiente' salta el nodo a eliminar
                actual.siguiente = actual.siguiente.siguiente; 
                nodosEliminados++;
                // NOTA: NO avanzamos 'actual' aquí, ya que el nuevo actual.siguiente también 
                // podría ser mayor al límite y debe ser evaluado.
            } else {
                // Si el siguiente nodo NO se elimina, avanzamos 'actual'
                actual = actual.siguiente;
            }
        }
        
        System.out.println("\n Proceso de eliminación finalizado. Se eliminaron **" + nodosEliminados + "** nodos.");
    }
}
```
### PruebaPrincipal
```javascript
package Actividad1;
import java.util.Scanner;

/**
 *
 * @author angellunaperez
 * En esta clase principal para probar la 
 * implementación de la Lista 
 * Enlazada Simple.
 */


public class Principal {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        ListaEnlazadaSimple lista = new ListaEnlazadaSimple();

        // --- Tarea 1: Crear la lista ---
        lista.generarYCrear(15, 1, 50); 

        // --- Tarea 2: Recorrer la lista antes de la eliminación ---
        System.out.println("\n*** estado inicial de la lista ***");
        lista.recorrerYMostrar();

        // --- Tarea 3: Eliminar nodos ---
        int limite = 0;
        try {
            System.out.print("\n Ingrese el valor limite. Se eliminarán los nodos MAYORES a este valor: ");
            limite = scanner.nextInt();
        } catch (java.util.InputMismatchException e) {
            System.out.println("Entrada no valida");
            limite = 25;
            scanner.nextLine(); // Limpiar el buffer
        }
        
        lista.eliminarMayoresA(limite);

        // --- Tarea 2: Recorrer la lista después de la eliminación ---
        System.out.println("\n*** estado final de la lista (Limite: " + limite + ") ***");
        lista.recorrerYMostrar();

        scanner.close();
    }
}
```
## Actividad 02: Lista Enlazada de Palabras desde Archivo
### Nodo
```javascript
package Actividad2;

/**
 *
 * @author angellunaperez
 * Esta clasde representa un nodo en la lista 
 * enlazada, 
 * conteniendo una palabra.
 */
public class Nodo {
    public String palabra;
    public Nodo siguiente;

    public Nodo(String palabra) {
        this.palabra = palabra;
        this.siguiente = null;
    }
}
```
### ListaPabras
```javascript
package Actividad2;
import java.util.ArrayList;
/**
 *
 * @author angellunaperez
 * Esta claswe implementa la lista
 * enlazada simple para almacenar palabras.
 */

public class ListaPalabras {
    private Nodo cabeza;

    public ListaPalabras() {
        this.cabeza = null;
    }

    // --- Tarea 2: Formación de la lista (Insertar al final) ---
    /**
     * Inserta una palabra al final de la lista,
     * manteniendo el orden de aparicion
\     */
    public void insertarAlFinal(String palabra) {
        Nodo nuevoNodo = new Nodo(palabra);
        
        if (this.cabeza == null) {
            this.cabeza = nuevoNodo;
            return;
        }
        
        Nodo actual = this.cabeza;
        while (actual.siguiente != null) {
            actual = actual.siguiente;
        }
        actual.siguiente = nuevoNodo;
    }

    // --- Tarea 3: Manipulación dinámica (Añadir) ---
    public void anadirPalabra(String palabra) {
        // La inserción al final ya cumple con el requisito de añadir
        insertarAlFinal(palabra);
        System.out.println("Palabra '" + palabra + "' añadida al final de la lista.");
    }
    
    // --- Tarea 3: Manipulación dinámica (Eliminar) ---
    /**
     * Elimina la primera aparicion de una palabra especifica de la lista.
     * @param palabraAEliminar La palabra a buscar y eliminar.
     * @return true si se eliminó, false si no se encontro
     */
    public boolean eliminarPalabra(String palabraAEliminar) {
        Nodo actual = this.cabeza;
        Nodo anterior = null;

        // Caso 1: La cabeza contiene la palabra
        if (actual != null && actual.palabra.equalsIgnoreCase(palabraAEliminar)) {
            this.cabeza = actual.siguiente; // Mover la cabeza al siguiente nodo
            System.out.println("Palabra '" + palabraAEliminar + "' eliminada (era la primera).");
            return true;
        }

        // Caso 2: Buscar en el resto de la lista
        while (actual != null && !actual.palabra.equalsIgnoreCase(palabraAEliminar)) {
            anterior = actual;
            actual = actual.siguiente;
        }

        // Si 'actual' es null, la palabra no fue encontrada
        if (actual == null) {
            System.out.println("Palabra '" + palabraAEliminar + "' no encontrada en la lista.");
            return false;
        }

        // Si se encontro, 'anterior' salta al nodo siguiente de 'actual'
        anterior.siguiente = actual.siguiente;
        System.out.println("Palabra '" + palabraAEliminar + "' eliminada.");
        return true;
    }
    
    // --- Tarea 4: Escritura en archivo (Obtener todas las palabras) ---
    /**
     * Recorre la lista y devuelve todas las palabras en un ArrayList.
     * @regresa una lista de Strings con todas las palabras en orden.
     */
    public ArrayList<String> obtenerTodasLasPalabras() {
        ArrayList<String> palabras = new ArrayList<>();
        Nodo actual = this.cabeza;
        while (actual != null) {
            palabras.add(actual.palabra);
            actual = actual.siguiente;
        }
        return palabras;
    }
    
    // Mostrar el contenido de la lista (utilidad para la interfaz)
    public void mostrarLista() {
        if (this.cabeza == null) {
            System.out.println("La lista está vacía.");
            return;
        }
        System.out.println("\n*** CONTENIDO ACTUAL DE LA LISTA ***");
        Nodo actual = this.cabeza;
        StringBuilder sb = new StringBuilder();
        int contador = 0;
        while (actual != null) {
            sb.append(actual.palabra);
            if (actual.siguiente != null) {
                sb.append(" -> ");
            }
            actual = actual.siguiente;
            contador++;
        }
        System.out.println(sb.toString());
        System.out.println("Total de palabras: " + contador);
    }
}
```
### Principal
```javascript
package Actividad2;
import java.io.File;
import java.io.FileWriter;
import java.io.IOException;
import java.util.Scanner;
import java.util.ArrayList;

/**
 *
 * @author angellunaperez
 *  Esta es la clase principal que maneja la 
 * lectura/escritura 
 * del archivo y la interacción.
 */

public class Principal {
    
    private static final String palabras = "palabras.txt";

    public static void main(String[] args) {
        ListaPalabras lista = new ListaPalabras();
        Scanner entradaUsuario = new Scanner(System.in);

        // --- Tarea 1 & 2: Lectura y Formación de la lista ---
        leerArchivoALista(lista);

        // --- Tarea 3: Manipulación dinámica ---
        manipulacionDinamica(lista, entradaUsuario);

        // --- Tarea 4: Escritura en archivo ---
        escribirListaAArchivo(lista);

        entradaUsuario.close();
    }
    
    /**
     * Lee el archivo y carga las palabras en la lista enlazada
     */
    private static void leerArchivoALista(ListaPalabras lista) {
        System.out.println(" Leyendo el archivo '" + palabras + "'...");
        try (Scanner scannerArchivo = new Scanner(new File(palabras))) {
            // El Scanner lee palabras automáticamente, separadas por espacios, saltos de línea, etc.
            while (scannerArchivo.hasNext()) {
                String palabra = scannerArchivo.next();
                // Tarea 2: Inserción en orden de aparición (al final)
                lista.insertarAlFinal(palabra);
            }
            System.out.println("Lectura finalizada. Lista creada.");
            lista.mostrarLista();
        } catch (IOException e) {
            System.err.println("Error al leer el archivo " + palabras + ": " + e.getMessage());
            System.out.println("Creando una lista vacía para continuar...");
        }
    }
    
    /**
     * permite al usuario interactuar con la lista
     */
    private static void manipulacionDinamica(ListaPalabras lista, Scanner scanner) {
        int opcion;
        String palabra;
        
        do {
            System.out.println("\n--- Menú de Manipulación ---");
            System.out.println("1. Añadir nueva palabra (al final)");
            System.out.println("2. Eliminar palabra específica");
            System.out.println("3. Mostrar lista actual");
            System.out.println("0. Guardar y Salir");
            System.out.print("Seleccione una opción: ");
            
            try {
                opcion = scanner.nextInt();
                scanner.nextLine(); // Consumir el salto de línea
                
                switch (opcion) {
                    case 1:
                        System.out.print("Ingrese la palabra a añadir: ");
                        palabra = scanner.nextLine().trim();
                        if (!palabra.isEmpty()) lista.anadirPalabra(palabra);
                        break;
                    case 2:
                        System.out.print("Ingrese la palabra a eliminar: ");
                        palabra = scanner.nextLine().trim();
                        if (!palabra.isEmpty()) lista.eliminarPalabra(palabra);
                        break;
                    case 3:
                        lista.mostrarLista();
                        break;
                    case 0:
                        System.out.println("Preparando para guardar y salir...");
                        break;
                    default:
                        System.out.println("Opción no válida. Intente de nuevo.");
                }
            } catch (java.util.InputMismatchException e) {
                System.out.println(" Entrada inválida. Por favor, ingrese un número.");
                scanner.nextLine(); // Limpiar el buffer
                opcion = -1;
            }
        } while (opcion != 0);
    }
    
    /**
     * Escribe todo el contenido actual de la lista de vuelta al archivo
     */
    private static void escribirListaAArchivo(ListaPalabras lista) {
        ArrayList<String> palabras = lista.obtenerTodasLasPalabras();
        
        System.out.println("\n Escribiendo el contenido final al archivo '" + palabras + "'...");
        
        // Usamos try-with-resources para asegurar que FileWriter se cierre
        try (FileWriter writer = new FileWriter(palabras)) {
            // Escribir las palabras separadas por un espacio
            for (int i = 0; i < palabras.size(); i++) {
                writer.write(palabras.get(i));
                // Separar por espacio, excepto después de la última palabra
                if (i < palabras.size() - 1) {
                    writer.write(" "); 
                }
            }
            System.out.println("Escritura completada. El archivo ha sido actualizado.");
            
        } catch (IOException e) {
            System.err.println("Error al escribir en el archivo: " + e.getMessage());
        }
    }
}
```

