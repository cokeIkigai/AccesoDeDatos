# Agregaciones en MongoDB 

## Concepto de agregación

- Una agregación es un mecanismo de MongoDB que permite `procesar, agrupar y transformar` conjuntos de documentos para obtener información resumida o analítica.

- En lugar de devolver documentos individuales, una agregación devuelve resultados calculados (contadores, medias, totales, agrupaciones).

**¿Para qué se usan las [agregaciones](https://aitor-medrano.github.io/iabd2223/sa/05agregaciones.html#operadores-del-pipeline)?**

1. `Análisis` de logs y eventos del sistema.

2. `Informes` de uso y actividad.

3. `Auditoría` de accesos.

4. `Detección` de errores y picos de carga.

5. `Apoyo` a la administración de sistemas.

### Diferencia entre find y aggregate.

- **find:** búsqueda de documentos. 

- **aggregate:** análisis de datos.

*Una agregación puede filtrar, agrupar, ordenar y calcular en una sola operación.*
---

### El Aggregation Pipeline.

El `Aggregation Pipeline` es una secuencia de etapas (stages). Cada etapa recibe documentos, los procesa y pasa el resultado a la siguiente.

Se puede comparar con una cadena de montaje o con una tubería de datos.

### Etapas del pipeline

Cada etapa comienza por $ y cumple una función concreta:

* **Filtrar**: *$match*

  * Filtra documentos (equivalente a WHERE en SQL)

  * Reduce datos antes de agrupar

  * Mejora el rendimiento   

* **Agrupar**: *$group* 

  * Agrupa documentos por un campo

  * Siempre usa _id como clave de agrupación

  * Permite cálculos acumulados

* **Ordenar**: *$sort, $limit, $skip*

  * Ordenación de resultados

  * Limitación y paginación

* **Transformar**: *$addFields y $set*
  
  * Añadir campos calculados.
   
  * Diferencias con $project.

* **Selección y cálculo:**  *$project*

  * Selecciona campos

  * Renombra campos

  * Crea campos calculados
 
* **Acumuladores**: Funciones de agregación

  * $sum: suma o contador
  
  * $avg: media
  
  * $min: valor mínimo
  
  * $max: valor máximo
  
  * $count: número de documentos
  
  * $push: agrupa valores en un array
  
  * $addToSet: agrupa valores únicos

---

### Flujo de datos

1. MongoDB `toma` los documentos de la colección.

2. `Aplica` la primera etapa.

3. El resultado pasa a la `siguiente`.

4. El resultado final se `devuelve` al usuario.

![Flujo](../../img/flujoDatos-aggregation-pipeline.png)

---

Ejemplos de agregación por categoría, usuario o fecha.

5. Operaciones con arrays
5.1 $unwind

Descomposición de arrays

Uso con preserveNullAndEmptyArrays

5.2 $arrayElemAt, $size, $filter

Manipulación de arrays dentro del pipeline

6. Transformación de datos
6.1 $addFields y $set



6.2 $replaceRoot y $replaceWith

Reestructuración de documentos

* **Operadores de expresiones**: 

* **Operadores aritméticos**:
* **$add, $subtract, $multiply, $divide)

* **Operadores lógicos** ($and, $or, $not)

Operadores condicionales ($cond, $ifNull)

Operadores de comparación ($eq, $gt, $lt, $gte, $lte)

* **Operadores de fecha:** *$year, $month, $dayOfMonth, $dateToString*

 * Agrupaciones por día, mes y año

 * Casos prácticos de informes temporales

* **Joins en MongoDB**: *$lookup*

 * Relación entre colecciones

 * $lookup básico

 * $lookup con pipeline














