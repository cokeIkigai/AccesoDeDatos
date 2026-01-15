# TEMA: JSON aplicado a Java (base para Acceso a Datos)

## Enfoque del tema

Este tema prepara directamente para la asignatura **Acceso a Datos**. El JSON se trabaja como **fuente real de datos**, no como simple formato.

El alumno debe ser capaz de:

* Leer datos desde JSON
* Mapear JSON ↔ objetos Java
* Modificar datos
* Persistir cambios
* Entender que JSON es una alternativa real a la BD

---

## 1. ¿Por qué JSON en Acceso a Datos?

Antes de usar:

* JDBC
* JPA / Hibernate
* Bases de datos

Se empieza por **ficheros estructurados**.

JSON representa:

* Persistencia
* Serialización
* Intercambio de datos

Mismo concepto → distinto soporte.

---

## 2. Estructura de JSON (repaso esencial)

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

## 3. JSON y objetos Java (idea clave del tema)

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

Conceptos:

* Serialización (objeto → JSON)
* Deserialización (JSON → objeto)

---

## 5. Lectura de un JSON desde archivo

### Ejemplo: data/personas.json

```json
[
  { "id": 1, "nombre": "Ana", "edad": 25 },
  { "id": 2, "nombre": "Luis", "edad": 30 }
]
```

### Clase modelo

```java
class Persona {
  int id;
  String nombre;
  int edad;
}
```

### Lectura en Java

```java
Gson gson = new Gson();
Reader reader = new FileReader("personas.json");
Persona[] personas = gson.fromJson(reader, Persona[].class);
```

---

## 6. JSON como "base de datos"

Operaciones equivalentes a CRUD:

| Operación | JSON             |
| --------- | ---------------- |
| SELECT    | Leer archivo     |
| INSERT    | Añadir objeto    |
| UPDATE    | Modificar objeto |
| DELETE    | Eliminar objeto  |

Esto conecta directamente con **DAO**.

---

## 7. Guardar cambios en JSON

```java
Writer writer = new FileWriter("personas.json");
gson.toJson(listaPersonas, writer);
writer.close();
```

Concepto clave:

> Persistencia sin base de datos

---

## 8. Patrón DAO con JSON (puente a Acceso a Datos)

```java
interface PersonaDAO {
  List<Persona> findAll();
  Persona findById(int id);
  void save(Persona p);
  void delete(int id);
}
```

Implementación:

* PersonaDAOJson
* Lee y escribe JSON

Mismo patrón → luego JDBC / JPA.

---

## 9. Errores reales (muy importantes)

* JSON mal formado
* Tipos incompatibles
* Archivos vacíos
* Clases que no coinciden con estructura

Se trabajan como **excepciones**.

---

## 10. Ejercicios propuestos

### Ejercicio 1 – Interpretación

Dado un JSON:

* Identificar objetos
* Identificar arrays
* Detectar errores

---

### Ejercicio 2 – Lectura

* Leer JSON
* Mostrar datos por consola

---

### Ejercicio 3 – CRUD

* Añadir persona
* Modificar edad
* Eliminar por id
* Guardar cambios

---

### Ejercicio 4 – DAO

* Crear interfaz DAO
* Implementar con JSON

---

### Ejercicio 5 – Puente a BD

Pregunta teórica:

> ¿Qué cambiaría si los datos estuvieran en una base de datos?

---

## 11. Evaluación

* Comprende JSON
* Mapea correctamente a Java
* Usa Gson
* Implementa CRUD
* Entiende el paso a Acceso a Datos

---

## Idea pedagógica clave

> JSON no es el fin. Es el **primer proveedor de datos**.

Luego vendrán:

* JDBC
* JPA
* APIs

El alumno ya sabrá **leer, transformar y persistir datos**.
