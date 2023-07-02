# SQL

## Operadores

1. SELECT
2. FROM
3. WHERE
4. LIKE
5. DISTINCT
6. ORDER BY
7. UNION
8. LIMIT
9. GROUP BY

_Ahora agregaremos otros operadores como AVG(), SUM, MIN, MAX, COUNT, entre otros. Todos estos son funciones y entregan informacion sobre la columna que se coloca en el parentesis y no necesariamente devuelven tablas. _

_Se puede utilizar HAVING para agregar otra condicion despues del GROUP BY, es util pues, podemos realizar otro ajuste despues de reagrupar los datos de otra forma. _

## Consultas anidadas.

_ Se puede anidar una consulta a otra, por ejemplo que cierto atributo este en cierta tabla que se genera a partir de la subconsulta. _

## Mas operadores

1. s IN R, buscara que s este en R
2. s > ALL R, buscara el s que sea mas grande que todos los elementos de R
3. s > ANY R, buscara los s que sean menores a algun elemento de R.
4. EXISTS R, que exista el elemento R.

### Informacion incompleta

_Cuando falta informacion se puede completar mediante nulos NULL. _

_Pueden significar 3 cosas: _

1. El valor existe pero no se tiene la informacion.
2. El valor no existe.
3. No se sabe si el valor existe o no.

_Para ver si un elementoes nulo se usa IS NULL y para ver si no es nulo se usa IS NOT NULL. _

#### Logica de tres valores.

_El tener nulos provoca logica con tres valores, true, false , unknown. Unknown AND true = unknown, Unknown AND false = false, Unknown AND Unknown = Unknown. _

_Se puede hacer que una tabla no permita NULL: _

CREATE TABLE <name> (...
    <atr> <type> NOT NULL,
    ...)

### Inner Join

_Funciona de la misma forma que un join pero puede tener una sintaxis mas clara. _

SELECT *
FROM <name> INNER JOIN <name2>
ON atr1 = atr2;

### Outer Join

_Las consultas realizadas con OUTER JOIN permiten mantener las tuplas que no tienen pareja, es decir, la informacion sin contraparte se mantiene. Tiene 3 casos R LEFT OUTER JOIN S, mantiene las tuplas de R sin contraperte, R RIGHT OUTER JOIN S, matiene las tuplas de S sin contraparte y R FULL OUTER JOIN S, mantiene las tuplas de R y S que no tienen contraparte. _