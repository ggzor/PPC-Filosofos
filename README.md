# Programación concurrente y paralela: Filósofos Comensales

**Equipo:**  

- **201764692** Cortez Chávez Sergio Daniel  
- **201745351** Huitzil Juárez Marisol  
- **201768489** Padilla Rios Ruben  
- **201744436** Suárez Polo Axel  

## Problema

Cinco filósofos están sentados alrededor de una mesa y pasan su vida cenando y pensando. Cada filósofo tiene un plato de fideos y un palillo a la izquierda de su plato. Para comer los fideos son necesarios dos palillos y cada filósofo sólo puede tomar el palillo que está a su izquierda y el de su derecha.

Si cualquier filósofo toma un palillo y el otro está ocupado, se quedará esperando, con el palillo en la mano, hasta que pueda tomar el otro palillo, para luego empezar a comer. El resto de filósofos que no está ni comiendo ni con un palillo en la mano está pensando.

El problema consiste en inventar un algoritmo que permita comer a los filósofos.

## Variación

Para los fines de la práctica se agrega la condición de que si un filósofo ha intentado 10 veces obtener
un palillo y no ha podido entonces este muere de **inanición**.

## Solución

La solución consiste en tener un arreglo de `RLock`, que representarán los palillos y la estrategia consiste en tomar el palillo de la izquierda, y revisar si está disponible el de la derecha, si este es el caso, entonces se toma el de la derecha y se empieza a comer.

El código principal para esta lógica es el siguiente:

```python
palillo_izq.acquire()

if palillo_der.acquire(blocking=False):
    return True
else:
    palillo_izq.release()
    return False
```
