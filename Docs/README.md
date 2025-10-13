# Proyecto: Despliegue y Depuración de Aplicación CRUD

Este proyecto documenta el proceso completo de puesta en marcha y corrección de una aplicación web CRUD (Crear, Leer, Actualizar y Borrar). El objetivo es mostrar el ciclo de vida desde la configuración de un servidor hasta la identificación y solución de errores en el código fuente.

## Descripción General

El proyecto se divide en dos fases principales:

1.  **Infraestructura y Despliegue Inicial:** Se detalla la preparación de un servidor web desde cero, instalando y configurando todos los servicios necesarios para alojar la aplicación. En esta fase, se despliega intencionadamente una versión del código que contiene errores.
2.  **Análisis y Corrección de Errores:** Se identifican y solucionan los fallos presentes en el código PHP y SQL de la aplicación, explicando la causa de cada uno y la lógica detrás de la corrección para dejarla en un estado funcional.

## Tecnologías y Arquitectura

La aplicación se despliega en una arquitectura de servidor único (*all-in-one*), utilizando un stack tecnológico estándar basado en LAMP.

-   **Sistema Operativo:** Ubuntu 24.04
-   **Servidor Web:** Apache2
-   **Base de Datos:** MariaDB
-   **Lenguaje de Programación:** PHP 8.3.6

Para la gestión del código fuente y el control de versiones, se utiliza **Git** y **GitHub**.

## Resumen de Correcciones Realizadas

La depuración del código abordó varios tipos de errores comunes en el desarrollo web:

-   **Errores de conexión con la base de datos:** Se corrigió un error tipográfico en los parámetros de conexión que impedía la comunicación con MariaDB.
-   **Errores de sintaxis SQL:** Se reescribieron las consultas de inserción, actualización y borrado (`INSERT`, `UPDATE`, `DELETE`) para adecuarlas a la sintaxis estándar de SQL.
-   **Errores en el código HTML:** Se solucionaron problemas de estructura, como etiquetas duplicadas y atributos incorrectos en los formularios, que afectaban al renderizado y la funcionalidad.
-   **Errores de lógica en PHP:** Se ajustó la forma en que los ficheros PHP procesaban los datos y construían las consultas a la base de datos.
