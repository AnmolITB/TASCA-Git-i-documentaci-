





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
