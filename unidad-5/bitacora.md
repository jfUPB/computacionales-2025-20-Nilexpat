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

En el codigo podemos observar como se crean dos clases abstractas una llamada ``Particula``(define el comportamiento de la particula y el momento en el que morira) y otra Llamada ``ExplosionParticle``(define como van a explotar las pariculas;cuadradas,circulares o estrella)

**COSAS QUE ME GENERAN DUDAS**

* ¿como sabe la clase ExplosionParticle cuando muere Una particula para activarse o como funciona la comunicacion entre estas dos clases abtractas?

> Aquí documentas cada ciclo de pregunta -> hipótesis -> experimento -> hallazgo -> reflexión.
> Debe ser rico en evidencia visual (código, capturas del depurador con anotaciones, diagramas).

## 4.  **Consolidación, autoevaluación y cierre:**
> [!CAUTION]
> Esta sección es OBLIGATORIA y central para tu evaluación
