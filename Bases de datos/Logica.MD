## Vistas

CREATE VIEW <name> AS
...
...

_Esto ultimo permite crear una tabla virtual para realizarle consultas que se realizan frecuentemente. No son tablas fisicas, primero se reescribe la consulta original que queriamos hacer a la BDD para hacerla a la vista (escribimos el nombre de la vista en el FROM), luego esta consulta se realizara sobre las tablas originales. _

_Son convenientes pues lo unico que se esta guardando es la consulta que se realiza frecuentemente para utilizarla despues y no la tabla. Entonces no se crear una tabla en el disco  y se sigue trabajando con las tablas de la base, ademas si se actualiza un dato no hay problema (no es necesario cambiarlo en dos tablas.). _

_Sirven para reducir la complejidad de consultas grandes y evitan la repeticion de consultas frecuentes. Aun asi es mas lenteo que tener las tablas de verdad. _

_Las vistas materializadas generan la misma abstraccion que las normales pero son mas rapidas, a cambio de esto requieren un espacio adicional e introducen redundancia al esquema, por lo que hay que ir actualizandolas constantemente. _

CREATE MATERIALIZED VIEW <name>

REFRESH MATERIALIZED VIEW <name>

## Triggers

_Son procedimientos de la BDD que se gatillan segun ocurran ciertos eventos. Puede ser un ebento BEFORE, AFTER, INSTEAD OF junto con CREATE, DELETE, UPDATE, por ejemplo BEFORE CREATE. _

CREATE TRIGGER <name>
AFTER CREATE ON <table1>
FOR EACH ROW
  BEGIN
  UPDATE <table2>
  SET ....
END

## Stored Procedures

_Son funciones definidas en SQL que quedan guardadas en el DBMS y se pueden usar en consultas. _

CREATE or REPLACE Function <function_name>(<args>) RETURNS <type> AS $$

DECLARE
  <delacarion de variables>
BEGIN
 <sentencias SQL
END
$$ language plpgsql

## Conexion a la base de datos

_Utilizar la base de datos desde un programa mediante una librearia, por ejemplo en Python sqlite3 o psycopg2. _

import sqlite3
db_connection = sqlite3.connect('some_db.db')
_Aqui esta el proceso que realizamos con la bdd. _
db_connection.close() # cerramos la conexion

_Al conectarnos significa que la bdd esta esperando instrucciones de nuestro programa. _

### Cursores

_Permite ejecutar un comando SQL en Python y representa un puntero al output del comando. _

cur = db_connection.cursor() # instanciamos el cursor
create_query = "CREATE TABLE Peliculas(id INT, titulo
VARCHAR(100));"
insert_query = "INSERT INTO Peliculas VALUES (1, 'Minions');"
try:
  cur.execute(create_query)
  cur.execute(insert_query)
except sqlite3.OperationalError as e:
  print(e)
db_connection.commit() # guardamos los cambios en disco.
db_connection.close() #cerramos la conexion

_Para acceder a los resultados se puede utilizar fetchone() para obtener uno de estos o fetchall() para traerlos todos. _

_No se deben concatenar strings de los inputs pues es inseguro, si se utilizan parametros para una consulta que proviene del input de usuario se debe sanear el input: _

query = "SELECT * FROM Students \
         WHERE edad =%(edad)d AND nombre = %(nombre)s"
cursor.execute(query, {"nombre": "Rivera", "edad": 11})

## ORMs

_Consiste en tener para cada tabla de la DB un clase en el codigo de la aplicacion, proporcionan una capa de abstraccion sobre la base de datos. _

_Generalmente se llama Modelos a las clases que representan las tablas en el codigo. _

## Migraciones

_Scripts encargadas de generar cambios en el esquema de la DB, es decir, traducen el codigo del lenguaje de programacion a sentencias CREATE, ALTER o DELETE. _

