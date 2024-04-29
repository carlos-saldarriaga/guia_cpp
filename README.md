# Guía de Lectura y Escritura de Archivos de Texto en C++

Esta guía proporciona una introducción concisa sobre cómo leer y escribir archivos de texto en C++ utilizando la biblioteca estándar de C++.

## Inclusión de la Biblioteca

Para trabajar con archivos en C++, necesitas incluir la biblioteca `<fstream>` en tu programa:

```cpp
#include <fstream>
```

## Escritura de Archivos

Para escribir en un archivo de texto, sigue estos pasos:

1. Declara un objeto de la clase `ofstream` para representar el archivo de salida.
2. Abre el archivo utilizando el método `open()` y especifica el nombre del archivo.
3. Verifica si el archivo se abrió correctamente utilizando el método `is_open()`.
4. Escribe en el archivo utilizando el operador `<<`.
5. Cierra el archivo utilizando el método `close()`.

Ejemplo:

```cpp
#include <fstream>
#include <string>

int main() {
    std::ofstream archivo("ejemplo.txt");
    if (archivo.is_open()) {
        archivo << "Hola, mundo!" << std::endl;
        archivo << "Esta es otra línea." << std::endl;
        archivo.close();
    }
    return 0;
}
```

## Lectura de Archivos

Para leer desde un archivo de texto, sigue estos pasos:

1. Declara un objeto de la clase `ifstream` para representar el archivo de entrada.
2. Abre el archivo utilizando el método `open()` y especifica el nombre del archivo.
3. Verifica si el archivo se abrió correctamente utilizando el método `is_open()`.
4. Lee desde el archivo utilizando el operador `>>` o el método `getline()`.
5. Cierra el archivo utilizando el método `close()`.

Ejemplo de lectura línea por línea utilizando `getline()`:

```cpp
#include <fstream>
#include <string>
#include <iostream>

int main() {
    std::ifstream archivo("ejemplo.txt");
    if (archivo.is_open()) {
        std::string linea;
        while (std::getline(archivo, linea)) {
            std::cout << linea << std::endl;
        }
        archivo.close();
    }
    return 0;
}
```

Ejemplo de lectura con salto de línea utilizando el operador `>>`:

```cpp
#include <fstream>
#include <string>
#include <iostream>

int main() {
    std::ifstream archivo("ejemplo.txt");
    if (archivo.is_open()) {
        std::string palabra;
        while (archivo >> palabra) {
            std::cout << palabra << std::endl;
        }
        archivo.close();
    }
    return 0;
}
```

## Escritura y Lectura de Estructuras con Arreglo Estático

Puedes escribir y leer los datos de estructuras en un archivo de texto utilizando un arreglo estático. Aquí tienes un ejemplo:

```cpp
#include <fstream>
#include <string>
#include <cstring>
#include <iostream>

const int MAX_PERSONAS = 100;

struct Persona {
    char nombre[50];
    int edad;
};

void escribirEstructuras(const Persona* personas, int cantidad, const std::string& nombreArchivo) {
    std::ofstream archivo(nombreArchivo);
    if (archivo.is_open()) {
        archivo << cantidad << std::endl;
        for (int i = 0; i < cantidad; i++) {
            archivo << personas[i].nombre << "," << personas[i].edad << std::endl;
        }
        archivo.close();
    }
}

int leerEstructuras(Persona* personas, const std::string& nombreArchivo) {
    std::ifstream archivo(nombreArchivo);
    if (archivo.is_open()) {
        int cantidad;
        archivo >> cantidad;
        archivo.ignore();
        
        int contador = 0;
        std::string linea;
        while (std::getline(archivo, linea) && contador < cantidad) {
            std::string nombre;
            int edad;
            std::size_t pos = linea.find(',');
            if (pos != std::string::npos) {
                nombre = linea.substr(0, pos);
                edad = std::stoi(linea.substr(pos + 1));
                std::strncpy(personas[contador].nombre, nombre.c_str(), sizeof(personas[contador].nombre));
                personas[contador].edad = edad;
                contador++;
            }
        }
        archivo.close();
        return contador;
    }
    return 0;
}

int main() {
    Persona personas[MAX_PERSONAS];
    
    std::strncpy(personas[0].nombre, "Juan", sizeof(personas[0].nombre));
    personas[0].edad = 25;
    std::strncpy(personas[1].nombre, "María", sizeof(personas[1].nombre));
    personas[1].edad = 30;
    std::strncpy(personas[2].nombre, "Pedro", sizeof(personas[2].nombre));
    personas[2].edad = 40;
    
    int cantidadPersonas = 3;
    
    escribirEstructuras(personas, cantidadPersonas, "personas.txt");
    
    Persona personasLeidas[MAX_PERSONAS];
    int cantidadLeida = leerEstructuras(personasLeidas, "personas.txt");
    
    for (int i = 0; i < cantidadLeida; i++) {
        std::cout << personasLeidas[i].nombre << " - " << personasLeidas[i].edad << std::endl;
    }
    
    return 0;
}
```

En este ejemplo, se define una estructura `Persona` con los campos `nombre` y `edad`. El campo `nombre` es un arreglo de caracteres con tamaño fijo.

Se define una constante `MAX_PERSONAS` para establecer el tamaño máximo del arreglo estático de `Persona`.

La función `escribirEstructuras` toma un puntero al arreglo de `Persona`, la cantidad de personas y el nombre del archivo como parámetros. Esta función abre el archivo en modo escritura y escribe la cantidad de personas en la primera línea. Luego, itera sobre el arreglo y escribe los datos de cada `Persona` en una línea separada, utilizando una coma para separar el nombre y la edad.

La función `leerEstructuras` toma un puntero al arreglo de `Persona` y el nombre del archivo como parámetros. Esta función abre el archivo en modo lectura y lee la cantidad de personas de la primera línea. Luego, lee cada línea del archivo hasta alcanzar la cantidad de personas leídas. Utiliza la función `find` para encontrar la posición de la coma y luego utiliza `substr` para extraer el nombre y la edad. Convierte la edad de cadena a entero utilizando `stoi`. Luego, copia el nombre en el arreglo de caracteres de la estructura `Persona` utilizando `strncpy` y asigna la edad. Incrementa un contador para llevar la cuenta de las personas leídas. Finalmente, devuelve la cantidad de personas leídas.

En la función `main`, se crea un arreglo estático de `Persona` llamado `personas` con tamaño `MAX_PERSONAS`. Se asignan algunos datos de ejemplo a las primeras posiciones del arreglo.

Se llama a la función `escribirEstructuras` para escribir los datos de `personas` en el archivo "personas.txt", pasando la cantidad de personas como parámetro.

Se crea otro arreglo estático de `Persona` llamado `personasLeidas` para almacenar las personas leídas del archivo.

Se llama a la función `leerEstructuras` para leer los datos del archivo y almacenarlos en `personasLeidas`. La función devuelve la cantidad de personas leídas.

Finalmente, se itera sobre `personasLeidas` hasta la cantidad de personas leídas y se imprimen los datos de cada `Persona`.

## Manejo de Errores

Es importante manejar los errores al trabajar con archivos. Puedes verificar el estado del archivo utilizando los métodos `good()`, `eof()`, `fail()` y `bad()` de los objetos `ifstream` y `ofstream`.

Ejemplo:

```cpp
#include <fstream>
#include <iostream>

int main() {
    std::ifstream archivo("ejemplo.txt");
    if (!archivo.is_open()) {
        std::cout << "No se pudo abrir el archivo." << std::endl;
        return 1;
    }
    // Realizar operaciones de lectura
    archivo.close();
    return 0;
}
```

Esta guía cubre los conceptos básicos de lectura y escritura de archivos de texto en C++. Se han incluido ejemplos de lectura línea por línea utilizando `getline()`, lectura con salto de línea utilizando el operador `>>`, y escritura y lectura de estructuras utilizando un arreglo estático. En el último ejemplo, se muestra cómo leer la cantidad de elementos del arreglo desde la primera línea del archivo. Recuerda incluir la biblioteca `<fstream>`, abrir y cerrar los archivos correctamente, y manejar los errores adecuadamente en tus programas.
