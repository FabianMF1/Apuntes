## --- Modelo Relacional --- ##

_Se basa en: Tablas, columnas de las tablas y las filas de las tablas, que son las realaciones, atributos con sus tipos y las tuplas respectivamente._

_Es posible conectar un DBMS a los lenguajes de programacion y consultar la base de datos de forma programatica._

### Modelo de datos

_El modelo relacional consiste en almacenar datos en tablas (tuplas) y los datos semiestructurados tienen estructura jerarquica._

#### Modelo relacional

_Los datos se almacenan como tablas que tienen relaciones (las tablas), atributos (las columnas) y tuplas (las filas)._

_Para denominar las relaciones se escribe su nombre y sus tributos entre parenstesis:_

* ** Peliculas(id, nombre, categoria, calificacion)**

_El dominio se refiere al tipo de dato de los atributos_
* ** Peliculas(id:int, nombre:int, categoria:string, calificacion:float)**

_Una instancia de un esquema es un conjunto de tuplas para cada relacion del esquema (un esquema corresponde a los nombres de las columnas) y cuando se le agregan datos (tuplas) se convierte en una instancia. _

##### Restricciones de integridad

_Todas las instancias deben satisfacer las restricciones. La mas importante son las llaves, un conjunto de atributos es una llave si no existen dos tuplas para esa relacion con los mismos atributos de la llave y no hay un subconjunto de esos atributos que cumpla esa condicion, es decir, si se encuentra ese par de valores en una tupla, ese par es unico y esa tupla tambien, y no hay un conjunto menor a ese par de valores que haga lo mismo. _

_Al escribir la relacion se subrayan las llaves:_
* ** Peliculas(\_id\_, nombre, categoria, calificacion)**

_Los tipos de llaves que existen son:_

1. Super llave (superkey): cualquier conjunto de atributos que determina a todos los demas
2. Llave (candidata/minimal): cualquier conjunto de atributos que determina a todos los demas, y ninguno de sus subconjuntos es super llave.
3. Llave primaria: llave candidata que queremos destacar (la subrayada)/
4. Surrogate key: llave generica que simplifica cosas (la llave candidata con la que es mas facil trabajar).

## -- Algebra Relacional -- ##

_Lenguaje teorico que posee un conjunto de operadores que como input toman tablas y como output devuelven tablas. _

### Proyeccion (Pi)

_Dada una relacion R entonces Pi(R) es la nueva relacion que deja solo los atributos especificados en el subindice de R. Es importante destacar que este es un conjunto de tuplas, por lo que no hay duplicados entre filas, es decir, si las tuplas seleccionadas se repiten ya que no estamos selecionando alguna llave, entonces se eliminaran los repetidos. _

### Seleccion (sigma)

_En el subindice de sigma se especifica la condicion y queda sigma(R) y solo los datos que cumplen la condicion especificada se mostraran (por ejemplo columna 1 > 1). las condiciones pueden ser >, <, >=, <=, =, distinto y se pueden combinar con and , or. _

### Union (U)

_Sean R1 y R2 dos relaciones con la misma cantidad de atributos y del mismo tipo, entonces R1 U R2 es una nueva relacion que contiene la union de las tuplas de R1y R2. Recordar que si una tupla se repite solo saldra una vez y es necesario renombtrar el atributo para que tenga el mismo nombre. _

### Renombrar (ro)

_Se escribe ro((nombre -> name, categoria -> category), peliculas) y se cambiara el nombre del atributo especificado al de la derecha, al final se coloca la tabla donde queremos cambiar los atributos. Tambien sirve para cambiar el nombre de las relaciones ro(actores_jovenes, sigma_(edad<30)(actores)) y despues podemos acceder a esta nueva relacion como Pi(actores_jovenes). _

### Join

_Se define a partir del producto cruz y de seleccion, R1 join R2 con una condicion es lo mismo que sigma(condicion)(R1xR2). _

_Si los nombres de los atributos son los mismos no es necesario especificar la condicion de =. _

### Interseccion

_Si dos relaciones tienen los mismos atributos se puede generar la interseccion entre estas y se quedaran solo las tuplas que esten en ambas tablas. _

### Diferencia

_R1-R2 con los mismos atributos entrega las tuplas que estan en ambas tablas pero no en ambas a la vez. _

