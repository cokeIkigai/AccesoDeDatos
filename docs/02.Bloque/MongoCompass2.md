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

  * Filtra documentos 

  * Reduce datos antes de agrupar

  * Mejora el rendimiento   

* **Agrupar**: *$group* 

  * Agrupa documentos por un campo

  * Siempre usa _id como clave de agrupación

  * Permite cálculos acumulados

* **Ordenar**:

  * **$sort:** – Ordenar resultados

  * **$limit:** – Limitar resultados
   
  * **$skip:** – Saltar resultados


* **Transformar**: *$addFields y $set*
  
  * $addFields – Añadir campos

  * $set – Modificar o añadir campos 

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
 
* **Operadores de expresiones**: 

* **Operadores aritméticos**:
  * $add: Para $addicionar el impuesto al total de la factura.

  * $subtract: Necesitamos $subtract (restar) los gastos de los ingresos para calcular la utilidad.

  * $multiply: Debes $multiply (multiplicar) el precio unitario por la cantidad vendida.

  * $divide: Para hallar el promedio, debes $divide (dividir) la suma total entre el número de elementos.

  * $and: El pago se procesará $and (y) el pedido se enviará solo si el stock está disponible $and (y) la dirección es válida.

  * $or: Puedes pagar con tarjeta $or (o) con transferencia bancaria.

  * $not: $not (No) se aceptarán devoluciones si la etiqueta ha sido removida.
 
  * **Operadores Condicionales**:
    
    * $cond: Usaremos $cond para asignar un descuento del 10% si el cliente es frecuente, de lo contrario, el descuento será del 0%.

    * $ifNull: Aplicamos $ifNull al campo telefono para mostrar "No registrado" en el informe si el valor es nulo o no existe.

  * **Operadores de Comparación**:
    
    * $eq: Filtraremos los productos cuyo estado $eq (sea igual a) "activo".

    * $gt: Buscamos clientes con un puntaje de fidelidad $gt (mayor que) 100.

    * $lt: Seleccionaremos las órdenes con un monto total $lt (menor que) 50 para análisis de microventas.

    * $gte: El filtro aplica para pedidos $gte (mayores o iguales a) una fecha específica.

    * $lte: La promoción es válida para productos con precio $lte (menor o igual a) $20.

* **Operadores de fecha:** 

    * $year: Extraemos el año con {$year: "$fecha"} para agrupar las ventas por año.

    * $month: Separamos el mes con {$month: "$fecha"} y creamos un informe de ventas mensuales.

    * $dayOfMonth: Obtenemos el día con {$dayOfMonth: "$fecha"} y analizamos las ventas diarias.

    * $dateToString: Formateamos la fecha a "dd/mm/aaaa" con {$dateToString: {format: "%d/%m/%Y", date: "$fecha"}} para el reporte.

---

### Flujo de datos

1. MongoDB `toma` los documentos de la colección.

2. `Aplica` la primera etapa.

3. El resultado pasa a la `siguiente`.

4. El resultado final se `devuelve` al usuario.

![Flujo](../../img/flujoDatos-aggregation-pipeline.png)

---

Buscar para estos comandos y dejalo comentado en el codigo.

$unwind,  $arrayElemAt, $size, $filter, $replaceRoot y $replaceWith

---

### EJERCICIO

Configuración de campos para generar datos en **Mockaroo**  
Cantidad recomendada: **500–800 registros**

| Campo            | Tipo Mockaroo                                              | Ejemplo              |
|------------------|------------------------------------------------------------|----------------------|
| _id              | Row Number                                                 | 1                    |
| ticketId         | Custom Pattern → TKT###                                    | TKT001               |
| empleado         | Full Name                                                  | Ana López            |
| departamento     | Custom List → IT, Ventas, RRHH, Finanzas                   | IT                   |
| prioridad        | Custom List → Baja, Media, Alta, Crítica                   | Alta                 |
| estado           | Custom List → Abierto, En progreso, Cerrado                | Cerrado              |
| categoria        | Custom List → Hardware, Software, Red, Seguridad           | Red                  |
| horasResolucion  | Number (0–40)                                              | 6                    |
| costeHora        | Number (15–40)                                             | 25                   |
| fechaCreacion    | Datetime (last 2 years)                                    | 2025-10-02           |
| satisfaccion     | Number (1–5)                                               | 4                    |
| tecnico          | Full Name                                                  | Carlos Ruiz          |
| reabierto        | Boolean                                                    | true                 |

1. Contar el número total de tickets registrados en la colección usando $count.
2. Mostrar únicamente los tickets cuyo estado sea "Abierto" usando $match.
3. Calcular el número de tickets por departamento usando $group + $sum.
4. Calcular el número de tickets por prioridad y ordenarlos de mayor a menor usando $group + $sort.
5. Obtener la media global de horasResolucion usando $group + $avg.
6. Calcular las horas medias de resolución por departamento usando $group.
7. Crear un campo costeTicket = horasResolucion * costeHora usando $addFields + $multiply.
8. Calcular el coste total acumulado de todos los tickets usando $group + $sum.
9. Mostrar los 5 técnicos con mayor número de tickets gestionados usando $group + $sort + $limit.
10. Determinar qué categoría tiene más incidencias registradas usando $group + $sort + $limit.
11. Listar los tickets críticos cuya resolución haya superado 10 horas usando $match + $gt.
12. Añadir un campo booleano lento que indique si horasResolucion > 8 usando $addFields + $cond.
13. Formatear fechaCreacion al formato dd/mm/yyyy usando $project + $dateToString.
14. Mostrar solo los campos ticketId, tecnico y costeTicket usando $project.
15. Calcular la satisfacción media por técnico usando $group + $avg.
16. Calcular el número de tickets reabiertos por departamento usando $match + $group.
17. Obtener el porcentaje de tickets reabiertos respecto al total por departamento usando $group + operaciones aritméticas.
18. Agrupar por año de fechaCreacion y contar tickets anuales usando $year + $group.
19. Agrupar por año y mes de fechaCreacion y calcular total tickets, horas medias y coste total usando $year + $month + $group.
20. Construir un pipeline final por departamento que muestre total tickets, coste total, horas medias, satisfacción media y porcentaje de reabiertos, ordenado por coste descendente.


















