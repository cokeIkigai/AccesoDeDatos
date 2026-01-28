# AccesoDeDatos

[Link excel añadir vuestro git](https://docs.google.com/spreadsheets/d/1tGy0R4BZPBoiyI_JG91-o8v-iacbQehQ5QSvICMoAoU/edit?usp=sharing)

Ejercicio: API REST de Gestión de Aulas y Reservas
Descripción

* Tu tarea es completar una API REST en Spring Boot para gestionar Aulas y Reservas.
- El proyecto contiene la estructura básica de entidades, repositorios, servicios y controladores, pero todos los archivos están incompletos.

- Debes rellenar el código necesario para que la API funcione correctamente.

- Este ejercicio se realiza directamente en tu repositorio GitHub, mediante un fork del proyecto.

### Objetivos

- Comprender y aplicar CRUD completo en Spring Boot.

- Completar entidades, repositorios, servicios y controladores.

- Validar reglas de negocio básicas.

- Entregar el proyecto funcionando en tu repositorio GitHub.

### Instrucciones de trabajo:
1. Haz un fork de este repositorio

Pulsa el botón Fork en GitHub y trabaja únicamente en tu copia.
entra en la carpeta demo y pulsa punto (.)

2. Completa las entidades

**Ejemplo de atributos sugeridos (puedes cambiar los nombres si quieres):**

- Aula: nombre, capacidad, edificio

- Reserva: fecha, horaInicio, horaFin, aulaId

3. Completa los repositorios

- AulaRepository.java

- ReservaRepository.java

**Debes extender correctamente JpaRepository.**

Añadir métodos personalizados si los necesitas para validaciones.

4. Implementa los servicios, básicos.

