# Actividades-en-clase
Ejercicio 1

import java.util.Scanner;

/**
 * Implementación de una calculadora básica por consola
 * que maneja las cuatro operaciones aritméticas fundamentales.
 */
public class CalculadoraConsola {
    private static final Scanner entrada = new Scanner(System.in);
    
    public static void main(String[] args) {
        try {
            double primerNumero = leerNumero("Ingrese el primer número: ");
            double segundoNumero = leerNumero("Ingrese el segundo número: ");
            char operacion = leerOperacion();
            
            double resultado = calcular(primerNumero, segundoNumero, operacion);
            mostrarResultado(resultado);
        } catch (Exception e) {
            System.out.println("Error: " + e.getMessage());
        } finally {
            entrada.close();
        }
    }
    
    /**
     * Lee un número real desde la consola con el mensaje especificado
     * @param mensaje Texto que se muestra al usuario antes de la lectura
     * @return El número real ingresado
     * @throws IllegalArgumentException Si el valor ingresado no es un número válido
     */
    public static double leerNumero(String mensaje) {
        System.out.print(mensaje);
        while (true) {
            try {
                String valor = entrada.nextLine().trim();
                return Double.parseDouble(valor);
            } catch (NumberFormatException e) {
                System.out.print("Valor no válido. Ingrese un número: ");
            }
        }
    }
    
    /**
     * Solicita y valida una operación aritmética
     * @return El carácter correspondiente a la operación seleccionada
     */
    public static char leerOperacion() {
        while (true) {
            System.out.print("Ingrese la operación (+, -, *, /): ");
            String operacion = entrada.nextLine().trim();
            
            if (operacion.length() == 1) {
                char op = operacion.charAt(0);
                if (op == '+' || op == '-' || op == '*' || op == '/') {
                    return op;
                }
            }
            System.out.println("Operación no válida. Intente nuevamente.");
        }
    }
    
    /**
     * Realiza la operación aritmética solicitada
     * @param a Primer operando
     * @param b Segundo operando
     * @param op Operación a realizar
     * @return El resultado de la operación
     * @throws ArithmeticException Si se intenta dividir por cero
     * @throws IllegalArgumentException Si la operación no es reconocida
     */
    public static double calcular(double a, double b, char op) {
        switch (op) {
            case '+': return a + b;
            case '-': return a - b;
            case '*': return a * b;
            case '/': 
                if (b == 0) {
                    throw new ArithmeticException("No se puede dividir por cero");
                }
                return a / b;
            default:
                throw new IllegalArgumentException("Operación no soportada: " + op);
        }
    }
    
    /**
     * Muestra el resultado con precisión de dos decimales
     * @param resultado Valor a mostrar
     */
    public static void mostrarResultado(double resultado) {
        System.out.printf("Resultado: %.2f%n", resultado);
    }
}

Ejercicio 2

import java.util.Scanner;

/**
 * Utilidades para el procesamiento de cadenas de texto
 */
public class ProcesadorCadenas {
    private static final Scanner entrada = new Scanner(System.in);
    
    public static void main(String[] args) {
        String texto = leerCadena("Ingrese una cadena de texto: ");
        
        System.out.println("Número de vocales: " + contarVocales(texto));
        System.out.println("Cadena invertida: " + invertirCadena(texto));
        
        String esPalindromo = esPalindromo(texto) ? "Sí" : "No";
        System.out.println("¿Es palíndromo?: " + esPalindromo);
        
        entrada.close();
    }
    
    /**
     * Lee una cadena de texto desde la consola
     * @param mensaje Texto que se muestra al usuario
     * @return La cadena ingresada
     */
    public static String leerCadena(String mensaje) {
        System.out.print(mensaje);
        return entrada.nextLine();
    }
    
    /**
     * Cuenta el número de vocales en una cadena
     * @param s Cadena a procesar
     * @return Cantidad de vocales encontradas
     */
    public static int contarVocales(String s) {
        if (s == null || s.isEmpty()) {
            return 0;
        }
        
        int contador = 0;
        String vocales = "aeiouáéíóúàèìòùäëïöüAEIOUÁÉÍÓÚÀÈÌÒÙÄËÏÖÜ";
        
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (vocales.indexOf(c) != -1) {
                contador++;
            }
        }
        
        return contador;
    }
    
    /**
     * Invierte una cadena de texto sin usar funciones de alto nivel
     * @param s Cadena a invertir
     * @return Cadena invertida
     */
    public static String invertirCadena(String s) {
        if (s == null) {
            return null;
        }
        
        char[] caracteres = s.toCharArray();
        char[] resultado = new char[caracteres.length];
        
        for (int i = 0; i < caracteres.length; i++) {
            resultado[i] = caracteres[caracteres.length - 1 - i];
        }
        
        return new String(resultado);
    }
    
    /**
     * Verifica si una cadena es palíndroma
     * @param s Cadena a verificar
     * @return true si es palíndromo, false en caso contrario
     */
    public static boolean esPalindromo(String s) {
        if (s == null) {
            return false;
        }
        
        // Normalizar: quitar espacios y convertir a minúsculas
        String limpia = s.toLowerCase().replaceAll("\\s+", "");
        
        // También podríamos eliminar acentos para un análisis más flexible
        
        int inicio = 0;
        int fin = limpia.length() - 1;
        
        while (inicio < fin) {
            if (limpia.charAt(inicio) != limpia.charAt(fin)) {
                return false;
            }
            inicio++;
            fin--;
        }
        
        return true;
    }
}

Ejercicio 3

import java.util.Random;

/**
 * Clase para el análisis estadístico de arrays de enteros
 */
public class AnalizadorEstadistico {
    private static final Random rnd = new Random();
    
    public static void main(String[] args) {
        // Ejemplo de uso con array de 10 elementos con valores entre 0 y 100
        int[] numeros = generarArray(10, 100);
        
        System.out.println("Array generado:");
        mostrarArray(numeros);
        
        System.out.printf("Media: %.2f%n", calcularMedia(numeros));
        System.out.println("Máximo: " + encontrarMaximo(numeros));
        System.out.println("Mínimo: " + encontrarMinimo(numeros));
        System.out.printf("Desviación estándar: %.4f%n", calcularDesviacionEstandar(numeros));
    }
    
    /**
     * Genera un array de enteros aleatorios
     * @param n Longitud del array
     * @param maxValor Valor máximo posible (inclusivo)
     * @return Array de enteros aleatorios
     * @throws IllegalArgumentException Si n es negativo o maxValor es negativo
     */
    public static int[] generarArray(int n, int maxValor) {
        if (n < 0) {
            throw new IllegalArgumentException("La longitud del array no puede ser negativa");
        }
        if (maxValor < 0) {
            throw new IllegalArgumentException("El valor máximo no puede ser negativo");
        }
        
        int[] resultado = new int[n];
        for (int i = 0; i < n; i++) {
            resultado[i] = rnd.nextInt(maxValor + 1);
        }
        
        return resultado;
    }
    
    /**
     * Calcula la media aritmética de un array de enteros
     * @param arr Array a analizar
     * @return Media aritmética
     * @throws IllegalArgumentException Si el array está vacío
     */
    public static double calcularMedia(int[] arr) {
        if (arr == null || arr.length == 0) {
            throw new IllegalArgumentException("El array no puede estar vacío");
        }
        
        long suma = 0;
        for (int valor : arr) {
            suma += valor;
        }
        
        return (double) suma / arr.length;
    }
    
    /**
     * Encuentra el valor máximo en un array de enteros
     * @param arr Array a analizar
     * @return Valor máximo
     * @throws IllegalArgumentException Si el array está vacío
     */
    public static int encontrarMaximo(int[] arr) {
        if (arr == null || arr.length == 0) {
            throw new IllegalArgumentException("El array no puede estar vacío");
        }
        
        int max = arr[0];
        for (int i = 1; i < arr.length; i++) {
            if (arr[i] > max) {
                max = arr[i];
            }
        }
        
        return max;
    }
    
    /**
     * Encuentra el valor mínimo en un array de enteros
     * @param arr Array a analizar
     * @return Valor mínimo
     * @throws IllegalArgumentException Si el array está vacío
     */
    public static int encontrarMinimo(int[] arr) {
        if (arr == null || arr.length == 0) {
            throw new IllegalArgumentException("El array no puede estar vacío");
        }
        
        int min = arr[0];
        for (int i = 1; i < arr.length; i++) {
            if (arr[i] < min) {
                min = arr[i];
            }
        }
        
        return min;
    }
    
    /**
     * Calcula la desviación estándar de un array de enteros
     * @param arr Array a analizar
     * @return Desviación estándar
     * @throws IllegalArgumentException Si el array tiene menos de dos elementos
     */
    public static double calcularDesviacionEstandar(int[] arr) {
        if (arr == null || arr.length < 2) {
            throw new IllegalArgumentException("Se necesitan al menos dos elementos para calcular la desviación estándar");
        }
        
        double media = calcularMedia(arr);
        double sumaCuadrados = 0;
        
        for (int valor : arr) {
            double diferencia = valor - media;
            sumaCuadrados += diferencia * diferencia;
        }
        
        return Math.sqrt(sumaCuadrados / (arr.length - 1));
    }
    
    /**
     * Método auxiliar para mostrar el contenido de un array
     */
    private static void mostrarArray(int[] arr) {
        if (arr == null || arr.length == 0) {
            System.out.println("[]");
            return;
        }
        
        System.out.print("[");
        for (int i = 0; i < arr.length; i++) {
            System.out.print(arr[i]);
            if (i < arr.length - 1) {
                System.out.print(", ");
            }
        }
        System.out.println("]");
    }
}

Ejercicio 4

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.NoSuchElementException;

/**
 * Sistema de gestión de inventario para productos
 */
public class GestorInventario {
    private Map<Integer, Producto> productos;
    
    public GestorInventario() {
        this.productos = new HashMap<>();
    }
    
    public static void main(String[] args) {
        GestorInventario gestor = new GestorInventario();
        
        // Agregar algunos productos de ejemplo
        gestor.agregarProducto(new Producto(1, "Laptop", 5, 1200.00));
        gestor.agregarProducto(new Producto(2, "Mouse", 15, 25.50));
        gestor.agregarProducto(new Producto(3, "Teclado", 8, 45.75));
        gestor.agregarProducto(new Producto(4, "Monitor", 3, 150.99));
        
        // Ejemplo de uso
        try {
            gestor.registrarEntrada(2, 5);
            gestor.registrarSalida(1, 2);
            
            System.out.printf("Valor total del inventario: $%.2f%n", gestor.calcularValorTotal());
            
            List<Producto> bajoStock = gestor.listarProductosBajoStock(5);
            System.out.println("\nProductos con stock bajo (≤ 5):");
            for (Producto p : bajoStock) {
                System.out.printf("ID: %d, Nombre: %s, Cantidad: %d%n", 
                                p.getId(), p.getNombre(), p.getCantidad());
            }
        } catch (Exception e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
    
    /**
     * Agrega un nuevo producto al inventario
     * @param producto Producto a agregar
     * @throws IllegalArgumentException Si ya existe un producto con el mismo ID
     */
    public void agregarProducto(Producto producto) {
        if (producto == null) {
            throw new IllegalArgumentException("El producto no puede ser nulo");
        }
        
        if (productos.containsKey(producto.getId())) {
            throw new IllegalArgumentException("Ya existe un producto con ID " + producto.getId());
        }
        
        productos.put(producto.getId(), producto);
    }
    
    /**
     * Registra una entrada de stock para un producto
     * @param id ID del producto
     * @param cantidad Cantidad a agregar (debe ser positiva)
     * @throws NoSuchElementException Si no existe el producto
     * @throws IllegalArgumentException Si la cantidad es inválida
     */
    public void registrarEntrada(int id, int cantidad) {
        if (cantidad <= 0) {
            throw new IllegalArgumentException("La cantidad debe ser positiva");
        }
        
        Producto producto = buscarProducto(id);
        producto.setCantidad(producto.getCantidad() + cantidad);
    }
    
    /**
     * Registra una salida de stock para un producto
     * @param id ID del producto
     * @param cantidad Cantidad a retirar (debe ser positiva)
     * @throws NoSuchElementException Si no existe el producto
     * @throws IllegalStateException Si no hay suficiente stock
     * @throws IllegalArgumentException Si la cantidad es inválida
     */
    public void registrarSalida(int id, int cantidad) {
        if (cantidad <= 0) {
            throw new IllegalArgumentException("La cantidad debe ser positiva");
        }
        
        Producto producto = buscarProducto(id);
        
        if (producto.getCantidad() < cantidad) {
            throw new IllegalStateException(
                "Stock insuficiente. Disponible: " + producto.getCantidad());
        }
        
        producto.setCantidad(producto.getCantidad() - cantidad);
    }
    
    /**
     * Calcula el valor monetario total del inventario
     * @return Valor total
     */
    public double calcularValorTotal() {
        double total = 0;
        
        for (Producto p : productos.values()) {
            total += p.getCantidad() * p.getPrecioUnitario();
        }
        
        return total;
    }
    
    /**
     * Lista los productos con stock menor o igual al umbral
     * @param umbral Cantidad máxima para considerar stock bajo
     * @return Lista de productos con stock bajo
     * @throws IllegalArgumentException Si el umbral es negativo
     */
    public List<Producto> listarProductosBajoStock(int umbral) {
        if (umbral < 0) {
            throw new IllegalArgumentException("El umbral no puede ser negativo");
        }
        
        List<Producto> resultado = new ArrayList<>();
        
        for (Producto p : productos.values()) {
            if (p.getCantidad() <= umbral) {
                resultado.add(p);
            }
        }
        
        return resultado;
    }
    
    /**
     * Busca un producto por su ID
     * @param id ID del producto
     * @return El producto encontrado
     * @throws NoSuchElementException Si no existe el producto
     */
    private Producto buscarProducto(int id) {
        Producto producto = productos.get(id);
        
        if (producto == null) {
            throw new NoSuchElementException("No existe un producto con ID " + id);
        }
        
        return producto;
    }
}

/**
 * Clase que representa un producto en el inventario
 */
class Producto {
    private int id;
    private String nombre;
    private int cantidad;
    private double precioUnitario;
    
    /**
     * Constructor para crear un nuevo producto
     * @param id Identificador único
     * @param nombre Nombre del producto
     * @param cantidad Cantidad inicial en stock
     * @param precioUnitario Precio por unidad
     */
    public Producto(int id, String nombre, int cantidad, double precioUnitario) {
        if (id <= 0) {
            throw new IllegalArgumentException("El ID debe ser un número positivo");
        }
        if (nombre == null || nombre.trim().isEmpty()) {
            throw new IllegalArgumentException("El nombre no puede estar vacío");
        }
        if (cantidad < 0) {
            throw new IllegalArgumentException("La cantidad no puede ser negativa");
        }
        if (precioUnitario <= 0) {
            throw new IllegalArgumentException("El precio debe ser positivo");
        }
        
        this.id = id;
        this.nombre = nombre;
        this.cantidad = cantidad;
        this.precioUnitario = precioUnitario;
    }
    
    // Getters y setters
    
    public int getId() {
        return id;
    }
    
    public String getNombre() {
        return nombre;
    }
    
    public void setNombre(String nombre) {
        if (nombre == null || nombre.trim().isEmpty()) {
            throw new IllegalArgumentException("El nombre no puede estar vacío");
        }
        this.nombre = nombre;
    }
    
    public int getCantidad() {
        return cantidad;
    }
    
    public void setCantidad(int cantidad) {
        if (cantidad < 0) {
            throw new IllegalArgumentException("La cantidad no puede ser negativa");
        }
        this.cantidad = cantidad;
    }
    
    public double getPrecioUnitario() {
        return precioUnitario;
    }
    
    public void setPrecioUnitario(double precioUnitario) {
        if (precioUnitario <= 0) {
            throw new IllegalArgumentException("El precio debe ser positivo");
        }
        this.precioUnitario = precioUnitario;
    }
}
