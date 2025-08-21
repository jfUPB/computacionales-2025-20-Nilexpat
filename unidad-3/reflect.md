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
