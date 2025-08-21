# Unidad 3


## 🤔 Fase: Reflect

## Actividad 11
## Parte 1: recuperación de conocimiento (Retrieval Practice)

Explica con tus propias palabras qué es el stack y qué es el heap en C++.

el stack es un espacio de la memoria que guarda infomacion como funciones o variables locales, esta parte de la memoria es automatisada lo que entra se libera, en cambio el heap es un espacio en donde se guarda cosas como new y delete esta si tiene que eliminarse manualmente.

Describe las tres formas de pasar parámetros a una función en C++ (valor, referencia y puntero). Para cada una, explica qué sucede en memoria y cuándo usarías cada método.

* el paso por referencia modifica la variable original / esta la implementaria si necesito cambiar la varible original
* el paso por valor crea una copia dela variable original / esta la implementaria cuando quisiera cambiar la variable original.
* y un puntero sirve para modificar los valores internos de una direccion de memoria ya creada/ (consultando mas a profundidad para no quedar con la duda) Chat gpt me recomienda usar punteros para modificar variables dentro de un array.

¿Qué diferencia hay entre una variable local, una variable global y una variable local estática? ¿En qué segmento del mapa de memoria se almacena cada una?

la variable local se guarda en el stack, la global y la estatica en variables globales y estaticas

Explica qué es un objeto en C++ desde la perspectiva de memoria. ¿Dónde se almacenan los miembros de instancia y dónde los miembros estáticos?

un objeto es un molde con metodos que recibe parametros que cumplan con los requisitos, estos parametros pueden usar esos metodos, los metodos y funciones se guardan en el heap y el retorno creo que los puede guardar en el stack ya que es una parte de la memoria mas agil y se encarga de limpiar la memoria automaticamente.

## Codigo Problematico

```cpp
#include <iostream>
#include <string>

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

    void imprimir() {
        std::cout << "Personaje " << nombre
            << " [Vida: " << estadisticas[0]
            << ", ATK: " << estadisticas[1]
            << ", DEF: " << estadisticas[2]
            << "]" << std::endl;
    }
};

void simularEncuentro() {
    std::cout << "\n--- Iniciando encuentro ---" << std::endl;
    Personaje heroe("Aragorn", 100, 20, 15);

    Personaje copiaHeroe = heroe;
    copiaHeroe.nombre = "Copia de Aragorn";

    std::cout << "Saliendo del encuentro..." << std::endl;
}

int main() {
    simularEncuentro();
    std::cout << "\nSimulación terminada." << std::endl;
    return 0;
}
```

## Tu tarea:

Diagnóstico del problema (análisis): 

El codigo presenta fallas en su memoria, las funciones de constructor hay que liberarlas manualmente ya que se crean en el heap, tambien tiene fallas a la hora de querer guardar los datos de los dintintos personajes que se crean, ya que existe un puntero que hace que todo los personajes compartan exactamente lo mismo, y si implementamos un destructor la memoria se corrompera ya que todo esta ligado a una mimas posicion de memoria, en cambio si realisas una funcion de paso por valor en vez de un puntero puedes corregir este erro, el cual no modificara el espacio de memoria original.

* Compila y ejecuta el código.

Identifica y explica con detalle al menos dos errores críticos de gestión de memoria en la clase Personaje y su uso en simularEncuentro.

* Para cada error, describe:

*¿Cuál es el error? No existe un destructor que libere la memoria

*¿Por qué ocurre? porque las funciones entran en el estado de memoria heap y este no tiene la capacidad de liberar su memoria automaticamente.

*¿Cuál es su consecuencia? Que el programa empiece a ir lento, porque se llene la memoria.
Solución y refactorización (síntesis y creación):

crear un destructor para borrar (estadisticas)
```cpp
~Personaje() {
    delete[] estadisticas;
    std::cout << "Destructor: se destruye " << nombre << std::endl;
}
```

* ¿Cuál es el error? No existe un metodo que copie la varible estadisticas, todo se esta guardando en la misma posicion de memori.

* ¿Por qué ocurre? porque la funcion del puntero no es coiar, es posicionarse en una parte de la memoria en especifica.

* ¿Cuál es su consecuencia? que todos los personajes creados compartan la misma posicion de memoria.

* Solución y refactorización (síntesis y creación):

 hay que crear una funcion de paso por valor que nos ayude a duplicar la varible Estadisticas, para ello es importante tener en cuenta que tambien debemos reservar un nuevo espacio para estas variables new estadisticas.

 ```cpp
Personaje( Personaje& n){
// hasta aqui llego mi logica.
}

```

* Re-escribe la clase Personaje para que sea segura en cuanto a memoria. Debes utilizar los conocimientos adquiridos en esta unidad y por tanto tu solución no debería usar la Regla de los tres que probablemente sea la solución que te ofrezca una IA.
Presenta el código completo de tu clase Personaje corregida.

```cpp
#include <iostream>
#include <string>
#include <iostream>
#include <string>

class Personaje {
public:
    std::string nombre;
    int* estadisticas;

    // el puntero de estadisticas esta apuntando al mismo espacio de la memoria que las
	  // las estadisticas del personaje original, por ende es mas recomendable crear una copia 
    // por paso por valor.

    Personaje( Personaje& otro) {
   // algo que pueda duplicar las estadisticas
        }
     
    }

// Implementamos un destuctor para limpiar la memoria del Heap 

    // Destructor para liberar la memoria dinamica
    ~Personaje() {
        delete[] estadisticas;
        std::cout << "Destructor: se destruye " << nombre << std::endl;
    }
	// si queremos que el constructor haga una copia, debemos implementar un constructor de copia. ya que el puntero estadisticas es un          //puntero a memoria dinamica.lo que significa que ambos objetos compartirán el mismo espacio de memoria para las estadisticas.

    Personaje(std::string n, int vida, int ataque, int defensa) {
        nombre = n;
        estadisticas = new int[3];
        estadisticas[0] = vida;
        estadisticas[1] = ataque;
        estadisticas[2] = defensa;
        std::cout << "Constructor: nace " << nombre << std::endl;
    }

	// aqui hace falta el destructor, porque el constructor reserva memoria dinamica.

    void imprimir() {
        std::cout << "Personaje " << nombre
            << " [Vida: " << estadisticas[0]
            << ", ATK: " << estadisticas[1]
            << ", DEF: " << estadisticas[2]
            << "]" << std::endl;
    }
};

void simularEncuentro() {
    std::cout << "\n--- Iniciando encuentro ---" << std::endl;
    Personaje heroe("Aragorn", 100, 20, 15);

    Personaje copiaHeroe = heroe;
    copiaHeroe.nombre = "Copia de Aragorn";

    std::cout << "Saliendo del encuentro..." << std::endl;
}

int main() {
    simularEncuentro();
    std::cout << "\nSimulación terminada." << std::endl;
    return 0;
}
```

