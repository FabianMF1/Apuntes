## Costo de un algoritmo

Cuántas veces tengo que leer una página desde el disco, o
escribir una página al disco!

Las operaciones en buffer (RAM) son orden(es) de magnitud
más rápidas que leer/escribir al disco – costo 0

1. open(): se posiciona antes de la primera tupla de R
2. next(): devuelve la siguiente tupla o NULL
3. close(): cierra el iterador

## Seleccion

Si queremos hacer una selección sobre una tabla R:

open()
  R.open()
next() // retorna el siguiente seleccionado
  t:= R.next()
  while t != null do
    if t satisface condición then
      return t
    t:= R.next()
  return null

_Necesariamente tenemos que recorrer todo R al hacer seleccion. _

Con indice y consulta de igualdad: Si queremos hacer una selección sobre una tabla R a un
atributo indexado con un índice I

Sólo tenemos que leer las páginas que satisfacen la
condición (más I/O si muchas tuplas satisfacen la
condición)

## Nested Loop Join

Es una implementación directa basada en un loop.

Para cada tupla de R debemos leer S entera, aparte de leer
R entera una vez.

Costo en I/O es:
Costo(R) + Tuplas(R)·Costo(S)

## Block Nested Loop Join

Ahora cargamos muchas páginas de R a buffer.

Costo en I/O es:
Costo(R) + (Páginas(R)/Buffer)·Costo(S)

## Sorting

Necesitamos ordenar tuplas que exceden por mucho el
tamaño de la memoria RAM

### External Merge Sort

Hablaremos de Run como una secuencia de páginas que
contiene una conjunto ordenado de tuplas
Algoritmo funciona por fases

Fase 0: creamos los runs iniciales

Fase i:
• Traemos los runs a memoria
• Hacemos el merge de cada par de runs
• Almacenamos el nuevo run a disco (i.e. materializamos
resultados intermedios)

