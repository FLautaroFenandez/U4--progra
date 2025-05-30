# U4--progra
Unidad 4 - Ordenamiento
/*
UNIDAD 4 - ESTRUCTURAS DE DATOS Y ALGORITMOS EN C
--------------------------------------------------

ORDENAMIENTO
La ordenación consiste en organizar los elementos de un arreglo en un orden específico:
- Ascendente (menor a mayor)
- Descendente (mayor a menor)
*/

/* METODO BURBUJA (BUBBLE SORT)
   Compara elementos vecinos e intercambia si están en mal orden.
   Repite muchas veces hasta que todo esté ordenado. */

void bubbleSort(int arr[], int n) {
    int i, j, temp;
    for (i = 0; i < n-1; i++) {
        for (j = 0; j < n-i-1; j++) {
            if (arr[j] > arr[j+1]) {
                temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
            }
        }
    }
}

/* METODO SELECCION (SELECTION SORT)
   Busca el mínimo y lo pone adelante. Repite con el resto. */

void selectionSort(int arr[], int n) {
    int i, j, min_idx, temp;
    for (i = 0; i < n-1; i++) {
        min_idx = i;
        for (j = i+1; j < n; j++) {
            if (arr[j] < arr[min_idx])
                min_idx = j;
        }
        temp = arr[min_idx];
        arr[min_idx] = arr[i];
        arr[i] = temp;
    }
}

/* METODO INSERCION (INSERTION SORT)
   Como ordenar cartas en la mano: vas insertando cada una en su lugar correcto. */

void insertionSort(int arr[], int n) {
    int i, key, j;
    for (i = 1; i < n; i++) {
        key = arr[i];
        j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j+1] = arr[j];
            j--;
        }
        arr[j+1] = key;
    }
}

/*
LISTAS EN C
Una lista es una estructura dinámica (puede crecer y achicarse). Se hace con structs y punteros.
Tipos:
- Lista simplemente enlazada
- Lista doblemente enlazada
- Lista circular
*/

#include <stdio.h>
#include <stdlib.h>

// Lista simplemente enlazada: cada nodo apunta al siguiente

typedef struct Nodo {
    int dato;
    struct Nodo* siguiente;
} Nodo;

// Insertar al inicio de la lista
void insertarAlInicio(Nodo** cabeza, int valor) {
    Nodo* nuevo = (Nodo*) malloc(sizeof(Nodo));
    nuevo->dato = valor;
    nuevo->siguiente = *cabeza;
    *cabeza = nuevo;
}

// Mostrar la lista completa
void mostrarLista(Nodo* cabeza) {
    Nodo* actual = cabeza;
    while (actual != NULL) {
        printf("%d -> ", actual->dato);
        actual = actual->siguiente;
    }
    printf("NULL\n");
}

/*
ESTRUCTURAS (STRUCT)
Sirven para crear tipos de datos personalizados.
Ej: un alumno tiene nombre, edad y promedio. */

struct Alumno {
    char nombre[50];
    int edad;
    float promedio;
};

/*
BUSQUEDA BINARIA
Solo funciona si el arreglo está ORDENADO.
Divide el arreglo en mitades y busca de forma más rápida que una búsqueda común. */

int busquedaBinaria(int arr[], int izquierda, int derecha, int objetivo) {
    while (izquierda <= derecha) {
        int medio = izquierda + (derecha - izquierda) / 2;

        if (arr[medio] == objetivo)
            return medio; // Elemento encontrado

        if (arr[medio] < objetivo)
            izquierda = medio + 1;
        else
            derecha = medio - 1;
    }
    return -1; // No encontrado
}

/*
CADENAS Y ARREGLOS
- Una cadena es un arreglo de caracteres.
- Un arreglo guarda elementos del mismo tipo, uno al lado del otro en memoria. */

#include <string.h>
void usarCadena() {
    char nombre[20] = "Juan";
    printf("Hola %s\n", nombre);
}

/*
EJEMPLO DE TODO JUNTO EN MAIN
*/

int main() {
    // Ordenamiento
    int arreglo[5] = {5, 2, 8, 3, 1};
    bubbleSort(arreglo, 5);

    printf("Arreglo ordenado: ");
    for (int i = 0; i < 5; i++) printf("%d ", arreglo[i]);
    printf("\n");

    // Lista
    Nodo* lista = NULL;
    insertarAlInicio(&lista, 10);
    insertarAlInicio(&lista, 20);
    mostrarLista(lista);

    // Búsqueda binaria
    int resultado = busquedaBinaria(arreglo, 0, 4, 3);
    if (resultado != -1) printf("Elemento 3 encontrado en la posicion %d\n", resultado);
    else printf("Elemento no encontrado\n");

    // Struct
    struct Alumno a1 = {"Pedro", 19, 8.5};
    printf("Alumno: %s, Edad: %d, Promedio: %.2f\n", a1.nombre, a1.edad, a1.promedio);

    usarCadena();

    return 0;
}
