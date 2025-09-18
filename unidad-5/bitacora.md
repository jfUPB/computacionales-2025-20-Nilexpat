# Bitácora de aprendizaje de la unidad 5
LINK DE LAS ACTIVIDADES: (https://juanferfranco.github.io/computacionales-2025-20/units/unit5/)

## 1.  **Diagnóstico inicial**

### Parte 1: recordando los conceptos (en C#)

En tus cursos anteriores has trabajado principalmente con C#. Basándote en esa experiencia, responde con tus propias palabras:

* ¿Qué es el encapsulamiento para ti? Describe una situación en la que te haya sido útil o donde hayas visto su importancia.

Para mi es como guardar un tipo de informacion especifica de algun objeto.

* ¿Qué es la herencia? ¿Por qué un programador decidiría usarla? Da un ejemplo simple.
  La herencia para mi es cuando un objeto abquiere los metodos de una clase madre, un programador deberia usar la herecian ya que es la mejor forma de obtimizar un programa. 

* ¿Qué es el polimorfismo? Describe con tus palabras qué significa que un código sea “polimórfico”.

  polimorfismo es la capaciadad que tiene una clase madre de tener distintas formas tipico ejemplo, la manera de que se puede crear un carro o una moto con la misma clase.

Ahora, responde a estas preguntas sobre el código:

Encapsulamiento:

Señala una línea de código que sea un ejemplo claro de encapsulamiento y explica por qué lo es.
* ¿Por qué crees que el campo nombre es private pero la propiedad Nombre es public? ¿Qué problema se evita con esto?
  
Herencia:

* ¿Cómo se evidencia la herencia en la clase Circulo?
* Un objeto de tipo Circulo, además de Radio, ¿Qué otros datos almacena en su interior gracias a la herencia?

Polimorfismo:

* Observa el bucle foreach. La variable fig es de tipo Figura, pero a veces contiene un Circulo y otras un Rectangulo. Cuando se llama a fig.Dibujar(), el programa ejecuta la versión correcta. En tu opinión,
* ¿Cómo crees que funciona esto “por debajo”? No necesitas saber la respuesta correcta, solo quiero que intentes razonar cómo podría ser.



## 2.  **La pregunta inicial**

**COSAS QUE ME GENERAN DUDAS**


* ¿como se implemetan los o se crean nuevos objetos?
* ¿como creo un objeto diferente (polimorfismo)?
* ¿que debo de tener en cuenta para crear nuevos objetos con relacion a la clase abstracta ?

## 3.  **Registro de exploración:** 

### exploracion Actividad 1

<img width="470" height="95" alt="image" src="https://github.com/user-attachments/assets/74ea82a9-a5c1-4a4c-931d-633cc69e18c4" />


Aqui observamos como se generan 3 figuras distintas con sus respectivas medidas, todas estas tienen una misma clase en comun la cual es la clase figura, luego se crean clases aparte de cada figura, estas figuras heredan la clase Figura y luego son implementadas por el main() en donde se les asignan sus valores ``misFiguras.Add(new Circulo(5.0));``

* ¿Para implementar o dibujar las figuras es necesrio crear una lista, porque y como funciona?  ``List<Figura> misFiguras = new List<Figura>();``

  Hipotesis: no tengo idea, talvez ayude con el orden, o para guardar los objetos en un espacio de la memoria, talvez con esta lista podamos tener mayor control de estos objetos en programaciones mas avanzandas y necesitemos recorrer una lista.
  
### exploracion Actividad 2

**Analisis del codigo**

Ofapp.h

En el codigo podemos observar como se crean dos clases abstractas una llamada ``Particula``(define el comportamiento de la particula y el momento en el que morira) y otra Llamada ``ExplosionParticle``(define como van a explotar las pariculas;cuadradas,circulares o estrella)

Ofapp.cpp

En este lado del codigo podemos observar como se llaman a las particulas cuando damos click y toda la logica detras de ello, aqui anotare lo importante que resuelven algunas dudas obtenidas en la actividad pasada.

primero ¿como implemento estos objetos en el codigo?: en el siguiente codigo observamos como se elige una particula entre todas las que hay ``int explosionType = (int)ofRandom(3); // 0: Circular, 1: Random, 2: Star`` luego se procede a ejecutar las particulas seleccionadas de forma aleatoria con la siguientes instrucciones ``particles.push_back(new CircularExplosion(particles[i]->getPosition(), particles[i]->getColor()));`` estas instrucciones tambien las podemos leer de la siguiente forma: creame una explosion circular y quiero que tomes la posicion y color de la particula "de tal arreglo ``[i]``".  

```cpp
if (particles[i]->shouldExplode()) {
	int explosionType = (int)ofRandom(3); // 0: Circular, 1: Random, 2: Star
	int numParticles = (int)ofRandom(20, 30);
	for (int j = 0; j < numParticles; j++) {
		if (explosionType == 0) {
			particles.push_back(new CircularExplosion(particles[i]->getPosition(), particles[i]->getColor()));
		} else if (explosionType == 1) {
			particles.push_back(new RandomExplosion(particles[i]->getPosition(), particles[i]->getColor()));
		} else {
			particles.push_back(new StarExplosion(particles[i]->getPosition(), particles[i]->getColor()));
		}
	}
	delete particles[i];
	particles.erase(particles.begin() + i);
}

```
Evidencias fotograficas
<img width="1080" height="848" alt="image" src="https://github.com/user-attachments/assets/4ab602f2-9c07-41b2-b224-6e77928fbad7" />
<img width="844" height="602" alt="image" src="https://github.com/user-attachments/assets/73256d3a-a968-4799-8d05-02eef46f4ab4" />

### exploracion Actividad 3

> 📝 **Note**  
> Profe, tuve problemas para ver la memoria no se que estoy haciendo mal, en actividades pasadas ya lo habia hecho pero en esta no me ha dejado, usare sus pantallazos como referencia.

<img width="1177" height="346" alt="image" src="https://github.com/user-attachments/assets/dd6184c3-cdd8-4f50-a823-d4f5f5be02d0" />
<img width="1183" height="341" alt="image" src="https://github.com/user-attachments/assets/83c927b6-8c66-4279-86eb-633364d54da3" />

Analizando la memoria de estos dos objetos me doy cuenta que comparten la mayoria de sus metodos, ecepto la forma en este caso el draw y la clase hija de cada una de ellas. Aqui observamos como se evidencia el polimorfismo en los objetos de una misma clase abstracta ya que son dos figuras diferentes que comparten los mismos metodos.

**COSAS QUE ME GENERAN DUDAS**

* ¿como sabe la clase ExplosionParticle cuando muere Una particula para activarse o como funciona la comunicacion entre estas dos clases abtractas?

### exploracion Actividad 4 

**ejemplo 1**

En esta activdad nos centraremos en el encapsulamiento, aqui se puede ver un ejemplo de una clase que tiene 3 variables una protegida otra privada y una publica. Esto Ocurre al ejecutar el codigo y intemos modificar desde el main una variable publica

<img width="1462" height="264" alt="image" src="https://github.com/user-attachments/assets/54821cfe-409f-413b-97ba-8d0f1c892d63" />

y esto ocurre cuando intentamos modificar una variable privada o protegida:

<img width="576" height="273" alt="image" src="https://github.com/user-attachments/assets/27e47619-f1b3-45d4-9333-887ce3701af2" />
<img width="880" height="81" alt="image" src="https://github.com/user-attachments/assets/a28ad71c-3cf7-4845-9122-2da6e34cab26" />

Mi hipotesis es que el main no puede modificar una variable privada o protegida y por ello el computador bloquea el programa.

**ejemplo 2**

<img width="853" height="89" alt="image" src="https://github.com/user-attachments/assets/10f2c316-b7a6-4bc4-b944-6b1e5aa83500" />

Como se observa no me dejo compilarlo.

**ejemplo 3**

analisis del codigo: observamos que es elo mimos ejemplo con el anterior solo que aqui cambia el main, tambien se observa como el main es capaz de engañar al encapsulamiento debido a esta parte del codigo ``reinterpret_cast`` y aqui voy a pegar las dos clases para observar las diferencias

```cpp
int main() {
    MyClass obj(42, 3.14f, 'A');
    // Esta línea causará un error de compilación
    std::cout << obj.secret1 << std::endl;

    obj.printMembers();  // Método público para mostrar los valores
    return 0;
}
```

```cpp
int main() {
    MyClass obj(42, 3.14f, 'A');

    // Usando reinterpret_cast para violar el encapsulamiento
    int* ptrInt = reinterpret_cast<int*>(&obj);
    float* ptrFloat = reinterpret_cast<float*>(ptrInt + 1);
    char* ptrChar = reinterpret_cast<char*>(ptrFloat + 1);

    // Accediendo y mostrando los valores privados
    std::cout << "Accediendo directamente a los miembros privados:\n";
    std::cout << "secret1: " << *ptrInt << "\n";       // Accede a secret1
    std::cout << "secret2: " << *ptrFloat << "\n";     // Accede a secret2
    std::cout << "secret3: " << *ptrChar << "\n";      // Accede a secret3

    return 0;
}
```

<img width="606" height="105" alt="image" src="https://github.com/user-attachments/assets/668b584a-6915-469c-b92f-50dc2e27901a" />


**COSAS QUE ME GENERAN DUDAS**

* ¿cual es la diferencia entre una variable privada y protegida?

### exploracion Actividad 5

para haredar una clase es importante que la clase asbtracta sea publica y luego escribimos otra clase que quiera heredarlo y para hacerlo debe incluir la siguiente notacion ``: public NombreDeLaClase`` un ejemplo tomado del codigo ``class RisingParticle : public Particle {...}``.

### exploracion Actividad 6

¿Qué relación existe entre los métodos virtuales y el polimorfismo? Según lo que observo, un método virtual es un método que se adapta a la función llamada.

Ejemplo:

Clase Figura (posee un método virtual llamado area).

Clase Rectángulo : public Figura (posee un método llamado area que calcula B * A).

Clase Triángulo : public Figura (posee un método llamado area que calcula (B * A) / 2).

Entonces, cuando se llama este método, se adapta a las necesidades del objeto instanciado.

## **Aplicacion**

### Actividad 7

¿Qué harás?

[] Agrega dos nuevos tipos de Particle diferentes a RisingParticle.
[] Implementar un nuevo modo de explosión.

Aqui creamos una clase para crear una explosion triangulo.

```cpp
class TriangularExplosion : public ExplosionParticle {
public:
	TriangularExplosion(const glm::vec2 & pos, const ofColor & col)
		: ExplosionParticle(pos, glm::vec2(0, 0), col, 1.2f, ofRandom(16, 32)) {
		velocity = glm::vec2(ofRandom(-150, 150), ofRandom(-150, 150));
	}

	void draw() override {
		ofSetColor(color);

		float x = position.x;
		float y = position.y;
		float r= size;
		ofDrawTriangle(

		x, y - r,
		x - r, y + r,
		x + r, y + r
		);
	}
};
```

Aqui ampliamos el rongo del random de 3->4
```cpp
int explosionType = (int)ofRandom(3); // 0: Circular, 1: Random, 2: Star, 3: triangulo
```

Aqui agregamos en el if el llamado de la clase triangulo
```cpp
for (int j = 0; j < numParticles; j++) {
	if (explosionType == 0) {
		particles.push_back(new CircularExplosion(particles[i]->getPosition(), particles[i]->getColor()));
	} else if (explosionType == 1) {
		particles.push_back(new RandomExplosion(particles[i]->getPosition(), particles[i]->getColor()));
	}else if (explosionType == 3) {
		particles.push_back(new TriangularExplosion(particles[i]->getPosition(), particles[i]->getColor()));
	}
	else {
		particles.push_back(new StarExplosion(particles[i]->getPosition(), particles[i]->getColor()));
	}
}
```

[] Reporta en tu bitácora de aprendizaje:

[] ¿Cómo y por qué de la implementación de cada una de las extensiones solicitadas al caso de estudio?
[] ¿Cómo y por qué de la implementación de los conceptos de encapsulamiento, herencia y polimorfismo en tu código?
[] Explica cómo verificaste que cada una de las extensiones funciona correctamente, muestra capturas de pantalla del depurador donde evidencias lo anterior, en particular el polimorfismo en tiempo de ejecución.

## 4.  **Consolidación, autoevaluación y cierre:**
> [!CAUTION]
> Esta sección es OBLIGATORIA y central para tu evaluación
