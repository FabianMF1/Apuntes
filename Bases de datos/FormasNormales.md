## Dependencia funcional

_Para una relacion R una dependencia funcional es X -> Y, donde X e Y son conjuntos de atributos de R. Esta dependencia es valida ssi para toda tupla perteneciente a R se tiene que: Pi(t1)=Pi(t2) implica Pi(t1)=pi(t2) para condiciones iguales, es decir, si se aplica la misma condicion en la proyeccion, se tiene que obtener el mismo resultado (si es que para alguna condicion anterior t1 y t2 dieron lo mismo). _

_Para reducir la redundancia se tiene que: _
1. Averiguar las dependencias que aplican. (por ejemplo la transitividad permite eliminar el dato intermedio.)
2. Descomponer las tablas en tablas mas pequeñas.

## BCNF

_Causa de anomalias X->Y cuando X no es una super llave. Entonces, una relacion R esta en BCNF si para toda dependencia funcional no triviarl X -> Y, X es una super llave (no trivial quiere decir que Y no es subconjunto de X). _

## 3NF

_Una relacion R esta en #NF si para toda dependencia funcional no trivial X-> Y, X es una super llave o Y es parte de una llave minimal. Y es una llave minimal si no existe Y' tal que Y' es subconjunto de Y._

_Es un poco mas flexible que BCNF, otra forma de llegar a 3NF es generando 1NF, despues 2NF y finalmente 3NF. _

