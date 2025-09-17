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
  
### exploracion Activida 2

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

### exploracion Activida 3

> 📝 **Note**  
> Profe, tuve problemas para ver la memoria no se que estoy haciendo mal, en actividades pasadas ya lo habia hecho pero en esta no me ha dejado, usare sus pantallazos como referencia.

<img width="1177" height="346" alt="image" src="https://github.com/user-attachments/assets/dd6184c3-cdd8-4f50-a823-d4f5f5be02d0" />
<img width="1183" height="341" alt="image" src="https://github.com/user-attachments/assets/83c927b6-8c66-4279-86eb-633364d54da3" />

Analizando la memoria de estos dos objetos me doy cuenta que comparten la mayoria de sus metodos, ecepto la forma en este caso el draw y la clase hija de cada una de ellas. Aqui observamos como se evidencia el polimorfismo en los objetos de una misma clase abstracta ya que son dos figuras diferentes que comparten los mismos metodos.



**COSAS QUE ME GENERAN DUDAS**

* ¿como sabe la clase ExplosionParticle cuando muere Una particula para activarse o como funciona la comunicacion entre estas dos clases abtractas?

* Aquí documentas cada ciclo de pregunta -> hipótesis -> experimento -> hallazgo -> reflexión.
* Debe ser rico en evidencia visual (código, capturas del depurador con anotaciones, diagramas).

## 4.  **Consolidación, autoevaluación y cierre:**
> [!CAUTION]
> Esta sección es OBLIGATORIA y central para tu evaluación
