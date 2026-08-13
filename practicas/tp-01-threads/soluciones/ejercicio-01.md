# Ejercicio 1 — Solución

## Idea principal

El pool tiene dos threads y ejecuta las tareas `T1` y `T2` concurrentemente.

Cada tarea conserva el orden de sus propias instrucciones:

```text
T1: A antes que B
T2: 1 antes que 2
```

No hay ninguna sincronización que determine el orden relativo entre ambas tareas. Por lo tanto, sus impresiones pueden intercalarse, siempre que se respeten esas dos reglas.

## Salidas posibles

```text
AB12
A1B2
A12B
1AB2
1A2B
12AB
```

## Sobre la cantidad de cores

Las seis salidas son posibles tanto en una máquina con varios cores como en una con un solo core.

Con varios cores, los dos threads pueden ejecutarse en paralelo. Con un solo core, el sistema operativo puede pausar un thread entre sus dos `print` y ejecutar el otro; a esto se lo llama cambio de contexto. Por ejemplo:

```text
T1 imprime A
T1 es pausado
T2 imprime 1
T1 continúa e imprime B
T2 continúa e imprime 2
```

Así también puede obtenerse `A1B2` usando un único core.

## Sobre `shutdown()` y `shutdownNow()`

`shutdown()` impide enviar nuevas tareas al pool, pero permite que `T1` y `T2`, que ya fueron enviadas con `execute`, terminen normalmente.

`awaitTermination(800, TimeUnit.MILLISECONDS)` espera hasta 800 milisegundos a que finalicen. Estas tareas solo realizan dos impresiones y no contienen operaciones bloqueantes, por lo que para la resolución normal ambas terminan dentro de ese tiempo.

Si se alcanzara el timeout, `shutdownNow()` solicitaría la interrupción de las tareas activas; no las detiene de manera forzosa. Como `T1` y `T2` no consultan si fueron interrumpidas, no se toma como una fuente de salidas parciales como `AB` o `12`.
