## NoSQL

Término común para denominar bases de datos con:
• Menos restricciones que el modelo relacional
• Menos esquema
• Menos garantías de consistencia
• Más adecuadas para la distribución

Dos problemas fundamentales:

1. Datos no caben en un computador
2. Servidores pueden fallar

Para el primero se pueden fragmentar los datos y para el segundo se pueden replicar los datos.

Garantías en un entorno distribuido
Tres propiedades fundamentales:
• Consistency (todos los usuarios ven lo mismo)
• Availability (todas las consultas siempre reciben una
respuesta, aunque sea errónea)
• Partition tolerance (el sistema funciona bien pese a estar
físicamente dividido)

Estos sistemas toleran un poco mas las fallas.

### Teorema CAP

Plantea que para una base de datos distribuida es imposible
mantener simultáneamente estas tres características:

• Consistency
• Availablity
• Partition tolerance

Hay que elegir entre consistency y availablity. Estos son los sistemas CP y AP.

### BASE

En la práctica, sistemas distribuidos fijan el P, y balancean entre
C y A, sin elegir uno exclusivamente.
Paradigma BASE:
• Basically Available
• Soft state
• Eventually consistent

### Tipos de BDD NoSQL

• BD key-value
• BD de grafos
• BD de documentos

#### BD Key - Value

Independientemente del esquema

• Arquitectura almacena información por medio de
pares
• Cada par tiene una llave (identificador) y un valor

Operaciones cruciales:
• put(key,value)
• get(key)
• delete(key)

Son grandes tablas de hash persistentes

• Esta categoría es difusa, pues muchas de las aplicaciones de
otros tipos de BD usan key - value y hashing hasta cierto
punto.

#### BD de Grafos y RDF

Especializadas para guardar relaciones

• En general, almacenan sus datos como property graphs
• Algunos ejemplos son Neo4J, Virtuoso, Jena, Blazegraph

#### BD Orientadas a Documentos

Especializadas en documentos

• CouchDB, MongoDB (estas y otras BD almacenan sus
datos en documentos JSON)
• JSON no es el único estándar de documentos (por
ejemplo, existe también XML)

Parecidas a key-value stores:

• El valor es ahora un documento (JSON)
• Pueden agrupar documentos (colecciones)
• Lenguaje de consultas mucho más poderoso

### JSON

Su nombre viene de JavaScript Object Notation

Estándar de intercambio de datos semiestructurados /
datos en la Web

• JSON se acopla muy bien a los lenguajes de
programación

La base son los pares key - value

Los objetos se escriben entre {} y contienen una cantidad
arbitraria de pares key - value

{
    nombre": “Matías”, “apellido": “Jünemann”
    }

Los arreglos se escriben entre [] y contienen valores

{
“profesores”: [
  {“nombre”: “Juan”, “apellido": “Reutter”},
  {“nombre”: “Cristian”, “apellido": “Riveros”},
  {“nombre”: “Marcelo”, “apellido": “Arenas”}
]
}

SQL:
• Esquema de datos
• Lenguajes de consulta independientes del código

JSON:
• Más flexible, no hay que respetar necesariamente un
esquema
• Más tipos de datos (como arreglos)
• Human - Readable

### BD de documentos

Qué hacen bien:

• Si quiero lista de alumnos de un curso
• Si quiero nombres de todos los cursos
• Si quiero todo los cursos tomados por David

Muy útiles a la hora de desplegar información en la web

Qué hacen mal:

• Manejo de información que cambia mucho
• Cruce de información no trivial

En resumen:

BD de documentos:
• Útiles para despliegue de información estática
• Búsquedas simples
• Cruces muy sencillos

BD SQL:
• Información cambia mucho
• Tengo que hacer cruces cada rato
• Necesito ACID

### Consultando a MongoDB

show dbs … muestra bases de datos disponibles
use dbName … ahora usamos base de datos dbName
show collections … colecciones en nuestra base de datos
db.colName.find() … todos los documentos en la colección colName
db.colName.find().pretty() … pretty print
db.colName.find({"name": "Adrian"}) … selección
db.colName.find({"age": {$gte:23}}) … selección
db.colName.find({"age": {$gte:23}},{"name":1}) … proyección

Text Search en MongoDB:

Un índice especial … permite búsqueda rápida de texto

db.colName.createIndex({"attributeName":"text"})
db.users.find({$text: {$search: "Delantero de Cobreloa"}})

