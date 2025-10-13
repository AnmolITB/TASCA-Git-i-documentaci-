# 🧠 PROJECTE CRUD PHP + MariaDB

Aquest projecte mostra el procés complet de creació i desplegament d’una aplicació **CRUD** (Create, Read, Update, Delete) amb **PHP**, **Apache2** i **MariaDB**, integrant la gestió de versions amb **GitHub**.

---

## ⚙️ Procediment pas a pas

### 1️⃣ Generació de clau SSH
Es crea una clau SSH per connectar-se amb GitHub sense contrasenya.

```bash
ssh-keygen -t ed25519 -C "anmolpreet.singh.kaur.7e8@itb.cat"
```
![Generació clau SSH](img/1_sshkeygen.png)

---

### 2️⃣ Connexió amb GitHub
Es comprova la connexió SSH amb GitHub per assegurar la identificació.
```bash
ssh -T git@github.com
```
![Connexió GitHub SSH](img/2_ssh_github.png)

---

### 3️⃣ Clonació del repositori
Es clona el repositori del projecte al directori local.
```bash
git clone https://github.com/AnmolITB/TASCA-Git-i-documentaci.git
```
![Clonació del repositori](img/3_git_clone.png)

---

### 4️⃣ Instal·lació del servidor LAMP
Es configuren Apache2, PHP i MariaDB.
```bash
sudo apt -y install apache2 php php-mysql libapache2-mod-php mariadb-server
```
![Instal·lació LAMP](img/4_lamp_install.png)

---

### 5️⃣ Activació dels serveis
S’inicien automàticament Apache2 i MariaDB.
```bash
sudo systemctl enable --now apache2 mariadb
```
![Activació serveis](img/5_enable_services.png)

---

### 6️⃣ Neteja del directori web
Es buida `/var/www/html` per preparar el desplegament.
```bash
sudo rm -rf /var/www/html/*
```
![Neteja directori](img/6_rm_html.png)

---

### 7️⃣ Verificació de PHP
Es crea un fitxer `info.php` i es comprova la seva execució al navegador.
```bash
echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/info.php > /dev/null
```
![Prova phpinfo](img/7_phpinfo.png)

---

### 8️⃣ Creació de la base de dades
Es crea `crud_db` i la taula `users` per guardar la informació.
```bash
CREATE DATABASE crud_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
USE crud_db;
CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  email VARCHAR(100) NOT NULL
);
```
![Creació base de dades](img/8_db_creation.png)

---

### 9️⃣ Definició del directori font
Es defineix la ruta del codi del projecte CRUD.
```bash
SRC="$HOME/TASCA-Git-i-documentaci-/Código Completo con errores"
```
![Variable SRC](img/9_src_path.png)

---

### 🔟 Creació dels fitxers PHP
Es creen `db.php`, `index.php`, `add.php`, `edit.php` i `delete.php`.
```bash
nano ~/crud/db.php
nano ~/crud/index.php
nano ~/crud/add.php
nano ~/crud/edit.php
nano ~/crud/delete.php
```
![Creació fitxers CRUD](img/10_create_files.png)

---

### 11️⃣ Connexió a la base de dades
S’estableix la connexió amb MariaDB des de PHP.
```php
<?php
$servername = "localhost";
$username = "root";
$password = "root";
$dbname = "crud_db";

$conn = new mysqli($servername, $username, $password, $dbname);

if ($conn->connect_error) {
    die("Connexió fallida: " . $conn->connect_error);
}
?>
```
![Connexió DB](img/11_db_php.png)

---

### 12️⃣ Execució amb errors
Es prova el CRUD inicialment i es detecten fallades.
![Codi erroni](img/12_codi_erroni.png)

---

### 13️⃣ Correcció del codi
Es solucionen els errors i el CRUD ja funciona correctament.
![Codi corregit](img/13_codi_funcional.png)

---

### 14️⃣ Afegir un usuari nou
Es comprova el formulari afegint un registre nou.
![Afegir usuari](img/14_afegir_usuari.png)

---

### 15️⃣ Visualització d’usuaris
Es mostra la taula amb les dades introduïdes.
![Usuari a la llista](img/15_llista_usuari.png)

---

### 16️⃣ CRUD complet
El sistema permet afegir, editar i eliminar usuaris des de la web.
![CRUD complet](img/16_crud_complet.png)

---

## 💡 Resultat final

El projecte **CRUD PHP + MariaDB** ha estat desplegat amb èxit sobre un servidor **Apache2** amb suport **PHP 8.3** i connexió segura a **MariaDB**.  
Totes les operacions del CRUD funcionen correctament i s’han verificat mitjançant el navegador local.

---

## 🧰 Tecnologies utilitzades

- 🐧 **Ubuntu 24.04**
- 🌐 **Apache2**
- 🐘 **PHP 8.3**
- 🗄️ **MariaDB**
- 🔗 **Git / GitHub**

---

## 🧑‍💻 Autor

**Anmolpreet Singh Kaur**  
ITB — CFGS ASIXc — Administració de Sistemes Operatius  
📧 [anmolpreet.singh.kaur.7e8@itb.cat](mailto:anmolpreet.singh.kaur.7e8@itb.cat)
