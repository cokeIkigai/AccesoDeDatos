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

7. Operadores de expresiones

Operadores aritméticos ($add, $subtract, $multiply, $divide)

Operadores lógicos ($and, $or, $not)

Operadores condicionales ($cond, $ifNull)

Operadores de comparación ($eq, $gt, $lt, $gte, $lte)

8. Trabajo con fechas

Operadores de fecha:

$year, $month, $dayOfMonth

$dateToString

Agrupaciones por día, mes y año

Casos prácticos de informes temporales

9. Joins en MongoDB con $lookup

Relación entre colecciones

$lookup básico

$lookup con pipeline

Similitudes y diferencias con JOIN en SQL

10. Subpipelines y facetado
10.1 $facet

Múltiples agregaciones en una sola consulta

Dashboards y estadísticas combinadas

11. Optimización de agregaciones

Uso de índices en agregaciones

Colocar $match y $project al inicio

Coste computacional de $group y $lookup

Análisis con explain()

12. Agregaciones en MongoDB Compass

Uso visual del Aggregation Builder

Ventajas para aprendizaje y depuración

13. Buenas prácticas

Legibilidad del pipeline

Reutilización de agregaciones

Cuándo usar agregaciones vs lógica en aplicación

14. Casos prácticos propuestos (enfoque ASIR)

Análisis de uso de sistemas (logs)

Monitorización de eventos y errores

Estadísticas de acceso de usuarios

Consumo de recursos por servicio

14.1 Casos prácticos propuestos

Ventas por cliente y mes

Media de precios por categoría

Usuarios más activos

Análisis de logs o eventos

15. Comparativa con SQL

GROUP BY vs $group

WHERE vs $match

SELECT vs $project

JOIN vs $lookup

Este temario está adaptado a ASIR – Gestión de Bases de Datos, con un enfoque en administración, análisis de datos operativos, monitorización y apoyo a la toma de decisiones, más que en el desarrollo de aplicaciones.

Listo. He convertido Aggregation en MongoDB en un bloque de temario explicativo, con:

Definición clara y enfoque ASIR – Gestión de BBDD

Conceptos clave explicados de forma progresiva

Pipeline explicado como proceso (no como código)

Relación directa con SQL administrativo

Ejercicios tipo clase/examen, sin entrar aún en sintaxis

Este formato es ideal para:

Explicarlo en pizarra o diapositivas

Introducir MongoDB a alumnos con base SQL

Evaluar comprensión conceptual, no solo técnica

Siguiente pasos posibles (elige):

Resolver los ejercicios con código MongoDB

Añadir ejercicios de examen con solución

Crear un caso práctico completo de logs ASIR

Adaptarlo a 1 sesión de 2 horas o 2 sesiones

Dime cómo lo quieres cerrar didácticamente y lo dejamos redondo.
