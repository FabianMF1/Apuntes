## Transactions

Propiedades ACID:

1. Atomicity: O se ejecutan todas las operaciones de la transacción, o no se ejecuta ninguna.
2. Consistency: Cada transacción preserva la consistencia de la BD (restricciones de integridad, etc.).
3. Isolation: Cada transacción debe ejecutarse como si se estuviese ejecutando sola, de forma aislada.
4. Durability: Los cambios que hace cada transacción son permanentes en el tiempo, independiente de cualquier tipo de falla.

Transaction Manager se encarga de asegurar Isolation y Consistency

Log y Recovery Manager se encargan de asegurar Atomicity y Durability

Una transacción es una secuencia de 1 o más operaciones que modifican o consultan la base de datos.

START TRANSACTION

UPDATE cuentas
SET saldo = saldo - v
WHERE cid = 1

UPDATE cuentas
SET saldo = saldo + v
WHERE cid = 2

COMMIT

START TRANSACTION y COMMIT nos permiten agrupar operaciones en una sola transacción.

## Operaciones

1. R(X): Lectura del elemento X.
2. W(X): Escritura del elemento X.
3. A: Abortar transaccion.
4. C: Finalizar transaccion.

## Conflicos con transacciones

Lecturas sucias (Write - Read)
Lecturas no repetibles (Read - Write)
Actualización perdida o reescritura de datos temporales (Write - Write)

## Schedule

Un schedule S es una secuencia de operaciones primitivas de una o más transacciones, tal que para toda transacción, las acciones de ella aparecen en el mismo orden que en su definición.

Un schedule S es serial si no hay intercalación entre las acciones

Un schedule S es serializable si existe algún schedule S’ serial con las mismas transacciones, tal que el resultado de S y S’ es el mismo para todo estado inicial de la BD.

La tarea del Transaction Manager es permitir solo schedules que sean serializables.

### Acciones no conflictivas

Las siguientes acciones son NO conflictivas para dos
transacciones distintas i, j:

• Ri(X), Rj(Y)
• Ri(X), Wj(Y) con X != Y
• Wi(X), Rj(Y) con X != Y
• Wi(X), Wj(Y) con X != Y

Podemos cambiarlas de orden en un schedule.

### Acciones conflictivas

Las siguientes acciones son conflictivas para dos
transacciones distintas i, j:

• Pi(X), Qi(Y) con P,Q en {R, W}
• Ri(X), Wj(X)
• Wi(X), Rj(X)
• Wi(X), Wj(X)

No podemos cambiar su orden en un schedule a la ligera.

Puedo permutar un par de operaciones consecutivas si:

• No usan el mismo recurso
• Usan el mismo recurso pero ambas son de lectura

Un schedule es conflict serializable si puedo transformarlo a uno serial usando permutaciones

Si un schedule es conflict serializable implica que también es serializable, pero hay schedules serializables que no son conflict serializable.

## Grafo de precedencia

Dado un schedule puedo construir su grafo de precedencia

• Nodos: transacciones del sistema
• Aristas: hay una arista de T a T’ si T ejecuta una
operación op1 antes de una operación op2 de T’,
tal que op1 y op2 no se pueden permutar.

Un schedule es conflict serializable ssi el grafo de precedencia es acíclico.

## Strict 2PL

1. Si una transacción T quiere leer (resp. modificar) un objeto, primero pide un shared lock (resp. exclusive lock) sobre el objeto.

Una transacción que pide un lock se suspende hasta que el lock es otorgado.

Si una transacción mantiene un exclusive lock de un
objeto, ninguna otra transacción puede mantener un
shared o exclusive lock sobre el objeto

Es importante notar que por lo anterior, para obtener
el exclusive lock, no debe haber ningún lock sobre el
objeto

2. Cuando la transacción se completa, libera todos los
locks que mantenía

Si se siguen estas reglas se aseguran solo schedules conflict serializables.

ROLLBACK; permite deshacer una transaccion.

ROLLBACK TO SAVEPOINT, se borra el savepoint pero se vuelve a este estado antes.

## Recuperacion de fallas

### Log Manager

Una página se va llenando secuencialmente con logs

Cuando la página se llena, se almacena en disco

Todas las transacciones escriben el log de manera
concurrente

Registra todas las acciones de las transacciones

Los logs comunes son:
• <START T>
• <COMMIT T>
• <ABORT T>
• <T UPDATE>
• <T, X, t> donde t es el valor antiguo de X

#### Undo Logging

Regla 1: si T modifica X, todos logs <T, X, t> deben
ser escritos antes que el valor X sea escrito en disco

Regla 2: si T hace commit, el log <COMMIT T> debe
ser escrito justo después de que todos los datos
modificados por T estén almacenados en disco

Recuperacion con undo logging:

Procesamos el log desde el final hasta el principio:
• Si leo <COMMIT T>, marco T como realizada
• Si leo <ABORT T>, marco T como realizada
• Si leo <T, X, t>, debo restituir X := t en disco, si
no fue realizada.
• Si leo <START T>, lo ignoro

Utilizamos checkpoints para no tener que leer el log
entero y para manejar las fallas mientras se hace
recovery

• Dejamos de escribir transacciones
• Esperamos a que las transacciones actuales
terminen
• Se guarda el log en disco
• Escribimos <CKPT> y se guarda en disco
• Se reanudan las transacciones

Problema: es prácticamente necesario apagar el
sistema para guardar un checkpoint

Nonquiescent Checkpoints son un tipo de
checkpoint que no requiere "apagar" el sistema

#### Redo Logging 

Los logs son:
• <START T>
• <COMMIT T>
• <ABORT T>
• <T, X, v> donde v es el valor nuevo de X
• <T,END>

Regla 1: Antes de modificar cualquier elemento X en
disco, es necesario que todos los logs estén
almacenados en disco, incluido el COMMIT

Esto es al revés respecto a Undo Logging

En resumen:
• Escribir el log <T, X, v>
• Escribir <COMMIT T>
• Escribir los datos en disco
• Escribir <T,END> en log (en disco)

Recuperacion con Redo Logging.

Procesamos el log desde el principo hasta el final:
• Identificamos las transacciones que hicieron
COMMIT sin hacer END (si hicieron END todo OK)
• Hacemos un scan desde el principio
• Si leo <T, X, v>:
• Si T no hizo COMMIT, no hacer nada
• Si T hizo COMMIT, reescribir con el valor v
• Para cada transacción sin COMMIT, escribir
<ABORT T>

Usando checkpoints:

• Escribimos un log <START CKPT (T1, ..., Tn)>,
donde T1, ..., Tn son transacciones activas y sin
COMMIT
• Guardar todo el log en el disco
• Guardar en disco todo lo que haya hecho COMMIT
hasta ese punto; escribir en log END al finalizar
• Una vez hecho, escribir <END CKPT>

Problema: no es posible ir grabando los valores de X
en disco antes que termine la transacción

Por lo tanto se congestiona la escritura en disco

#### Undo/Redo Logging

Es la solución para obtener mayor performance que
mezcla las estrategias anteriormente planteadas

Los logs son:
• <START T>
• <COMMIT T>
• <ABORT T>
• <T, X, vantiguo, vnuevo>
• <T,END> (todo en disco – COMIT y valor)

El flujo:
• Log <T, X, vantiguo, vnuevo> va al disco antes de X
• (write-ahead logging)
• <T,COMMIT> va de manera arbitraria al disco
• (antes o después de X)
• <T,END> va cuando escribimos y datos y COMMIT

Recuperación:
• Undo de transacciones sin COMMIT
• Redo transacciones con COMMIT y sin END

