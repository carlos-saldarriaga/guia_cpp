# Matrices en C++

En este README, exploraremos el concepto de matrices en C++ y cómo utilizarlas en nuestros programas. Las matrices son estructuras de datos fundamentales que nos permiten almacenar y manipular conjuntos de valores del mismo tipo en una disposición rectangular de filas y columnas.

## ¿Qué es una matriz?

Una matriz es una estructura de datos que consta de una colección de elementos del mismo tipo organizados en filas y columnas. Cada elemento de la matriz se accede mediante dos índices: uno para la fila y otro para la columna. Las matrices nos permiten almacenar y trabajar con conjuntos de datos relacionados de manera eficiente.

## Declaración de una matriz

Para declarar una matriz en C++, debemos especificar el tipo de datos de los elementos, seguido del nombre de la matriz y el tamaño de la matriz entre corchetes. La sintaxis general es la siguiente:

```cpp
tipo_de_dato nombre_de_matriz[número_de_filas][número_de_columnas];
```

Por ejemplo, para declarar una matriz de enteros de tamaño 3x3, utilizaríamos el siguiente código:

```cpp
int matriz[3][3];
```

## Inicialización de una matriz

Podemos inicializar una matriz en el momento de la declaración utilizando una lista de valores entre llaves. Los valores se asignan a los elementos de la matriz en orden de filas y columnas. Por ejemplo:

```cpp
int matriz[3][3] = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
```

En este caso, la matriz `matriz` se inicializa con los valores 1, 2, 3 en la primera fila, 4, 5, 6 en la segunda fila y 7, 8, 9 en la tercera fila.

## Acceso a los elementos de una matriz

Para acceder a un elemento específico de una matriz, utilizamos los índices de fila y columna. Los índices comienzan desde cero, por lo que el primer elemento se encuentra en la posición [0][0]. Por ejemplo, para acceder al elemento en la segunda fila y tercera columna de la matriz `matriz`, utilizaríamos `matriz[1][2]`.

Ejemplo de acceso a elementos de una matriz:

```cpp
int valor = matriz[1][2];  // Obtiene el valor en la segunda fila y tercera columna
matriz[0][0] = 10;         // Asigna el valor 10 al primer elemento de la matriz
```

## Recorrido de una matriz

A menudo necesitamos recorrer todos los elementos de una matriz para realizar operaciones o cálculos. Podemos utilizar bucles anidados para recorrer las filas y columnas de la matriz. Por ejemplo:

```cpp
// Recorrido de una matriz
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        cout << matriz[i][j] << " ";
    }
    cout << endl;
}
```

En este ejemplo, utilizamos dos bucles `for` anidados para recorrer todas las filas y columnas de la matriz `matriz`. El bucle externo `i` representa las filas y el bucle interno `j` representa las columnas. Imprimimos cada elemento de la matriz seguido de un espacio y utilizamos `endl` para pasar a la siguiente línea después de cada fila.

## Ejemplo completo

A continuación, se muestra un ejemplo completo que demuestra la declaración, inicialización y recorrido de una matriz en C++:

```cpp
#include <iostream>
using namespace std;

int main() {
    // Declaración e inicialización de una matriz
    int matriz[3][3] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    // Acceso a elementos de la matriz
    cout << "Elemento en la segunda fila y tercera columna: " << matriz[1][2] << endl;

    // Modificación de un elemento de la matriz
    matriz[0][0] = 10;

    // Recorrido de la matriz
    cout << "Matriz completa:" << endl;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << matriz[i][j] << " ";
        }
        cout << endl;
    }

    return 0;
}
```

Este programa declara una matriz `matriz` de tamaño 3x3 y la inicializa con valores. Luego, accede al elemento en la segunda fila y tercera columna y lo imprime. A continuación, modifica el primer elemento de la matriz asignándole el valor 10. Finalmente, recorre la matriz completa utilizando bucles anidados e imprime cada elemento seguido de un espacio, pasando a la siguiente línea después de cada fila.

La salida del programa sería:

```
Elemento en la segunda fila y tercera columna: 6
Matriz completa:
10 2 3
4 5 6
7 8 9
```


# Sistema de Reservas de Asientos de Cine

Imagina que estás desarrollando un sistema de reservas de asientos para un cine. El cine tiene una sala con 5 filas y 10 asientos por fila. Puedes utilizar una matriz para representar la disposición de los asientos y realizar operaciones como reservar asientos, cancelar reservas y mostrar el estado actual de la sala.

A continuación, te muestro un ejemplo de cómo puedes implementar este sistema utilizando matrices en C++:

```cpp
#include <iostream>
using namespace std;

const int FILAS = 5;
const int COLUMNAS = 10;

// Función para mostrar el estado actual de la sala
void mostrarSala(char sala[FILAS][COLUMNAS]) {
    cout << "Estado actual de la sala:" << endl;
    for (int i = 0; i < FILAS; i++) {
        for (int j = 0; j < COLUMNAS; j++) {
            cout << sala[i][j] << " ";
        }
        cout << endl;
    }
}

// Función para reservar un asiento
void reservarAsiento(char sala[FILAS][COLUMNAS], int fila, int columna) {
    if (fila >= 0 && fila < FILAS && columna >= 0 && columna < COLUMNAS) {
        if (sala[fila][columna] == 'O') {
            sala[fila][columna] = 'X';
            cout << "Asiento reservado correctamente." << endl;
        } else {
            cout << "El asiento ya está reservado." << endl;
        }
    } else {
        cout << "Asiento inválido." << endl;
    }
}

// Función para cancelar una reserva de asiento
void cancelarReserva(char sala[FILAS][COLUMNAS], int fila, int columna) {
    if (fila >= 0 && fila < FILAS && columna >= 0 && columna < COLUMNAS) {
        if (sala[fila][columna] == 'X') {
            sala[fila][columna] = 'O';
            cout << "Reserva cancelada correctamente." << endl;
        } else {
            cout << "El asiento no está reservado." << endl;
        }
    } else {
        cout << "Asiento inválido." << endl;
    }
}

int main() {
    char sala[FILAS][COLUMNAS];

    // Inicializar la sala con asientos disponibles ('O')
    for (int i = 0; i < FILAS; i++) {
        for (int j = 0; j < COLUMNAS; j++) {
            sala[i][j] = 'O';
        }
    }

    // Ejemplo de uso del sistema de reservas
    mostrarSala(sala);

    reservarAsiento(sala, 2, 5);
    reservarAsiento(sala, 1, 3);
    reservarAsiento(sala, 4, 7);

    mostrarSala(sala);

    cancelarReserva(sala, 1, 3);

    mostrarSala(sala);

    return 0;
}
```

En este ejemplo, utilizamos una matriz `sala` de caracteres para representar la disposición de los asientos en la sala de cine. Inicialmente, todos los asientos están disponibles y se representan con el carácter 'O'.

Definimos funciones como `mostrarSala` para mostrar el estado actual de la sala, `reservarAsiento` para reservar un asiento específico y `cancelarReserva` para cancelar una reserva existente.

En la función `main`, inicializamos la sala con asientos disponibles y luego realizamos algunas operaciones de ejemplo, como reservar asientos, mostrar el estado de la sala y cancelar una reserva.

La salida del programa sería:

```
Estado actual de la sala:
O O O O O O O O O O
O O O O O O O O O O
O O O O O O O O O O
O O O O O O O O O O
O O O O O O O O O O
Asiento reservado correctamente.
Asiento reservado correctamente.
Asiento reservado correctamente.
Estado actual de la sala:
O O O O O O O O O O
O O O X O O O O O O
O O O O O X O O O O
O O O O O O O O O O
O O O O O O O X O O
Reserva cancelada correctamente.
Estado actual de la sala:
O O O O O O O O O O
O O O O O O O O O O
O O O O O X O O O O
O O O O O O O O O O
O O O O O O O X O O
```

Este es solo un ejemplo básico de cómo se pueden utilizar matrices en un sistema de reservas de asientos de cine. Puedes extender este ejemplo agregando más funcionalidades, como la selección interactiva de asientos por parte del usuario, el cálculo de estadísticas de ocupación, etc.



## Conclusión

Las matrices son una estructura de datos fundamental en C++ que nos permite almacenar y manipular conjuntos de valores relacionados. Podemos declarar matrices especificando el tipo de datos y el tamaño, inicializarlas con valores, acceder a elementos individuales utilizando índices de fila y columna, y recorrer la matriz utilizando bucles anidados.

Con las matrices, podemos representar y trabajar con datos bidimensionales de manera eficiente en nuestros programas. Son ampliamente utilizadas en una variedad de aplicaciones, como el procesamiento de imágenes, los juegos, las hojas de cálculo y más.

Recuerda que los índices de las matrices comienzan desde cero y que debemos tener cuidado al acceder a los elementos para evitar errores de índice fuera de rango.

