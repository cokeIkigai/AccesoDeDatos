# UT1 – Lectura de ficheros JSON en Java con Jackson

## 1. Introducción

En muchas aplicaciones reales no es necesario utilizar una base de datos para almacenar información.  
Configuraciones, usuarios simples, parámetros de ejecución o datos intercambiados entre aplicaciones suelen almacenarse en **ficheros JSON**.

En esta unidad veremos **cómo leer un fichero JSON existente en Java**, combinando:

- Acceso a ficheros (`File`)
- Manejo de excepciones (`IOException`)
- Uso de una librería externa de parseo JSON (**Jackson**)

> ⚠️ Importante: en este ejemplo **NO se escribe el JSON**, solo se **lee**.  
> El fichero debe existir previamente y contener JSON válido.

---

## 2. Requisitos previos

### 2.1 Dependencia Jackson (Maven)

Para poder trabajar con JSON en Java de forma cómoda, necesitamos una librería externa.

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.15.2</version>
</dependency>
