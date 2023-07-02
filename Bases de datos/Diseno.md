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