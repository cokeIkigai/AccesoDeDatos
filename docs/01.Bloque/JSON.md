

# 📜 JSON

## ¿Qué es JSON?

**JavaScript Object Notation** (JSON) es un formato basado en texto estándar para representar datos estructurados en la sintaxis de objetos de JavaScript.

---

## 1. Qué es realmente JSON?

JSON es un formato de datos basado en `texto` que sigue la sintaxis de `objeto` de JavaScript.

Los JSON son cadenas - útiles cuando se quiere transmitir datos a través de una red. 

Debe ser convertido a un `objeto nativo` de JavaScript cuando se requiera acceder a sus datos. Ésto no es un problema, dado que JavaScript posee un objeto global JSON que tiene los métodos disponibles para convertir entre ellos.  

### JSON representa:

* **Persistencia**
* **Serialización**
* **Intercambio de datos**

```json
{
  "empresa": "TechSolutions",
  "version": "1.0",
  "empleados": [
    {
      "id": 1,
      "nombre": "Ana",
      "apellidos": "García López",
      "edad": 29,
      "activo": true,
      "email": "ana.garcia@techsolutions.com",
      "departamento": {
        "id": 10,
        "nombre": "Desarrollo"
      },
      "puesto": "Programadora Java",
      "salario": 32000.50,
      "fechaAlta": "2022-03-15",
      "habilidades": ["Java", "Spring", "SQL"],
      "direccion": {
        "calle": "Gran Vía 10",
        "ciudad": "Madrid",
        "cp": "28013"
      }
    },
    {
      "id": 2,
      "nombre": "Luis",
      "apellidos": "Martín Pérez",
      "edad": 41,
      "activo": true,
      "email": "luis.martin@techsolutions.com",
      "departamento": {
        "id": 20,
        "nombre": "Sistemas"
      },
      "puesto": "Administrador de Sistemas",
      "salario": 28000,
      "fechaAlta": "2019-09-01",
      "habilidades": ["Linux", "Redes", "Docker"],
      "direccion": {
        "calle": "Calle Alcalá 45",
        "ciudad": "Madrid",
        "cp": "28014"
      }
    }
  ]
}
```

---

## 2. Estructura de JSON

```json
{
  "id": 1,
  "nombre": "Ana",
  "edad": 25,
  "activo": true
}
```

### Reglas estrictas 

* Comillas dobles obligatorias
* No coma final
* Claves siempre string
* JSON mal formado = datos inutilizables

---

## 3. JSON y objetos Java

| JSON    | Java         |
| ------- | ------------ |
| object  | clase        |
| array   | List<T>      |
| string  | String       |
| number  | int / double |
| boolean | boolean      |

Ejemplo mental:

```json
{ "nombre": "Luis" }
```

↔

```java
class Persona {
  String nombre;
}
```

---

## 4. Lectura de un JSON desde archivo
Este JSON está pensado solo para aprender la estructura:

* Cada clave indica el tipo de dato

* El valor muestra cómo se representa en JSON

* Incluye todos los casos habituales y alguno mixto

```json
{
  "string": "Esto es un texto",
  "number": 42,
  "decimal": 19.95,
  "boolean_true": true,
  "boolean_false": false,
  "null": null,

  "array_strings": ["Java", "JSON", "Gson"],
  "array_numbers": [1, 2, 3, 4],
  "array_mixed": ["texto", 10, false],

  "object": {
    "clave": "valor",
    "numero": 1,
    "activo": true
  },

  "array_objects": [
    { "id": 1, "nombre": "Ana" },
    { "id": 2, "nombre": "Luis" }
  ]
}

```
--- 

## Ejemplos de cambio de tablas a JSON

![Tabla](../../img/tabla.png)

**JSON:**

```json
{
  "id": 1,
  "nombre": "Ana López",
  "edad": 29,
  "activo": true,
  "saldo": 1520.75,
  "observaciones": null
}
```

## Ejemplos de cambio de archivo.csv a JSON

Un archivo csv, cada columna esta separada por `;` o `,` y si hay un enter sería la siguiente fila. 
La primera fila suele corresponder a las keys. Hay a veces que el archivo esta corructo y faltan comas o puntos y comas y se debería revisar.

```csv
id;nombre;departamento;teletrabajo
1;Carlos;IT;true
2;Marta;RRHH;false
3;Pedro;;true
```
**JSON:**

```json
{
  "empleados": [
        {
            "id": 1,
            "nombre": "Carlos",
            "departamento": "IT",
            "teletrabajo": true
        },
        {
            "id": 2,
            "nombre": "Marta",
            "departamento": "RRHH",
            "teletrabajo": false
        },
        {
            "id": 3,
            "nombre": "Pedro",
            "departamento": null,
            "teletrabajo": true
        }
    ]
}
```

--- 

### Ejercicio: Guardalo en un archivo con extensión .json

* Transforma 3 empleados de la tabla de Postgre.
* Crea en MongoDb Compass 3 documentos de empleados.
* Crea y descárgate un archivo .csv desde Mockaroo:

  * Genera 50 filas con datos realistas y variados.

  * Con ese archivo, importa los datos en una base de datos llamada mockaroo dentro de una colección/tabla llamada usuarios (50 documentos/registros).

  * Campos mínimos que debe tener el CSV (recomendados):
```console
id → Row Number (empieza en 1)
nombre → Full Name
email → Email Address
edad → Number (min 18, max 65)
activo → Boolean
saldo → Number (decimals 2, min 0, max 5000)
fecha_alta → Date (últimos 2 años)
telefono → Phone
pais → Country
```
