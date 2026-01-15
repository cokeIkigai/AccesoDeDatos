# 📚 Librería usada: Gson (Repaso)

En este bloque se trabaja con Gson, una librería de Google muy utilizada en Java para leer, escribir y manipular archivos JSON.
Es especialmente adecuada para aprendizaje porque:

- Tiene una sintaxis sencilla

- No requiere mucha configuración

- Funciona bien tanto con archivos como con APIs REST

- Dependencia Maven

Para poder usar Gson en un proyecto Maven, es necesario añadir la siguiente dependencia en el pom.xml:
```java
<dependency>
  <groupId>com.google.code.gson</groupId>
  <artifactId>gson</artifactId>
  <version>2.10.1</version>
</dependency>
```
--- 

## ¿Para qué usamos Gson?

Gson permite transformar datos entre Java y JSON, que es el formato más habitual cuando:

- Leemos archivos de configuración

- Intercambiamos información con APIs

- Trabajamos con bases de datos NoSQL como MongoDB

--- 

### Esta transformación puede darse en dos direcciones.

**Serialización (objeto → JSON)**

La serialización consiste en convertir un objeto Java en texto con formato JSON.
La ventaja es que JSON es un formato independiente del lenguaje, legible y muy estándar.

Este JSON puede:

- Guardarse en un archivo

- Enviarse por red

- Almacenarse en una base de datos

---

**Deserialización (JSON → objeto)**

La deserialización es el proceso inverso: a partir de un JSON, Gson reconstruye la información para que podamos trabajar con ella desde Java.

Esto permite:

- Acceder a valores concretos

- Hacer cálculos

- Mostrar información

- Modificar datos y volver a guardarlos

--- 

## Acceder al JSON (Repaso)

Vamos a trabajar directamente con el JSON sin usar todavía clases propias, accediendo a los datos mediante JsonObject, JsonArray y JsonElement.

Archivo: cliente.json

Este archivo contiene un ejemplo completo con:

Es importante fijarse en los tipos de datos, ya que en Java tendremos que acceder a ellos con el método adecuado.

Valores simples / Un array / Un objeto anidado

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
--- 

### Lectura del JSON desde Java

**Archivo: main.java**

1. Se lee el archivo JSON

2. Se convierte en un JsonObject

3. Se accede a cada valor según su tipo

```java
import com.google.gson.*;
import java.io.FileReader;

public class LeerClienteJson {

    public static void main(String[] args) {

        try {
            Gson gson = new Gson();
            // Aquí ocurre la deserialización: el archivo JSON se transforma en un objeto manejable desde Java.
            JsonObject cliente = gson.fromJson(
                new FileReader("cliente.json"), JsonObject.class
            );
```
--- 

### Acceso a valores simples

Cada tipo de dato tiene su método correspondiente:
```java
// valores tipo enteros
int id = cliente.get("id").getAsInt();
int edad = cliente.get("edad").getAsInt();

// valores tipo string
String nombre = cliente.get("nombre").getAsString();
String email = cliente.get("email").getAsString();

// valores tipo boolean
boolean activo = cliente.get("activo").getAsBoolean();
double saldo = cliente.get("saldo").getAsDouble();

// valores tipo Array
JsonArray telefonos = cliente.getAsJsonArray("telefonos");

// Se recorre para ver sus valores simples
for (JsonElement t : telefonos) {
    System.out.println("- " + t.getAsString());
}

// Cuando un campo contiene otro objeto, se accede con getAsJsonObject y luego se leen sus valores internos
JsonObject direccion = cliente.getAsJsonObject("direccion");
String ciudad = direccion.get("ciudad").getAsString();
String cp = direccion.get("cp").getAsString();
```


## Gestión de errores

Es necesrio utilizar try-catch para:

- Evitar que el programa se detenga si el archivo no existe.
  
- Detectar errores de formato JSON.
  
- Controlar problemas de lectura.
  
```java
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```
