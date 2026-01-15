# 🍃  MONGO COMPASS

MongoDB Compass es una herramienta gráfica (GUI) oficial de MongoDB que permite `visualizar, crear y modificar` bases de datos y colecciones sin necesidad de usar la consola.

**Su objetivo principal es:**

* Trabajar con datos en formato `JSON`.

* Entender `visualmente` cómo se almacenan los documentos.

* Facilitar el `aprendizaje` y la gestión de MongoDB.

---

**A diferencia de las bases de datos relacionales, MongoDB:**

* No usa `tablas`

* Usa `colecciones y documentos`

* Cada documento tiene estructura `clave : valor`

---

**MongoDB Compass es especialmente útil:**

* Permite `crear` bases de datos y colecciones de `forma visual`

* `Muestra` los documentos directamente en formato JSON.

* Ayuda a `detectar errores` de estructura ( comas, llaves, tipos de datos )

--- 

### Creación de la Base de datos.

Se da click al icono + para añadir la Base de datos nueva.

![Conection](https://github.com/cokeIkigai/Lenguajes/blob/ddf6619d2c3c12eb592d3513d51cdf1724294bc8/JAVA/img/newConnectionMongo.PNG)

--- 

### Interfaz de Compass

- Se pueden ver todas las demás Bases de datos creadas con anterioridad.
- Si selecionas una de ellas, aparecerán sus documentos con su forma JSON { clave: valor } 

![Compass](https://github.com/cokeIkigai/Lenguajes/blob/ddf6619d2c3c12eb592d3513d51cdf1724294bc8/JAVA/img/Compass.PNG)

---

### Insertar un nuevo Documento

- Utilizando el formato de JSON, se le irán añadiendo clave y valor de los mismos.

![Compass](https://github.com/cokeIkigai/Lenguajes/blob/ddf6619d2c3c12eb592d3513d51cdf1724294bc8/JAVA/img/insertDocument.PNG)

---

## Búsquedas en la barra de Compass

MongoDB Compass permite filtrar documentos usando consultas MongoDB en formato JSON.
El filtro se aplica sobre la `colección` seleccionada.

**Búsqueda simple (clave : valor)**: Devuelve los documentos cuyo valor coincida exactamente.

```json
{ "nombre": "Ana López" }
```

**Búsqueda por _id**: Útil cuando se conoce el identificador único del documento.
```json
{ "_id": ObjectId("65f1c2a8e9b123456789abcd") }
```
**Comparaciones numéricas**:
```json
{ "edad": { "$gt": 25 } }
```
**Operadores comunes:**

  * $gt → mayor que

  * $gte → mayor o igual

  * $lt → menor que

  * $lte → menor o igual
    
```json
{ "edad": { "$gte": 18, "$lte": 65 } }
```
**Búsqueda por boolean**
```json
{ "activo": true }
```
**Búsqueda de valores null**
```json
{ "observaciones": null }
```
**Búsqueda por texto parcial (regex)**: i → no distingue mayúsculas/minúsculas
```json
{ "email": { "$regex": "mail", "$options": "i" } }
```
**Búsqueda con varias condiciones (AND)**: MongoDB aplica AND automáticamente.
```json
{
  "activo": true,
  "edad": { "$gt": 30 }
}
```
**Búsqueda con OR**:
```json
{
  "$or": [
    { "nombre": "Ana López" },
    { "nombre": "Luis Pérez" }
  ]
}
```
**Búsqueda por existencia de campo**: No todos los documentos tienen porque tener dicho campo.
```json
{ "telefono": { "$exists": true } }
```
