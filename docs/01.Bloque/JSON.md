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

### Reglas estrictas (evaluables)

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

## 4. Librería usada: Gson

Se trabaja con **Gson** (sencilla, clara y muy usada).

Dependencia Maven:

```xml
<dependency>
  <groupId>com.google.code.gson</groupId>
  <artifactId>gson</artifactId>
  <version>2.10.1</version>
</dependency>
```

### Librería gson:

Vimos cómo utilizábamos la librería Gson para leer y modificar archivos JSON. Para ello, Gson debe transformar los datos entre objetos Java y formato JSON.

**Serialización (objeto → JSON):**
Consiste en convertir un objeto Java en una representación `JSON`, que es un formato de texto estructurado. Esto permite guardar la información en un archivo o enviarla de forma independiente al lenguaje.

**Deserialización (JSON → objeto):** 
Consiste en leer un JSON y reconstruir los `objetos` Java correspondientes, de manera que podamos manejar sus datos dentro del programa.

---

## 5. Lectura de un JSON desde archivo
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

### Acceder al JSON (Repaso)

**Archivo: cliente.json **

```json
{
  "id": 1,
  "nombre": "Ana",
  "email": "ana@email.com",
  "edad": 30,
  "activo": true,
  "saldo": 1250.75,
  "telefonos": ["600123123", "911223344"],
  "direccion": {
    "ciudad": "Madrid",
    "cp": "28013"
  }
}
```
```java
import com.google.gson.*;
import java.io.FileReader;

public class LeerClienteJson {

    public static void main(String[] args) {

        try {
            Gson gson = new Gson();

            JsonObject cliente = gson.fromJson(
                new FileReader("cliente.json"), JsonObject.class
            );

            // Valores simples

            // getAsInt para cuando es un entero
            int id = cliente.get("id").getAsInt();
            int edad = cliente.get("edad").getAsInt();

            // getAsString para cuando es string
            String nombre = cliente.get("nombre").getAsString();
            String email = cliente.get("email").getAsString();        
            

            // getAsBoolean para cuando es boleano
            boolean activo = cliente.get("activo").getAsBoolean();
            // getAsDouble cuando es valor decimal
            double saldo = cliente.get("saldo").getAsDouble();

            // Array []
            // getAsJsonArray para acceder a un array y se queda tipo JsonArray
            JsonArray telefonos = cliente.getAsJsonArray("telefonos");
            // Después se itera el array
            // dependiendo de lo que tenga pues se accede con los valores simples de arriba
            for (JsonElement t : telefonos) {
                System.out.println("- " + t.getAsString());
            }

            // Objeto anidado {}
            // dentro puede haber array y valores simples
            JsonObject direccion = cliente.getAsJsonObject("direccion");
            String ciudad = direccion.get("ciudad").getAsString();
            String cp = direccion.get("cp").getAsString();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```
---

