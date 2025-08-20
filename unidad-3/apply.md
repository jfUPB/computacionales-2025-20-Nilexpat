# Unidad 3


## 🛠 Fase: Apply
## Actividad 06
### Hola Objeto: creación de un objeto en el stack

* Ejecuta el programa en C++ en modo depuración (F5) y coloca un breakpoint en la línea donde se declara Punto p(10, 20);.
  
* Paso a paso (F10), observa en la ventana de variables (Autos/Locals) los valores de x y y.
  
* En el menú Debug, selecciona Windows > Memory > Memory 1 y observa la dirección de memoria de p. Escribe en la entrada de texto de Memory 1 la dirección de memoria de p así &p y presiona Enter. Observa la dirección de memoria de p. Observa el contenido de la memoria, deberías ver algunos números en hexadecimal, tales como 0a 00 00 00 14 00 00 00.
Abre la calculadora de Windows y selecciona el modo de programador. Cambia a modo hexadecimal.

* Escribe 0a ¿Qué valor en decimal obtienes? Escribe 14 ¿Qué valor en decimal obtienes? ¿Qué observas?

con 0a me da igual a 10 y con 14 me da igual a 20 en HEX

* Nota el orden en el que están almacenados los bytes en la memoria. Observa que el byte de menor peso (menos significativo) está almacenado primero, es decir, en una dirección de memoria menor. A esto se le conocen como arquitecturas little-endian. Otro tipo de arquitectura es big-endian, donde el byte de mayor peso (más significativo) se almacena primero. La mayoría de las arquitecturas modernas son little-endian. Si la arquitectura de tu computador fuera big-endian, ¿Cómo quedarían almacenados los bytes en la memoria de p?

Muy enrredado, no entiendo.

Reflexiona sobre las siguientes cuestiones:

*¿Cuál es la diferencia entre un constructor y un destructor en C++? el constructor es una funcion que construye algo apartir de unos insumos que el requiere y retorna lo construido en una parte de la memoria, el destructor lo que hace es que se ejecuta automaticamente para borrar lo construido cuando ya cuando salga de la funcion del constructor. esto ayuda para que la memoria no se llene y cause problemas a largo plazo.

*¿Cuál es la diferencia entre un objeto y una clase en C++?

una clase es un molde que defininen como debe ser el objeto, el objeto posee caracteristicas definidas (los metodos de la clase se ejecutan en los objetos)

*¿Qué diferencia notas entre el objeto Punto en C++ y C#?
que en c++ es una copia y en C# es un referencia que apunta a la misma posicion de memoria del valor original

*¿Qué es p en C++ y qué es p en C#? (en uno de ellos p es un objeto y en el otro es una referencia a un objeto).
en C++ es una copia y en C# es una referencia.

*¿En qué parte de memoria se almacena p en C++ y en C#?
en C puede almacenarce en el stack o en el heap y en C# siempre se guarda en el heap. aqui un apunte de chat GPT

En C++

* Si declaras Punto p; → el objeto p se guarda en el stack (memoria automática).

* Si usas Punto* p = new Punto(); → el objeto está en el heap, y el puntero p en el stack.

En C#

*  Punto p = new Punto(); → el objeto siempre se guarda en el heap, y la referencia (puntero gestionado) está en el stack.

*¿Qué observaste con el depurador acerca de p? Según lo que observaste ¿Qué es un objeto en C++?

puedo intuir que un objeto ocupa un espacio de la memoria, pero la verda del resto nada.

## Actividad 07

## Actividad integradora de aplicación

Tu tarea:

Diagnóstico del problema (análisis):

Compila y ejecuta el código.

Identifica y explica con detalle al menos dos errores críticos de gestión de memoria en la clase Personaje y su uso en simularEncuentro.

Para cada error, describe:

¿Cuál es el error? No se libera la memoria de la clase personaje

¿Por qué ocurre? como no se libera memoria las estadistias del personaje siempre estaran en el heap

¿Cuál es su consecuencia? que se llene la memoria y deje de funcionar el motor

Solución y refactorización (síntesis y creación):

La solucion es crear un destructor:

```cpp
  ~Personaje() {
        delete[] estadisticas;
        std::cout << "Destructor: muere " << nombre << std::endl;
    }
```


¿Cuál es el error? Cuando se copia un personaje esta haciendo algo parecido a un paso por referencia 

¿Por qué ocurre? `Personaje copiaHeroe = heroe;` es que todos los personajes creados apuntan a la misma direccion de memoria copiando exactamen los mismos datos.

¿Cuál es su consecuencia? que cuando de implemente el destructor se eliminen todos los datos.
```
STACK                          HEAP
--------------------------------------------------
heroe                          [100][20][15]   ← estadisticas
   nombre → "Aragorn"  ──────┘
   estadisticas ──────┘

copiaHeroe
   nombre → "Copia de Aragorn"
   estadisticas ──────────────┘ (MISMA dirección)
```
----------------------------------------------------------------------------------
""como debe de ser""
```
STACK                          HEAP
--------------------------------------------------
heroe                          [100][20][15]   ← estadisticas (A)
   nombre → "Aragorn"  ──────┘
   estadisticas ──────┘

copiaHeroe                     [100][20][15]   ← estadisticas (B, nueva copia)
   nombre → "Copia de Aragorn" ──────┘
   estadisticas ──────────────┘
```

Solución y refactorización (síntesis y creación):
```
class Personaje {
public:
    std::string nombre;
    int* estadisticas;

    Personaje(std::string n, int vida, int ataque, int defensa) {
        nombre = n;
        estadisticas = new int[3];
        estadisticas[0] = vida;
        estadisticas[1] = ataque;
        estadisticas[2] = defensa;
        std::cout << "Constructor: nace " << nombre << std::endl;
    }

    // Destructor
    ~Personaje() {
        delete[] estadisticas;
        std::cout << "Destructor: muere " << nombre << std::endl;
    }

    // Constructor de copia (deep copy)
    Personaje(const Personaje& other) {
        nombre = other.nombre;
        estadisticas = new int[3];
        for (int i = 0; i < 3; i++) {
            estadisticas[i] = other.estadisticas[i];
        }
        std::cout << "Constructor de copia: nace copia de " << nombre << std::endl;
    }

    // Operador de asignación (deep copy)
    Personaje& operator=(const Personaje& other) {
        if (this != &other) {
            delete[] estadisticas; // limpiar la memoria previa
            nombre = other.nombre;
            estadisticas = new int[3];
            for (int i = 0; i < 3; i++) {
                estadisticas[i] = other.estadisticas[i];
            }
        }
        return *this;
    }

    void imprimir() {
        std::cout << "Personaje " << nombre
            << " [Vida: " << estadisticas[0]
            << ", ATK: " << estadisticas[1]
            << ", DEF: " << estadisticas[2]
            << "]" << std::endl;
    }
};
```

Re-escribe la clase Personaje para que sea segura en cuanto a memoria. Debes utilizar los conocimientos adquiridos en esta unidad y por tanto tu solución no debería usar la Regla de los tres que probablemente sea la solución que te ofrezca una IA.
Presenta el código completo de tu clase Personaje corregida.
Justificación de la Solución:






