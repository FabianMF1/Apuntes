## Disco Duro, RAM y DBMS

_Los records de las bases datos se almacenan en paginas de disco. Y  cuando sea necesario, las paginas se traen a la memoria principal (buffer). _

_Para trabajar con las tuplas de una relacion, la base de datos carga la pagina con la tupla desde el disco, para cargar estas paginas, la base de datos reserva un espacio en RAM llamado buffer. _

_Lo mas lento del DBMS es ir a buscar los datos del disco, por lo que se quiere minimizar el numero de veces que se hace esto._

_El mayor costo es trar las paginas del disco duro a la RAM. _

_El costo de I/O es el numero de paginas llevadas a la memoria para responder una consulta. _

## Indices

_Herramientas que optimizan el acceso a los datos para una consulta o un conjunto de estas. _

CREATE INDEX <nombre índice> ON table <atributo>

Supongamos que tengo la tabla:

Usuarios(uid: int PRIMARY KEY,
nombre: text,
edad: int)

en donde tenemos indexada la tabla por la primary
key, que es el atributo uid

El índice normalmente es una colección de archivos
que puede ir completo en memoria

Si hacemos la consulta:

SELECT * FROM Usuarios WHERE uid = 104

esta se resolverá con el índice, así evitaremos recorrer
toda la tabla

Search Key: es el parámetro con el que busco algo
en mi índice (por ejemplo, el uid de una tabla de
usuarios)

Data Entry: la tupla que nos retorna el índice después
de preguntar por una Search Key en particular

## Tablas de Hash

Iniciamos un número fijo de casilleros (buckets)

Cada tupla va a parar a un casillero según su id

Para esto utilizamos una función de hash.

Una función de hash es simplemente una función h
que lleva elementos de un conjunto U a otro
conjunto M (los casilleros/buckets)

En general, suponemos que las funciones de hash
distribuyen uniforme

También suponemos que hay suficientes casilleros para
que la búsqueda se haga en 1 paso (o no mucho más)

### Hash Index

_Intentar replicar lo mismo en una base de datos. Ahora se insertan las tuplas a una base de datos, puede ocurrir un overflow para lo que se crea un overflow page. _

Para una relación R y un atributo A
  N páginas de disco sirven de buckets
  Cada bucket cuenta con una lista ligada de overflow pages
  Usamos una función de hash h que me indicará que bucket le corresponde a cada valor:

h: dominio(A) → [0, …, N - 1]

## B+ Tree Index

Es un índice basado en un árbol:
• Las páginas del disco representan nodos del árbol
• Las tuplas están en las hojas
• Provee un tiempo de búsqueda logarítmico
• Se comporta bien en consultas de rango
• Es el índice que usa Postgres sobre las llaves
primarias (y en general, todos los sistemas)

Importante: para facilitar inserción de datos nuevos
los B+ trees no tienen nodos completamente llenos

El costo de busqueda el log(R)

Hablaremos de un índice Clustered si al preguntarle
por un valor me retorna una tupla, se conoce como indice primario.

Hablaremos de un índice Unclustered si me retorna
un puntero, se conoce como indice secundario.

