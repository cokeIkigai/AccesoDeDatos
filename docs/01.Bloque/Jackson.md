# Lectura de ficheros JSON en Java con Jackson

En muchas aplicaciones reales no es necesario utilizar una base de datos para almacenar información.  
Configuraciones, usuarios simples, parámetros de ejecución o datos intercambiados entre aplicaciones suelen almacenarse en **ficheros JSON**.

En este ejemplo veremos **cómo leer un fichero JSON existente en Java**, combinando:

- Acceso a ficheros (`File`)
- Manejo de excepciones (`IOException`)
- Uso de una librería externa de parseo JSON (**Jackson**)

> ⚠️ Importante: en este ejemplo **NO se escribe el JSON**, solo se **lee**.  
> El fichero debe existir previamente y contener JSON válido.

---

Para poder trabajar con JSON en Java de forma cómoda, necesitamos una librería externa.

**pom.xml**:

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.15.2</version>
</dependency>
```
---

**LecturaJSON.java**:

```java
import com.fasterxml.jackson.databind.JsonNode;
import com.fasterxml.jackson.databind.ObjectMapper;

import java.io.File;
import java.io.IOException;

public class ProcesarJSONSimple {

    public static void main(String[] args) {
        File archivoJSON = new File("unidad1_ejemplos/usuario_simple.json");

        try {
           

            ObjectMapper mapper = new ObjectMapper();
            JsonNode root = mapper.readTree(empleados.json);

            // Comprobando que se leen los campos del json (Cambiarlos por los que tenga el JSON):
            System.out.println("Nombre: " + root.path("nombre").asText());
            System.out.println("Edad: " + root.path("edad").asInt());
            System.out.println("Activo: " + root.path("activo").asBoolean());

            // En caso de ser un array
            System.out.print("telefonos: ");
            for (JsonNode h : root.path("telefonos")) {
                System.out.print(h.asText() + " ");
            }
            System.out.println();

        } catch (IOException e) {
            System.err.println("No se pudo leer o parsear el JSON: " + e.getMessage());
        }
    }
}
```
