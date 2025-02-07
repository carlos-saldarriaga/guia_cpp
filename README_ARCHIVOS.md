# Guía de Manejo de Archivos en C++

## Archivos de Texto

### Conceptos Básicos
- Biblioteca necesaria: `#include <fstream>`
- Clases principales: 
  - `ofstream`: Escritura
  - `ifstream`: Lectura
  - `fstream`: Lectura y escritura

### Operaciones Básicas con Archivos de Texto

#### Abrir un Archivo
```cpp
ofstream archivo_salida("datos.txt");
ifstream archivo_entrada("datos.txt");
```

#### Verificar si se abrió correctamente
```cpp
if (!archivo_salida.is_open()) {
    cout << "Error al abrir el archivo" << endl;
    return 1;
}
```

#### Escribir en un Archivo
```cpp
ofstream archivo("datos.txt");
archivo << "Texto a escribir" << endl;
archivo << variable << endl;
```

#### Leer de un Archivo
```cpp
string linea;
ifstream archivo("datos.txt");
while (getline(archivo, linea)) {
    cout << linea << endl;
}
```

### Trabajando con Estructuras en Archivos de Texto

```cpp
struct Estudiante {
    string nombre;
    int edad;
    float promedio;
};

// Escribir estructura
void guardarEstudiante(ofstream& archivo, const Estudiante& est) {
    archivo << est.nombre << endl;
    archivo << est.edad << endl;
    archivo << est.promedio << endl;
}

// Leer estructura
Estudiante leerEstudiante(ifstream& archivo) {
    Estudiante est;
    getline(archivo, est.nombre);
    archivo >> est.edad;
    archivo >> est.promedio;
    archivo.ignore(); // Limpiar el buffer
    return est;
}
```

## Archivos Binarios

### Ventajas de los Archivos Binarios
- Más eficientes en espacio
- Más rápidos de leer/escribir
- Mantienen el formato exacto de los datos

### Operaciones con Archivos Binarios

#### Abrir en Modo Binario
```cpp
ofstream archivo("datos.bin", ios::binary);
ifstream archivo("datos.bin", ios::binary);
```

#### Escribir Estructura en Binario
```cpp
void guardarEstudianteBinario(ofstream& archivo, const Estudiante& est) {
    archivo.write(reinterpret_cast<const char*>(&est), sizeof(Estudiante));
}
```

#### Leer Estructura en Binario
```cpp
Estudiante leerEstudianteBinario(ifstream& archivo) {
    Estudiante est;
    archivo.read(reinterpret_cast<char*>(&est), sizeof(Estudiante));
    return est;
}
```

### Consideraciones Importantes para Archivos Binarios
1. No usar `string` en estructuras para archivos binarios (usar arrays de char)
2. Estructura correcta para binario:
```cpp
struct EstudianteBinario {
    char nombre[50];
    int edad;
    float promedio;
};
```

### Ejemplo Completo con Archivos Binarios
```cpp
#include <fstream>
#include <iostream>
using namespace std;

struct EstudianteBinario {
    char nombre[50];
    int edad;
    float promedio;
};

int main() {
    EstudianteBinario est = {"Juan Perez", 20, 8.5};
    
    // Escribir
    ofstream archivoSalida("estudiantes.bin", ios::binary);
    archivoSalida.write(reinterpret_cast<char*>(&est), sizeof(EstudianteBinario));
    archivoSalida.close();
    
    // Leer
    EstudianteBinario estLeido;
    ifstream archivoEntrada("estudiantes.bin", ios::binary);
    archivoEntrada.read(reinterpret_cast<char*>(&estLeido), sizeof(EstudianteBinario));
    archivoEntrada.close();
    
    cout << "Nombre: " << estLeido.nombre << endl;
    cout << "Edad: " << estLeido.edad << endl;
    cout << "Promedio: " << estLeido.promedio << endl;
    
    return 0;
}
```

### Consejos y Buenas Prácticas
1. Siempre cerrar los archivos después de usarlos
2. Verificar que el archivo se abrió correctamente
3. Usar `try-catch` para manejar errores
4. Hacer respaldo antes de escribir en archivos importantes
5. Para strings en binario, usar `char arrays` con tamaño fijo

## Aplicaciones y Operaciones Comunes

### Operaciones Principales
1. Crear (Create)
2. Leer (Read)
3. Actualizar (Update)
4. Eliminar (Delete)
5. Buscar (Search)
6. Listar (List)
7. Modificar (Modify)

### Ejemplos Banco ABC

#### 1. Guardar Socios (Escribir al Final)
```cpp
#include <fstream>
#include <iostream>
using namespace std;

int main() {
    ofstream archivo("socios.txt", ios::app);
    
    char nombre[50];
    char cedula[15];
    char ciudad[30];
    char telefono[15];
    char token[10];
    float saldo;
    
    cout << "Nombre: ";
    cin.getline(nombre, 50);
    cout << "Cedula: ";
    cin.getline(cedula, 15);
    cout << "Ciudad: ";
    cin.getline(ciudad, 30);
    cout << "Telefono: ";
    cin.getline(telefono, 15);
    cout << "Token: ";
    cin.getline(token, 10);
    cout << "Saldo inicial: ";
    cin >> saldo;
    
    archivo << nombre << "," << cedula << "," << ciudad << "," 
            << telefono << "," << token << "," << saldo << endl;
    
    archivo.close();
    return 0;
}
```

#### 2. Guardar Transacciones
```cpp
#include <fstream>
#include <iostream>
using namespace std;

int main() {
    ofstream archivo("transacciones.txt", ios::app);
    
    char cedula[15];
    char fecha[15];
    char tipo[10];
    float monto;
    float saldo;
    
    cout << "Cedula: ";
    cin.getline(cedula, 15);
    cout << "Fecha (dd/mm/yyyy): ";
    cin.getline(fecha, 15);
    cout << "Tipo (Deposito/Retiro): ";
    cin.getline(tipo, 10);
    cout << "Monto: ";
    cin >> monto;
    cout << "Saldo actual: ";
    cin >> saldo;
    
    archivo << cedula << "," << fecha << "," << tipo << "," 
            << monto << "," << saldo << endl;
    
    archivo.close();
    return 0;
}
```

#### 3. Sistema Completo Simple
```cpp
#include <fstream>
#include <iostream>
using namespace std;

void registrarSocio() {
    ofstream archivo("socios.txt", ios::app);
    char nombre[50], cedula[15], ciudad[30];
    float saldo = 0;
    
    cout << "Nombre: ";
    cin.ignore();
    cin.getline(nombre, 50);
    cout << "Cedula: ";
    cin.getline(cedula, 15);
    cout << "Ciudad: ";
    cin.getline(ciudad, 30);
    
    archivo << nombre << "," << cedula << "," << ciudad << "," << saldo << endl;
    archivo.close();
}

void realizarDeposito() {
    char cedula[15];
    float monto;
    
    cout << "Cedula: ";
    cin.ignore();
    cin.getline(cedula, 15);
    cout << "Monto a depositar: ";
    cin >> monto;
    
    ofstream transaccion("transacciones.txt", ios::app);
    transaccion << cedula << ",Deposito," << monto << endl;
    transaccion.close();
}

void mostrarSocios() {
    ifstream archivo("socios.txt");
    string linea;
    
    cout << "\nLISTA DE SOCIOS\n";
    while(getline(archivo, linea)) {
        cout << linea << endl;
    }
    archivo.close();
}

int main() {
    int opcion;
    
    do {
        cout << "\nBANCO ABC\n";
        cout << "1. Registrar Socio\n";
        cout << "2. Realizar Deposito\n";
        cout << "3. Ver Socios\n";
        cout << "4. Salir\n";
        cout << "Opcion: ";
        cin >> opcion;
        
        switch(opcion) {
            case 1: registrarSocio(); break;
            case 2: realizarDeposito(); break;
            case 3: mostrarSocios(); break;
        }
    } while(opcion != 4);
    
    return 0;
}
```
```cpp
#include <fstream>
#include <iostream>
using namespace std;

int main() {
    ofstream archivo("notas.txt", ios::app);
    
    archivo << "Juan 8.5" << endl;
    archivo << "Ana 9.0" << endl;
    
    archivo.close();
    return 0;
}
```

#### 2. Sobreescribir Todo el Archivo
```cpp
#include <fstream>
#include <iostream>
using namespace std;

int main() {
    ofstream archivo("notas.txt"); // Sin ios::app
    
    archivo << "Pedro 7.5" << endl; // Borra contenido anterior
    archivo << "Maria 8.0" << endl;
    
    archivo.close();
    return 0;
}
```

#### 3. Escribir al Principio y Final
```cpp
#include <fstream>
#include <iostream>
using namespace std;

int main() {
    // Leer contenido actual
    ifstream archivoLeer("notas.txt");
    string contenido;
    string linea;
    
    while(getline(archivoLeer, linea)) {
        contenido += linea + "\n";
    }
    archivoLeer.close();
    
    // Escribir nuevo contenido
    ofstream archivoEscribir("notas.txt");
    archivoEscribir << "INICIO DEL ARCHIVO" << endl; // Al principio
    archivoEscribir << contenido;                    // Contenido original
    archivoEscribir << "FIN DEL ARCHIVO" << endl;    // Al final
    
    archivoEscribir.close();
    return 0;
}
```

#### 4. Ejemplo con Notas de Clase
```cpp
#include <fstream>
#include <iostream>
using namespace std;

int main() {
    int opcion;
    string nombre;
    float nota;
    
    do {
        cout << "\nMENU" << endl;
        cout << "1. Agregar nota al final" << endl;
        cout << "2. Sobreescribir archivo" << endl;
        cout << "3. Ver notas" << endl;
        cout << "4. Salir" << endl;
        cout << "Opcion: ";
        cin >> opcion;
        
        switch(opcion) {
            case 1: {
                ofstream archivo("notas.txt", ios::app);
                cout << "Nombre: ";
                cin >> nombre;
                cout << "Nota: ";
                cin >> nota;
                archivo << nombre << " " << nota << endl;
                archivo.close();
                break;
            }
            
            case 2: {
                ofstream archivo("notas.txt");
                cout << "Nombre: ";
                cin >> nombre;
                cout << "Nota: ";
                cin >> nota;
                archivo << nombre << " " << nota << endl;
                archivo.close();
                break;
            }
            
            case 3: {
                ifstream archivo("notas.txt");
                cout << "\nNOTAS:" << endl;
                string linea;
                while(getline(archivo, linea)) {
                    cout << linea << endl;
                }
                archivo.close();
                break;
            }
        }
    } while(opcion != 4);
    
    return 0;
}
```
```cpp
#include <fstream>
#include <iostream>
using namespace std;

// Estructura simple para datos del estudiante
struct Estudiante {
    char nombre[30];
    int nota;
};

// Guardar estudiante en archivo
void guardarEstudiante(Estudiante estudiante) {
    ofstream archivo("notas.bin", ios::binary | ios::app);
    archivo.write((char*)&estudiante, sizeof(Estudiante));
    archivo.close();
}

// Mostrar todos los estudiantes
void mostrarEstudiantes() {
    ifstream archivo("notas.bin", ios::binary);
    Estudiante estudiante;
    
    cout << "\nLista de Estudiantes:" << endl;
    cout << "-------------------" << endl;
    
    while (archivo.read((char*)&estudiante, sizeof(Estudiante))) {
        cout << "Nombre: " << estudiante.nombre << endl;
        cout << "Nota: " << estudiante.nota << endl;
        cout << "-------------------" << endl;
    }
    archivo.close();
}

// Buscar estudiante por nombre
void buscarEstudiante(char nombre[30]) {
    ifstream archivo("notas.bin", ios::binary);
    Estudiante estudiante;
    bool encontrado = false;
    
    while (archivo.read((char*)&estudiante, sizeof(Estudiante))) {
        if (strcmp(estudiante.nombre, nombre) == 0) {
            cout << "\nEstudiante encontrado:" << endl;
            cout << "Nombre: " << estudiante.nombre << endl;
            cout << "Nota: " << estudiante.nota << endl;
            encontrado = true;
            break;
        }
    }
    
    if (!encontrado) {
        cout << "\nEstudiante no encontrado" << endl;
    }
    
    archivo.close();
}

int main() {
    int opcion;
    Estudiante estudiante;
    
    do {
        cout << "\nMENU" << endl;
        cout << "1. Agregar estudiante" << endl;
        cout << "2. Ver todos los estudiantes" << endl;
        cout << "3. Buscar estudiante" << endl;
        cout << "4. Salir" << endl;
        cout << "Elige una opcion: ";
        cin >> opcion;
        
        switch(opcion) {
            case 1:
                cout << "\nNombre del estudiante: ";
                cin.ignore();
                cin.getline(estudiante.nombre, 30);
                cout << "Nota del estudiante: ";
                cin >> estudiante.nota;
                guardarEstudiante(estudiante);
                break;
                
            case 2:
                mostrarEstudiantes();
                break;
                
            case 3:
                char nombreBuscar[30];
                cout << "\nIngrese nombre a buscar: ";
                cin.ignore();
                cin.getline(nombreBuscar, 30);
                buscarEstudiante(nombreBuscar);
                break;
        }
        
    } while(opcion != 4);
    
    return 0;
}
```

### Manejo de Errores
```cpp
try {
    ofstream archivo("datos.bin", ios::binary);
    if (!archivo) {
        throw runtime_error("Error al abrir el archivo");
    }
    // Operaciones con el archivo
    archivo.close();
} catch (const exception& e) {
    cout << "Error: " << e.what() << endl;
}
```
