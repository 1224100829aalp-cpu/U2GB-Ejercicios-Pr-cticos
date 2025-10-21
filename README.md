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
## Actividad 03: Representación y Evaluación de Polinomios con Listas Enlazadas
### Nodo
```javascript
package Actividad3;

/**
 *
 * @author angellunaperez
 * Esta clase representa un término del
 * polinomio (un nodo en la lista)
 */

public class Nodo {
    public double coeficiente;
    public int exponente;
    public Nodo siguiente;

    /**
     * Constructor para crear un nuevo termino.
     *  El coeficiente numerico del término
     * El exponente entero del término
     */
    public Nodo(double coeficiente, int exponente) {
        this.coeficiente = coeficiente;
        this.exponente = exponente;
        this.siguiente = null;
    }
}
```
### PolinomioLista
```javascript
package Actividad3;

/**
 *
 * @author angellunaperez
 * En esta clase se Representa el polinomio
 * completo mediante una lista
 * enlazada simple.
*/

public class PolinomioLista {
    private Nodo cabeza;

    public PolinomioLista() {
        this.cabeza = null;
    }

    //  Tarea 2: Representación con lista enlazada (Inserción al final) 
    /**
     * Agrega un nuevo término al final de la lista.
   */
    public void agregarTermino(double coeficiente, int exponente) {
        if (coeficiente == 0) return; // No agregar términos con coeficiente cero

        Nodo nuevoNodo = new Nodo(coeficiente, exponente);

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

    // --- Tarea 3: Evaluación del polinomio ---
    /**
     * Calcula el valor del polinomio P(x) para un valor de x dado.
     * * P(x) = Sumatoria de (coeficiente * x^exponente) para todos los términos.
     * @param x El punto en el que se evalúa el polinomio.
     * @return El valor total del polinomio en ese punto.
     */
    public double evaluar(double x) {
        double resultado = 0.0;
        Nodo actual = this.cabeza;

        while (actual != null) {
            // Cálculo: coeficiente * x^exponente
            double valorTermino = actual.coeficiente * Math.pow(x, actual.exponente);
            resultado += valorTermino;
            
            actual = actual.siguiente;
        }
        return resultado;
    }

    // --- Utilidad: Mostrar el polinomio de forma legible ---
    public String toString() {
        if (this.cabeza == null) {
            return "P(x) = 0";
        }
        
        StringBuilder sb = new StringBuilder("P(x) = ");
        Nodo actual = this.cabeza;
        while (actual != null) {
            // Formateo simple para la salida
            if (actual != this.cabeza && actual.coeficiente > 0) {
                sb.append(" + ");
            } else if (actual.coeficiente < 0) {
                 sb.append(" - ");
            }

            // Manejar valor absoluto del coeficiente para no duplicar el signo
            double absCoeff = Math.abs(actual.coeficiente);
            
            if (actual.exponente == 0) {
                sb.append(absCoeff);
            } else if (actual.exponente == 1) {
                sb.append(absCoeff).append("x");
            } else {
                sb.append(absCoeff).append("x^").append(actual.exponente);
            }

            actual = actual.siguiente;
        }
        return sb.toString();
    }

}
```
### Principal 
```javascript
package Actividad3;
import java.util.Scanner;

/**
 *
 * @author angellunaperez
 * 
 * Clase principal para la entrada
 * de datos y presentación de 
 * resultados.
 * 
 */


public class Principal {
    
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        PolinomioLista polinomio = new PolinomioLista();

        // --- Tarea 1: Entrada del polinomio ---
        System.out.println("REPRESENTACIÓN Y EVALUACIÓN DE POLINOMIOS CON LISTAS ENLAZADAS");
        System.out.println("------------------------------------------------------------------");
        System.out.println("Ingrese los términos del polinomio en pares (coeficiente exponente).");
        System.out.println("Para terminar, ingrese '0 0' o una entrada vacía.");

        while (true) {
            System.out.print("Término (ej. 3 4 para 3x^4): ");
            String linea = scanner.nextLine().trim();

            if (linea.isEmpty() || linea.equals("0 0")) {
                break;
            }

            try {
                // Dividir la línea en coeficiente y exponente
                String[] partes = linea.split("\\s+"); 
                if (partes.length < 2) {
                    System.out.println("⚠️ Formato incorrecto. Intente de nuevo (ej. 5 2).");
                    continue;
                }
                
                double coef = Double.parseDouble(partes[0]);
                int exp = Integer.parseInt(partes[1]);
                
                // Tarea 2: Agregar a la lista
                polinomio.agregarTermino(coef, exp);
                
            } catch (NumberFormatException e) {
                System.out.println("⚠️ Error: Asegúrese de que el coeficiente sea un número y el exponente un entero.");
            }
        }
        
        System.out.println("\n------------------------------------------------------------------");
        System.out.println("Polinomio ingresado y representado:");
        System.out.println(polinomio.toString());
        System.out.println("------------------------------------------------------------------");


        // --- Tarea 3: Evaluación y Tabla de Valores ---
        System.out.println("\n📊 TABLA DE EVALUACIÓN P(x) de x = 0.0 hasta x = 5.0 (incremento 0.5)");
        System.out.printf("%-10s | %s%n", "x", "P(x)");
        System.out.println("-----------|-----------");

        final double VALOR_INICIO = 0.0;
        final double VALOR_FIN = 5.0;
        final double INCREMENTO = 0.5;

        for (double x = VALOR_INICIO; x <= VALOR_FIN; x += INCREMENTO) {
            // Asegurar que 5.0 se incluya a pesar de posibles errores de punto flotante
            if (x > VALOR_FIN) x = VALOR_FIN; 
            
            double resultado = polinomio.evaluar(x);
            
            // Usar formato para asegurar dos decimales para x, y dos decimales para P(x)
            System.out.printf("%-10.1f | %-10.2f%n", x, resultado);

            // Detener el bucle después de evaluar 5.0
            if (x >= VALOR_FIN) break; 
        }

        scanner.close();
    }
}
```
## Actividad 04: Polinomio con Lista Enlazada Circular
### Nodo
```javascript
package Actividad4;

/**
 *
 * @author angellunaperez
 * Esta clase usa la misma 
 * estructura de nodo que la 
 * acitivida 3 solo 
 * la forma de conexion cambia
 */

public class Nodo {
    public double coeficiente;
    public int exponente;
    public Nodo siguiente;

    public Nodo(double coeficiente, int exponente) {
        this.coeficiente = coeficiente;
        this.exponente = null; // En la circular, el enlace se gestiona en la lista
    }
}
```
### PolinomioListaCircular
```javascript
package Actividad4;
import java.util.Scanner;

/**
 *
 * @author angellunaperez
 * 
 * Esta clase representa el polinomio
 * mediante una lista enlazada circular
 */
 


public class PolinomioListaCircular {
    private Nodo ultimo; 

    public PolinomioListaCircular() {
        this.ultimo = null; // La lista inicia vacía
    }

    // --- Tarea 3: Entrada del polinomio (Insertar al final) ---
    public void agregarTermino(double coeficiente, int exponente) {
        if (coeficiente == 0) return;

        Nodo nuevoNodo = new Nodo(coeficiente, exponente);

        if (this.ultimo == null) {
            // Caso 1: Lista vacía. El nodo es el único y se apunta a sí mismo.
            this.ultimo = nuevoNodo;
            nuevoNodo.siguiente = nuevoNodo; // Tarea 2: Forma el ciclo
        } else {
            // Caso 2: Insertar después del último nodo.
            nuevoNodo.siguiente = this.ultimo.siguiente; // El nuevo nodo apunta al primero
            this.ultimo.siguiente = nuevoNodo;          // El último apunta al nuevo
            this.ultimo = nuevoNodo;                    // El nuevo nodo es ahora el último
        }
    }

    // --- Tarea 4: Recorrido circular ---
    public void recorrerYMostrar() {
        if (this.ultimo == null) {
            System.out.println("P(x) = 0 (Lista vacía)");
            return;
        }

        System.out.print("P(x) = ");
        // Tarea 4: Partir del nodo siguiente al último (es decir, el primer nodo)
        Nodo actual = this.ultimo.siguiente; 
        
        do {
            // Formato simple para la salida
            if (actual != this.ultimo.siguiente) {
                 if (actual.coeficiente > 0) {
                    System.out.print(" + ");
                } else if (actual.coeficiente < 0) {
                    System.out.print(" - ");
                }
            }

            double absCoeff = Math.abs(actual.coeficiente);
            
            if (actual.exponente == 0) {
                System.out.print(absCoeff);
            } else if (actual.exponente == 1) {
                System.out.print(absCoeff + "x");
            } else {
                System.out.print(absCoeff + "x^" + actual.exponente);
            }
            
            actual = actual.siguiente;
        } while (actual != this.ultimo.siguiente); // Tarea 4: Detener al volver al nodo inicial
        
        System.out.println();
    }
    
    // Método de utilidad para la evaluación (tomado de la actividad anterior)
    public double evaluar(double x) {
        if (this.ultimo == null) return 0.0;
        
        double resultado = 0.0;
        Nodo actual = this.ultimo.siguiente;

        do {
            resultado += actual.coeficiente * Math.pow(x, actual.exponente);
            actual = actual.siguiente;
        } while (actual != this.ultimo.siguiente);
        
        return resultado;
    }
}
```
### Principal
```javascript
package Actividad4;
import java.util.Scanner;


/**
 *
 * @author angellunaperez
 *  * Clase principal para la entrada
 * de datos y presentación de 
 * resultados.
 */

public class Principal {
    
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        // Usamos la nueva implementación circular
        PolinomioListaCircular polinomio = new PolinomioListaCircular(); 

        // --- Tarea 3: Entrada del polinomio ---
        System.out.println("POLINOMIO CON LISTA ENLAZADA CIRCULAR");
        System.out.println("------------------------------------------------------------------");
        System.out.println("Ingrese los términos (coeficiente exponente). '0 0' para terminar.");

        while (true) {
            System.out.print("Término (ej. 3 -4, 2): ");
            String linea = scanner.nextLine().trim();

            if (linea.isEmpty() || linea.equals("0 0")) {
                break;
            }

            try {
                String[] partes = linea.split("\\s+"); 
                if (partes.length < 2) continue;
                
                double coef = Double.parseDouble(partes[0]);
                int exp = Integer.parseInt(partes[1]);
                
                polinomio.agregarTermino(coef, exp); // Inserción circular
                
            } catch (NumberFormatException e) {
                System.out.println("Error: Formato de número incorrecto.");
            }
        }
        
        System.out.println("\n------------------------------------------------------------------");
        System.out.println("Polinomio representado (Recorrido Circular):");
        
        // Tarea 4: Recorrido e impresión
        polinomio.recorrerYMostrar(); 
        System.out.println("------------------------------------------------------------------");


        // --- Evaluación (Opcional, para demostrar la funcionalidad) ---
        System.out.println("\nEvaluando P(x) en x=2.0:");
        double x_val = 2.0;
        double resultado = polinomio.evaluar(x_val);
        System.out.printf("P(%.1f) = %.2f%n", x_val, resultado);

        scanner.close();
    }
}

```



