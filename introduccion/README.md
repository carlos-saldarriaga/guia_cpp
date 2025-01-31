# Fundamentos de Programación en C++: Conceptos Básicos

## Índice
1. [Estructuras (struct)](#estructuras)
2. [Arreglos Unidimensionales](#arreglos)
3. [Funciones](#funciones)
4. [Variables y Alcance](#variables)
5. [Estructuras de Control](#control)
6. [Buenas Prácticas](#practicas)

## Estructuras (struct) {#estructuras}

Las estructuras son tipos de datos compuestos que permiten agrupar elementos de diferentes tipos bajo un mismo nombre.

### Características de las Estructuras

- Permiten crear tipos de datos personalizados
- Pueden contener diferentes tipos de datos
- Los elementos dentro de una estructura se llaman miembros
- Cada miembro puede ser accedido usando el operador punto (.)

### Sintaxis Básica

```cpp
struct NombreEstructura {
    tipo1 miembro1;
    tipo2 miembro2;
    tipo3 miembro3;
};
```

### Ejemplo de Uso

```cpp
struct Persona {
    string nombre;
    int edad;
    double altura;
};

// Crear una variable de tipo Persona
Persona persona1;
persona1.nombre = "Ana";
persona1.edad = 25;
persona1.altura = 1.65;

// Inicialización directa
Persona persona2 = {"Juan", 30, 1.75};
```

## Arreglos Unidimensionales {#arreglos}

Los arreglos son estructuras de datos que permiten almacenar múltiples elementos del mismo tipo en posiciones de memoria contiguas.

### Características de los Arreglos

- Tamaño fijo definido en la declaración
- Índice base 0
- Elementos del mismo tipo
- Acceso directo a elementos por índice

### Declaración y Uso

```cpp
// Declaración
tipo nombreArreglo[tamaño];

// Ejemplos
int numeros[5] = {1, 2, 3, 4, 5};
int valores[3];  // Sin inicializar

// Acceso a elementos
numeros[0] = 10;  // Modificar primer elemento
int x = numeros[1];  // Obtener segundo elemento
```

### Arreglos de Estructuras
```cpp
struct Producto {
    string nombre;
    double precio;
};

Producto inventario[100];  // Arreglo de 100 productos
inventario[0].nombre = "Laptop";
inventario[0].precio = 999.99;
```

### Recorrido de Arreglos
```cpp
// Usando for
for (int i = 0; i < 5; i++) {
    cout << numeros[i] << " ";
}

// Recorrer arreglo de estructuras
for (int i = 0; i < 100; i++) {
    cout << inventario[i].nombre << ": $";
    cout << inventario[i].precio << endl;
}
```

## Funciones {#funciones}

Las funciones son bloques de código reutilizable que realizan una tarea específica.

### Tipos de Funciones

#### Funciones sin Retorno (void)
```cpp
void saludar() {
    cout << "¡Hola mundo!" << endl;
}
```

#### Funciones con Retorno
```cpp
int sumar(int a, int b) {
    return a + b;
}
```

### Paso de Parámetros

#### Por Valor
```cpp
void modificarNumero(int x) {
    x = x + 1;  // No modifica la variable original
}
```

#### Por Referencia
```cpp
void modificarNumero(int& x) {
    x = x + 1;  // Modifica la variable original
}
```

### Funciones con Arreglos
```cpp
void mostrarArreglo(int arr[], int tamano) {
    for (int i = 0; i < tamano; i++) {
        cout << arr[i] << " ";
    }
}
```

## Variables y Alcance {#variables}

### Variables Globales

- Declaradas fuera de todas las funciones
- Accesibles desde cualquier parte del programa
- Usar con moderación

```cpp
int variableGlobal = 10;  // Variable global

void funcion() {
    variableGlobal++;  // Acceso a variable global
}
```

### Variables Locales

- Declaradas dentro de una función o bloque
- Solo accesibles dentro de su bloque
- Preferibles sobre variables globales

```cpp
void funcion() {
    int variableLocal = 5;  // Solo existe dentro de funcion()
}
```

### Constantes

```cpp
const int MAX_ELEMENTOS = 100;  // Constante global
const double PI = 3.14159;
```

## Estructuras de Control {#control}

### Estructura switch

```cpp
switch (expresion) {
    case valor1:
        // código
        break;
    case valor2:
        // código
        break;
    default:
        // código por defecto
}
```

### Bucles

#### Bucle for
```cpp
for (int i = 0; i < 10; i++) {
    cout << i << " ";
}
```

#### Bucle while
```cpp
int i = 0;
while (i < 10) {
    cout << i << " ";
    i++;
}
```

#### Bucle do-while
```cpp
int opcion;
do {
    cout << "Menu:\n";
    cout << "1. Opción 1\n";
    cout << "2. Salir\n";
    cin >> opcion;
} while (opcion != 2);
```

## Buenas Prácticas {#practicas}

### Nomenclatura
- Usar nombres descriptivos
- Seguir una convención consistente
- Evitar nombres de una sola letra (excepto en bucles)

### Organización del Código
- Mantener funciones cortas y con un solo propósito
- Agrupar código relacionado
- Usar comentarios para explicar el código complejo

### Manejo de Errores
- Validar entrada de usuarios
- Verificar índices de arreglos
- Manejar casos especiales

### Indentación y Formato
- Usar indentación consistente
- Dejar espacios entre operadores
- Usar llaves de manera consistente

### Documentación
```cpp
/**
 * Descripción de la función
 * @param parametro1 descripción del parámetro 1
 * @return descripción del valor retornado
 */
tipo funcion(tipo parametro1) {
    // código
}
```

### Tips de Depuración
1. Usar cout para debug
2. Verificar valores límite
3. Probar casos especiales
4. Dividir problemas grandes en partes más pequeñas


# Sistema de Gestión de Biblioteca

Este ejemplo práctico implementa un sistema básico para gestionar los préstamos de libros en una biblioteca. El sistema permite registrar libros, usuarios y préstamos, además de generar estadísticas básicas.

## Estructuras Utilizadas

### Estructura Libro
```cpp
struct Libro {
    string titulo;
    string autor;
    int anioPublicacion;
    bool disponible;
    int vecesPrestado;
};
```

### Estructura Usuario
```cpp
struct Usuario {
    string nombre;
    string id;
    int librosPrestados;
    bool activo;
};
```

## Variables Globales
```cpp
const int MAX_LIBROS = 100;
const int MAX_USUARIOS = 50;

Libro biblioteca[MAX_LIBROS];
Usuario usuarios[MAX_USUARIOS];
int totalLibros = 0;
int totalUsuarios = 0;
```

## Funciones Principales

### Registro de Libros
```cpp
void registrarLibro() {
    if (totalLibros >= MAX_LIBROS) {
        cout << "La biblioteca está llena" << endl;
        return;
    }

    Libro nuevoLibro;
    cout << "Ingrese título: ";
    cin.ignore();
    getline(cin, nuevoLibro.titulo);
    
    cout << "Ingrese autor: ";
    getline(cin, nuevoLibro.autor);
    
    cout << "Ingrese año de publicación: ";
    cin >> nuevoLibro.anioPublicacion;
    
    nuevoLibro.disponible = true;
    nuevoLibro.vecesPrestado = 0;
    
    biblioteca[totalLibros] = nuevoLibro;
    totalLibros++;
    
    cout << "Libro registrado exitosamente" << endl;
}
```

### Registro de Usuarios
```cpp
void registrarUsuario() {
    if (totalUsuarios >= MAX_USUARIOS) {
        cout << "No se pueden registrar más usuarios" << endl;
        return;
    }

    Usuario nuevoUsuario;
    cout << "Ingrese nombre: ";
    cin.ignore();
    getline(cin, nuevoUsuario.nombre);
    
    cout << "Ingrese ID: ";
    getline(cin, nuevoUsuario.id);
    
    nuevoUsuario.librosPrestados = 0;
    nuevoUsuario.activo = true;
    
    usuarios[totalUsuarios] = nuevoUsuario;
    totalUsuarios++;
    
    cout << "Usuario registrado exitosamente" << endl;
}
```

### Préstamo de Libros
```cpp
void prestarLibro() {
    string idUsuario, tituloLibro;
    
    cout << "Ingrese ID del usuario: ";
    cin.ignore();
    getline(cin, idUsuario);
    
    // Buscar usuario
    int indiceUsuario = -1;
    for (int i = 0; i < totalUsuarios; i++) {
        if (usuarios[i].id == idUsuario && usuarios[i].activo) {
            indiceUsuario = i;
            break;
        }
    }
    
    if (indiceUsuario == -1) {
        cout << "Usuario no encontrado o inactivo" << endl;
        return;
    }
    
    cout << "Ingrese título del libro: ";
    getline(cin, tituloLibro);
    
    // Buscar libro
    int indiceLibro = -1;
    for (int i = 0; i < totalLibros; i++) {
        if (biblioteca[i].titulo == tituloLibro && biblioteca[i].disponible) {
            indiceLibro = i;
            break;
        }
    }
    
    if (indiceLibro == -1) {
        cout << "Libro no encontrado o no disponible" << endl;
        return;
    }
    
    // Realizar préstamo
    biblioteca[indiceLibro].disponible = false;
    biblioteca[indiceLibro].vecesPrestado++;
    usuarios[indiceUsuario].librosPrestados++;
    
    cout << "Préstamo realizado exitosamente" << endl;
}
```

### Estadísticas de la Biblioteca
```cpp
void mostrarEstadisticas() {
    // Libro más prestado
    int maxPrestamos = 0;
    string libroMasPrestado;
    
    for (int i = 0; i < totalLibros; i++) {
        if (biblioteca[i].vecesPrestado > maxPrestamos) {
            maxPrestamos = biblioteca[i].vecesPrestado;
            libroMasPrestado = biblioteca[i].titulo;
        }
    }
    
    // Cantidad de libros disponibles
    int librosDisponibles = 0;
    for (int i = 0; i < totalLibros; i++) {
        if (biblioteca[i].disponible) {
            librosDisponibles++;
        }
    }
    
    // Usuario con más préstamos
    int maxLibrosPrestados = 0;
    string usuarioMasPrestamos;
    
    for (int i = 0; i < totalUsuarios; i++) {
        if (usuarios[i].librosPrestados > maxLibrosPrestados) {
            maxLibrosPrestados = usuarios[i].librosPrestados;
            usuarioMasPrestamos = usuarios[i].nombre;
        }
    }
    
    cout << "\n=== Estadísticas de la Biblioteca ===" << endl;
    cout << "Libro más prestado: " << libroMasPrestado << " (" << maxPrestamos << " veces)" << endl;
    cout << "Libros disponibles: " << librosDisponibles << " de " << totalLibros << endl;
    cout << "Usuario con más préstamos: " << usuarioMasPrestamos << " (" << maxLibrosPrestados << " libros)" << endl;
}
```

### Menú Principal
```cpp
int main() {
    int opcion;
    
    do {
        cout << "\n=== SISTEMA DE BIBLIOTECA ===" << endl;
        cout << "1. Registrar libro" << endl;
        cout << "2. Registrar usuario" << endl;
        cout << "3. Prestar libro" << endl;
        cout << "4. Ver estadísticas" << endl;
        cout << "5. Salir" << endl;
        cout << "Seleccione una opción: ";
        cin >> opcion;
        
        switch (opcion) {
            case 1:
                registrarLibro();
                break;
            case 2:
                registrarUsuario();
                break;
            case 3:
                prestarLibro();
                break;
            case 4:
                mostrarEstadisticas();
                break;
            case 5:
                cout << "¡Hasta luego!" << endl;
                break;
            default:
                cout << "Opción inválida" << endl;
        }
    } while (opcion != 5);
    
    return 0;
}
```

## Conceptos Demostrados

1. **Estructuras**: 
   - Uso de struct para Libro y Usuario
   - Campos de diferentes tipos en cada estructura

2. **Arreglos**:
   - Arreglos de estructuras (biblioteca[] y usuarios[])
   - Control de índices y límites

3. **Funciones**:
   - Funciones sin retorno (void)
   - Manipulación de estructuras en funciones
   - Búsqueda en arreglos

4. **Variables Globales**:
   - Constantes para límites
   - Arreglos globales
   - Contadores globales

5. **Entrada/Salida**:
   - Uso de cin y cout
   - Manejo de strings con getline

6. **Estructuras de Control**:
   - Switch para el menú
   - Bucles for para búsquedas
   - Control de flujo con if-else
