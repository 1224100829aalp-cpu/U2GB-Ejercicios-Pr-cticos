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
            System.out.print("\n➡️ Ingrese el valor limite. Se eliminarán los nodos MAYORES a este valor: ");
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
