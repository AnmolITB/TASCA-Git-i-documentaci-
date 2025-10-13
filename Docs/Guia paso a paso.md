# Documentación de Instalación y Despliegue

Este documento detalla el proceso de instalación y configuración del entorno necesario para el despliegue de la aplicación web del proyecto. Se describen los pasos para configurar el servidor, la base de datos y desplegar la versión inicial del código con errores.

---

## 1. Arquitectura del Sistema

Para este proyecto, se ha implementado una arquitectura de servidor único (también conocida como "all-in-one"). Todos los servicios necesarios para el funcionamiento de la aplicación residen en una misma máquina virtual.

* **Sistema Operativo:** Ubuntu 24.04
* **Servidor Web:** Apache2
* **Base de Datos:** MariaDB Server
* **Lenguaje de Programación:** PHP 8.3.6 con los módulos necesarios para Apache y MySQL (`php`, `php-mysql`, `libapache2-mod-php`)

---

## 2. Preparación del Entorno y Conexión a GitHub

Antes de instalar los servicios, se preparó el entorno para trabajar con el repositorio de Git donde se aloja el código.

### 2.1. Creación de Claves SSH para GitHubFinalmente, se desplegó el código PHP de la aplicación en el directorio raíz del servidor web.

Limpieza del Directorio Web: Primero, se vació el directorio /var/www/html para asegurar que no quedaran archivos residuales.



Para establecer una conexión segura y autenticada con GitHub sin necesidad de introducir usuario y contraseña en cada operación, se generó un par de claves SSH.

```bash
ssh-keygen -t ed25519 -C "anmolpreet.singh.kaur.7e8@itb.cat"
```
### 2.2. Verificación de la Conexión SSH

Una vez añadida la clave pública a GitHub, se verificó que la conexión funcionara correctamente con el siguiente comando.

```Bash
ssh -T git@github.com
```
La respuesta del servidor "Hi AnmolITB! You've successfully authenticated..." confirma que la configuración es correcta.

### 2.3. Clonación del Repositorio
Con la conexión a GitHub ya establecida, se clonó el repositorio del proyecto en la máquina local para tener acceso al código fuente.

```Bash
git clone [https://github.com/AnmolITB/TASCA-Git-i-documentaci-.git](https://github.com/AnmolITB/TASCA-Git-i-documentaci-.git)
```
Este comando descarga el contenido del repositorio en un nuevo directorio llamado TASCA-Git-i-documentaci-.

---

## 3. Instalación de Servicios (Stack LAMP)
Se instalaron todos los paquetes de software necesarios (Apache, MariaDB y PHP) con un único comando para montar el stack LAMP (Linux, Apache, MariaDB, PHP).
```Bash
sudo apt -y install apache2 php php-mysql libapache2-mod-php mariadb-server
```
Este comando descarga e instala el servidor web Apache, PHP junto a sus módulos de integración con Apache y MySQL, y el servidor de bases de datos MariaDB.
### 3.1. Habilitación de los Servicios
Una vez instalados, se activaron y arrancaron los servicios de Apache y MariaDB para asegurar que se inicien automáticamente con el sistema.

```Bash
sudo systemctl enable --now apache2 mariadb
```
El flag --now no solo los habilita para el arranque, sino que también los inicia en el mismo momento.

---

# 4. Verificación del Servidor Web y PHP
Para confirmar que el servidor web y el intérprete de PHP funcionaban correctamente, se creó un archivo de prueba en el directorio raíz del servidor web (/var/www/html/).
```Bash
echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/info.php > /dev/null
```
Este comando crea un archivo llamado info.php que ejecuta la función phpinfo(), la cual muestra toda la información de la configuración de PHP. Al acceder a la dirección http://<IP_DEL_SERVIDOR>/info.php desde un navegador, se pudo verificar que PHP v8.3.6 estaba activo y correctamente integrado con Apache.

---

# 5. Configuración de la Base de Datos
El siguiente paso fue preparar la base de datos que utilizará la aplicación.

## 5.1. Acceso a MariaDB
Se accedió a la consola de MariaDB como usuario root para poder ejecutar comandos de administración.

```Bash
sudo mysql -u root -p
```
## 5.2. Creación de la Base de Datos y la Tabla
Dentro de la consola de MariaDB, se crearon la base de datos crud_db y la tabla users necesaria para la aplicación.

```SQL
-- Creación de la base de datos
CREATE DATABASE crud_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```
```SQL
-- Selección de la base de datos
USE crud_db;
```
```SQL
-- Creación de la tabla de usuarios
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL
);
```
---

# 6. Despliegue de la Aplicación Inicial
Finalmente, se desplegó el código PHP de la aplicación en el directorio raíz del servidor web.

* **Limpieza del Directorio Web:** Primero, se vació el directorio /var/www/html para asegurar que no quedaran archivos residuales.
```Bash
sudo rm -rf "/var/www/html"/*
```
* **Copia de Ficheros:** Se copiaron los archivos de la aplicación (index.php, db.php, add.php, edit.php, delete.php) desde el directorio del repositorio clonado (~/TASCA-Git-i-documentaci-/Código Completo con errores) al directorio /var/www/html/. Aunque el comando de copia no aparece explícitamente, los pasos posteriores de edición y el contexto lo confirman.
* **Configuración:** Se editó el fichero db.php para ajustar los parámetros de conexión a la base de datos (servername, username, password, dbname).
Con estos pasos, la versión inicial de la aplicación, que contiene errores, quedó desplegada y lista para la siguiente fase del proyecto: la identificación y corrección de bugs.







# Corrección de Errores en Aplicación CRUD PHP

En este documento se detallan los errores encontrados y corregidos en el código de una aplicación CRUD (Create, Read, Update, Delete) simple desarrollada con PHP y MySQL.

---

## PARTE 2: CÓDIGO COMPLETO

### 1. `db.php`

* **Error:** La dirección del host de la base de datos estaba mal escrita como `locahost`.
* **Explicación:** `localhost` es el nombre de host estándar para referirse a la máquina local. Un error tipográfico en este valor impide que la aplicación se conecte al servidor de la base de datos MySQL, ya que no puede resolver la dirección correcta.
* **Solución:** Se corrigió el error tipográfico de `locahost` a `localhost`.

    ```php
    $servername = "localhost";
    $username = "root";
    $password = "root";
    $dbname = "crud_db";
    ```

---

### 2. Script SQL

* **Error:** Se utilizó una cláusula `WHERE FALSE` inválida en la declaración `CREATE DATABASE`.
* **Explicación:** La sintaxis de SQL para crear una base de datos no admite la cláusula `WHERE`. Esta construcción es sintácticamente incorrecta y provocaría un error al ejecutar el script.
* **Solución:** Se eliminó la cláusula `WHERE FALSE` para cumplir con la sintaxis SQL estándar.

    ```sql
    CREATE DATABASE crud_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
    ```

---

### 3. `index.php`

* **Error 1:** La etiqueta `<table>` estaba abierta dos veces consecutivas.
    * **Explicación:** Duplicar etiquetas de apertura en HTML puede causar problemas de renderizado en el navegador y lleva a una estructura de DOM inválida.
    * **Solución:** Se eliminó la etiqueta `<table>` redundante.

* **Error 2:** El método del formulario de creación estaba especificado como `"posts"` en lugar de `"post"`.
    * **Explicación:** El atributo `method` en un formulario HTML solo acepta valores válidos de métodos HTTP. El valor correcto para enviar datos es `post` (o `get`), no `posts`.
    * **Solución:** Se corrigió el valor del atributo a `method="post"`.

    ```html
    <form action="add.php" method="post">
    ```

---

### 4. `add.php`

* **Error:** La sintaxis en la cláusula `VALUES` de la consulta `INSERT` era incorrecta (`VALUES (*, ?)`).
* **Explicación:** La sintaxis `VALUES (*, ?)` no es válida en SQL para una inserción. Se deben especificar los marcadores de posición (`?`) para cada columna que recibirá un valor.
* **Solución:** Se corrigió la consulta para usar un marcador de posición para cada columna (`name` y `email`).

    ```php
    $stmt = $conn->prepare("INSERT INTO users (name, email) VALUES (?, ?)");
    ```

---

### 5. `edit.php`

* **Error:** La sintaxis de la consulta `UPDATE` era incorrecta (`UPDATE users where name=?, email=? WHERE id=?`).
* **Explicación:** La sintaxis correcta para una actualización en SQL requiere la palabra clave `SET` para asignar nuevos valores a las columnas. El uso de `where` en lugar de `SET` es un error de sintaxis.
* **Solución:** Se reestructuró la consulta para utilizar la sintaxis `UPDATE ... SET ... WHERE ...` correcta.

    ```php
    $stmt = $conn->prepare("UPDATE users SET name=?, email=? WHERE id=?");
    ```

---

### 6. `delete.php`

* **Error:** Se utilizó un asterisco (`*`) en la consulta `DELETE` (`DELETE * FROM ...`).
* **Explicación:** La sentencia `DELETE` en SQL elimina filas completas, no columnas individuales, por lo que no se debe usar `*`. El asterisco se reserva para `SELECT` para indicar "todas las columnas".
* **Solución:** Se eliminó el asterisco (`*`) de la consulta para que fuera sintácticamente correcta.

    ```php
    $conn->query("DELETE FROM users WHERE id=$id");
    ```
