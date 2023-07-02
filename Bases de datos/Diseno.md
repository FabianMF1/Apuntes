## Diagrama E/R

_Las entidades se representan con rectangulos, los atributos con ovalos y las relaciones con rombos._

_Cada entidad debe tener una llave._

_Las relaciones se construyen mediante las llaves de las entidades participantes, es decir, la llave de la relacion son las llaves de las entidades. _

### Multiplicidades

1. n a n quiere decir que se relacionan 0 o mas entidades con 0 o mas entidades.
2. n a  o 1, quiere decir que de una entidad se relaciona a lo mas con una de la otra y que la otra entidad puede relacionarse varias veces con la primera
3. 0 o 1 a n, quiere decir que la primera entidad se puede relacionar varias veces con la segunda y la segunda se puede relacionar a lo mas una ves con la primera.
4. 0 o 1 0 o 1, quiere decir que ambas entidades se pueden relacionar a lo mas una ves con la otra (en ambos sentidos se tiene a lo mas 1)

### Relaciones multiples

_Se puede utilizar una relacion multiple para ser mas conciso con el diagrama, es decir, una relacion con mas de dos entidades es mas concisa, pero un diagrama que solo utiliza relaciones binarias es mas flexivble. _

### Jerarquia de clases

_Se representan con un triangulo que conecta la superclase con la subclase. Las subclases no pueden tener llaves pero si atributos nuevos. _

### Entidades debiles

_Se encierran en una linea de mayor grosor que los demas elementos y corresponden a las entidades cuya llave depende de la llave de otra entidad. _

### Agregacion

_Se encapusla la relacion y sus entidades correspondientes en una entidad virtual._

## Transformar el modelo E/R al modelo relacional

1. Las llaves de las entidades involucradas en una relacion forman una super llave para esa relacion.
2. Se crea la tabla y ya tenemos anotado el nombre de esta en el diagrama junto con sus atributos y su llave..
3. Para las relaciones estas se crean con las dos llaves de las entidades que relaciona y se marca cada una por separado como FOREIGN KEY(llave1) REFERENCES <Tabla(llavetabla)> y la llave primaria como el par que contiene ambas llaves.

_Es importante destacar que no se pueden insertar valores donde la llave foranea no esta en la tabla referenciada (no se puede si la tabla referenciada no contiene el valor). _

_Lo mismo si se borra una tupla que contiene una llave foranea referenciada en la otra tabla, por default no se permite la eliminacion, pero tambien se puede propagar la eliminacion (tambien se elimina la tupla referenciada) o se deja la llave con el valor de null. _

_Las entidades debiles conviene crearlas con ON DELETE CASCADE, ya que estas solo existen si es que la llave de la otra tabla existe. _

### Restricciones de integridad

1. De valores nulos: un valor puede o no ser nulo
2. Unicidad: Dado un atributo, no pueden existir dos tuplas con el mismo valor.
3. De llave: es un valor unico y no puede ser NULL
4. De referencia: Si se trabaja en una compañía, esta deve existir (LLaves foraneas).
5. De dominio: Se debe especificar el rango de los datos.

_Para restringir el dominio se utiliza CHECK y se coloca la condicion entre parentesis: CHECK(condicion). _