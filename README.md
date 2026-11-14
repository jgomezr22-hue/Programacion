# Programacion
import java.util.ArrayDeque;
import java.util.ArrayList;
import java.util.List;
import java.util.Queue;

public class GrafoNoDirigido {
    private final int[][] matrizAdyacencia;

    public GrafoNoDirigido(int numeroVertices) {
        if (numeroVertices < 0) {
            throw new IllegalArgumentException("El número de vértices no puede ser negativo.");
        }
        matrizAdyacencia = new int[numeroVertices][numeroVertices];
    }

    public void agregarArista(int origen, int destino) {
        validarVertice(origen);
        validarVertice(destino);
        matrizAdyacencia[origen][destino] = 1;
        matrizAdyacencia[destino][origen] = 1;
    }

    public void imprimirMatriz() {
        System.out.print("   ");
        for (int i = 0; i < matrizAdyacencia.length; i++) {
            System.out.printf("%2d ", i);
        }
        System.out.println();

        for (int fila = 0; fila < matrizAdyacencia.length; fila++) {
            System.out.printf("%2d ", fila);
            for (int columna = 0; columna < matrizAdyacencia.length; columna++) {
                System.out.printf("%2d ", matrizAdyacencia[fila][columna]);
            }
            System.out.println();
        }
    }

    public List<Integer> bfs(int inicio) {
        validarVertice(inicio);
        List<Integer> recorrido = new ArrayList<>();
        boolean[] visitado = new boolean[matrizAdyacencia.length];
        Queue<Integer> cola = new ArrayDeque<>();

        visitado[inicio] = true;
        cola.add(inicio);

        while (!cola.isEmpty()) {
            int actual = cola.remove();
            recorrido.add(actual);

            for (int vecino = 0; vecino < matrizAdyacencia.length; vecino++) {
                if (matrizAdyacencia[actual][vecino] == 1 && !visitado[vecino]) {
                    visitado[vecino] = true;
                    cola.add(vecino);
                }
            }
        }

        return recorrido;
    }

    public List<Integer> dfs(int inicio) {
        validarVertice(inicio);
        List<Integer> recorrido = new ArrayList<>();
        boolean[] visitado = new boolean[matrizAdyacencia.length];
        dfsDesde(inicio, visitado, recorrido);
        return recorrido;
    }

    private void dfsDesde(int actual, boolean[] visitado, List<Integer> recorrido) {
        visitado[actual] = true;
        recorrido.add(actual);

        for (int vecino = 0; vecino < matrizAdyacencia.length; vecino++) {
            if (matrizAdyacencia[actual][vecino] == 1 && !visitado[vecino]) {
                dfsDesde(vecino, visitado, recorrido);
            }
        }
    }

    private void validarVertice(int vertice) {
        if (vertice < 0 || vertice >= matrizAdyacencia.length) {
            throw new IndexOutOfBoundsException("Vértice fuera de rango: " + vertice);
        }
    }

    public static void main(String[] args) {
        GrafoNoDirigido grafo = new GrafoNoDirigido(6);
        grafo.agregarArista(0, 1);
        grafo.agregarArista(0, 2);
        grafo.agregarArista(1, 3);
        grafo.agregarArista(1, 4);
        grafo.agregarArista(2, 4);
        grafo.agregarArista(3, 5);
        grafo.agregarArista(4, 5);

        System.out.println("Matriz de adyacencia:");
        grafo.imprimirMatriz();
        System.out.println("Recorrido BFS desde 0: " + grafo.bfs(0));
        System.out.println("Recorrido DFS desde 0: " + grafo.dfs(0));
    }
}

El programa fue desarrollado en Java utilizando Visual Studio Code con la asistencia del modo Agente de GitHub Copilot y modela un grafo no dirigido de 6 vértices (numerados del 0 al 5):   Matriz de Adyacencia: Se empleó una matriz bidimensional de enteros de tamaño times 6 para representar las conexiones entre vértices. Al tratarse de un grafo no dirigido, la matriz es simétrica respecto a su diagonal principal: cada vez que se agrega una arista entre dos nodos u y v, se asigna el valor 1 tanto en la posición [u][v] como en [v][u] para reflejar la bidireccionalidad de la conexión.   Algoritmo BFS (Búsqueda en Anchura): Recorre el grafo por niveles partiendo desde el vértice inicial (0). Utiliza una estructura de datos tipo cola (Queue) para encolar y visitar primero todos los vecinos adyacentes directos antes de pasar al siguiente nivel de profundidad, apoyándose en un arreglo booleano de nodos visitados para evitar ciclos. Como resultado de la ejecución, se obtuvo el recorrido [0, 1, 2, 3, 4, 5].   Algoritmo DFS (Búsqueda en Profundidad): Explora cada rama del grafo avanzando lo más profundo posible por los nodos adyacentes no visitados antes de retroceder (backtracking). Se implementó de forma recursiva aprovechando la pila de llamadas del sistema y llevando el registro de vértices visitados, obteniendo como salida la secuencia [0, 1, 3, 5, 4, 2].   
<img width="309" height="194" alt="image" src="https://github.com/user-attachments/assets/772200d9-3e83-46b8-ac19-2d58a8864f48" />
