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

    SELECT p.nombre, AVG(ca.nota) FROM profesores p
    INNER JOIN cursos c
    ON p.id = c.profesor_id
    LEFT JOIN calificaciones ca
    ON c.id = ca.curso_id
    GROUP BY p.nombre;

b) Mejores notas de cada alumno

    SELECT e.nombre, cur.asignatura, MAX(c.nota) FROM estudiantes e
    INNER JOIN calificaciones c
    ON e.id = c.estudiante_id
    INNER JOIN cursos cur
    ON c.curso_id = cur.id
    GROUP BY e.nombre;

c) Ordenar a los estudiantes por cursos en los que están inscritos

    SELECT c.asignatura, e.nombre FROM cursos c
    INNER JOIN estudiantes_cursos ec
    ON c.id = ec.curso_id
    INNER JOIN estudiantes e
    ON ec.estudiante_id = e.id
    ORDER BY c.asignatura;

d) Crear informe resumido de cursos y sus cualificaciones promedio, ordenados por el curso más desafiante (curso con la calificación promedio más baja) 
hasta el curso más fácil.

    SELECT c.asignatura, AVG(ca.nota) AS nota_promedio FROM cursos c
    INNER JOIN calificaciones ca
    ON c.id = ca.curso_id
    GROUP BY c.asignatura
    ORDER BY nota_promedio ASC;

e) Encontrar que estudiante y profesor tienen más cursos en común

> Como aquí tngo 3 resultados muestro el primero.

    SELECT p.nombre AS profesor, e.nombre AS estudiante, COUNT(e.nombre) AS cursos_en_comun FROM profesores p
    INNER JOIN cursos c
    ON p.id = c.profesor_id
    INNER JOIN estudiantes e
    INNER JOIN estudiantes_cursos ec
    ON e.id = ec.estudiante_id
    INNER JOIN cursos c1
    ON ec.curso_id = c1.id
    ON c.asignatura = c1.asignatura
    GROUP BY p.nombre, e.nombre
    ORDER BY cursos_en_comun DESC, p.nombre ASC
    LIMIT 1;




