# Prueba_Universidad

Diseñar una Base de Datos de una Universidad que tenga las siguientes tablas : estudiantes, profesores, cursos y calificaciones.

## Crear Base de datos
La base de datos se ha creado en MySQL usando **XAMPP**. _Enlace_ https://www.apachefriends.org/es/index.html.

Se ha usado también **MySQL Workbench**. _Enlace_ https://dev.mysql.com/downloads/workbench/.

> Se ha tenido en cuenta que un profesor puede impartir **n** cursos y un curso es impartido por un sólo profesor.

> Un estudiante puede estar inscrito en un curso pero no tener todavía calificaciones hasta que no realice el examen de ese curso.

> Un estudiante puede cursar **n** cursos o asignaturas y un curso puede ser seguido por **n** estudiantes.

> Un estudiante puede tener **n** calificaciones y cada calificación pertenece a un estudiante y un curso.

En las tablas se han puesto los datos básicos para poder hacer el ejercicio.

## Relaciones para completar todas las tablas

1.- Se puede ver el diseño de las relaciones en el siguiente fichero :

**Relaciones Base de Datos universidad.docx** https://github.com/jumair/Prueba_Universidad/blob/main/Relaciones%20Base%20de%20Datos%20universidad.docx

2.- Se puede ver el diseño completo con nombres de campos y relaciones exportado desde **phpmyadmin** en el siguiente fichero :

**univerdidad.pdf** https://github.com/jumair/Prueba_Universidad/blob/main/universidad.pdf

3.- Se puede ver el diseño de relaciones en el siguiente fichero creado desde **MySQL Workbench** :

**universidad.mwb** https://github.com/jumair/Prueba_Universidad/blob/main/universidad.mwb

## Script para completar todas las tablas

En phpmyadmin creamos la base de datos univerdidad e importamos el siguiente fichero y lo ejecutamos.

**universidad.sql**  https://github.com/jumair/Prueba_Universidad/blob/main/universidad.sql

_Creará todas las tablas, las relaciones entre tablas y los datos de prueba._

## Scripts de consulta de SQL

a) Nota media de cada profesor

> Saco la nota media de todos los cursos de cada profesor.

    SELECT p.nombre AS profesor, AVG(ca.nota) AS Nota_Media FROM profesores p
    INNER JOIN cursos c
    ON p.id = c.profesor_id
    INNER JOIN calificaciones ca
    ON c.id = ca.curso_id
    GROUP BY p.nombre;

b) Mejores notas de cada alumno

    SELECT e.nombre AS Estudiante, cur.asignatura AS Curso, MAX(c.nota) AS Nota FROM estudiantes e
    INNER JOIN calificaciones c
    ON e.id = c.estudiante_id
    INNER JOIN cursos cur
    ON c.curso_id = cur.id
    GROUP BY e.nombre;

c) Ordenar a los estudiantes por cursos en los que están inscritos

    SELECT c.asignatura AS Curso, e.nombre AS Estudiante FROM cursos c
    INNER JOIN estudiantes_cursos ec
    ON c.id = ec.curso_id
    INNER JOIN estudiantes e
    ON ec.estudiante_id = e.id
    ORDER BY c.asignatura;

d) Crear informe resumido de cursos y sus cualificaciones promedio, ordenados por el curso más desafiante (curso con la calificación promedio más baja) 
hasta el curso más fácil.

    SELECT c.asignatura AS Curso, AVG(ca.nota) AS Nota_Promedio FROM cursos c
    INNER JOIN calificaciones ca
    ON c.id = ca.curso_id
    GROUP BY c.asignatura
    ORDER BY nota_promedio ASC;

e) Encontrar que estudiante y profesor tienen más cursos en común

> Como aquí tengo 3 resultados que cumplen la condición muestro el primero con LIMIT 1.

    SELECT p.nombre AS Profesor, e.nombre AS Estudiante, COUNT(e.nombre) AS Cursos_en_Comun FROM profesores p
    INNER JOIN cursos c
    ON p.id = c.profesor_id
    INNER JOIN estudiantes_cursos ec
    ON c.id = ec.curso_id
    INNER JOIN estudiantes e
    ON ec.estudiante_id = e.id
    GROUP BY p.nombre, e.nombre
    ORDER BY cursos_en_comun DESC, p.nombre ASC
    LIMIT 1;




