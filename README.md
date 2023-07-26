# Prueba_Universidad

Diseñar una Base de Datos de una Universidad que tenga las siguientes tablas : estudiantes, profesores, cursos y calificaciones.

## Crear Base de datos
La base de datos se ha creado en MySQL usando XAMPP.

Se ha tenido en cuenta que un profesor puede impartir varios cursos y un curso es impartido por un sólo profesor.

Un estudiante puede estar inscrito en un curso pero no tener todavía calificaciones hasta que no realice el examen de ese curso.

En las tablas se han puesto los datos básicos para poder hacer el ejercicio.

## Relaciones para completar todas las tablas
1.- Se puede ver el diseño de las relaciones en el siguiente fichero :

**Relaciones Base de Datos universidad.docx** https://github.com/jumair/Prueba_Universidad/blob/main/Relaciones%20Base%20de%20Datos%20universidad.docx

2.- Se puede ver el diseño completo con nombres de campos y relaciones exportado desde **phpmyadmin** en el siguiente fichero :

**univerdidad.pdf** https://github.com/jumair/Prueba_Universidad/blob/main/universidad.pdf

## Script para completar todas las tablas

En phpmyadmin creamos la base de datos univerdidad e importamos el siguiente fichero y lo ejecutamos.

**universidad.sql**  https://github.com/jumair/Prueba_Universidad/blob/main/universidad.sql

_Creará todas las tablas, las relaciones entre tablas y los datos de prueba._

## Scripts de consulta de SQL

a) Nota media de cada profesor

**código**

>   SELECT p.nombre, AVG(ca.nota) FROM profesores p
INNER JOIN cursos c
ON c.profesor_id = p.id
LEFT JOIN calificaciones ca
ON ca.curso_id = c.id
GROUP BY p.nombre;

b) Mejores notas de cada alumno

``` SELECT e.nombre, cur.asignatura, MAX(c.nota) FROM estudiantes e
INNER JOIN calificaciones c
ON c.estudiante_id = e.id
INNER JOIN cursos cur
ON cur.id = c.curso_id
GROUP BY e.nombre; ```





