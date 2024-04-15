# Aplicación CRUD de PHP

Este repositorio contiene una aplicación PHP CRUD (Create, Read, Update, Delete) simple. Es una demostración básica de cómo integrar PHP con una base de datos MySQL para gestionar datos de usuarios. La aplicación permite a los usuarios agregar, ver, editar y eliminar información de usuario.

## Tecnologías Utilizadas

- **PHP:** Lenguaje de script del lado del servidor utilizado para el desarrollo web.
- **MySQL:** Sistema de gestión de base de datos utilizado para almacenar datos de usuario.
- **HTML & CSS:** Utilizados para estructurar y dar estilo a las páginas web.
- **Tailwind CSS:** Un framework de CSS utilitario para el desarrollo rápido de interfaces de usuario.

## Páginas y Funcionalidades

### 1. Página de Inicio (`display.php`)

![Página de Inicio](images/display.png)

- **Funcionalidad:** Muestra todos los usuarios de la base de datos en un formato de tabla.
- **Características:** 
  - Ver todos los usuarios.
  - Enlaces de navegación para agregar, editar o eliminar información de usuario.

### 2. Agregar Usuario (`user.php`)

![Agregar Usuario](images/add.png)

- **Funcionalidad:** Permite agregar un nuevo usuario a la base de datos.
- **Características:** 
  - Formulario para ingresar detalles del usuario (nombre, correo electrónico, teléfono móvil, contraseña).
  - Validación de datos y envío a la base de datos.

### 3. Editar Usuario (`edit.php`)

![Editar Usuario](images/edit.png)

- **Funcionalidad:** Permite editar detalles de usuarios existentes.
- **Características:** 
  - Formulario prellenado con la información actual del usuario.
  - Actualización de detalles del usuario en la base de datos.

### 4. Eliminar Usuario (`delete.php`)

- **Funcionalidad:** Facilita la eliminación de un usuario de la base de datos.
- **Características:** 
  - Eliminación de información de usuario basada en el ID de usuario.

## Conexión a la Base de Datos (`connect.php`)

- **Propósito:** Establece una conexión con la base de datos MySQL.
- **Credenciales:** Utiliza nombre de host, nombre de usuario, contraseña y nombre de la base de datos para la conexión.

## Cómo Ejecutar

1. Clona el repositorio en tu máquina local.
2. Configura un entorno PHP y MySQL (como XAMPP).
3. Crea la base de datos usando phpmyadmin.
4. Ejecuta la aplicación en un servidor local.

## Nota de Seguridad

Esta aplicación es una demostración básica y no implementa medidas avanzadas de seguridad. Es recomendable utilizar declaraciones preparadas (prepared statements) u ORM para las interacciones con la base de datos para prevenir ataques de inyección SQL.

##Configuración de la Base de Datos (config.php):

php
Copy code
<?php
$servername = "localhost";
$username = "tu_usuario";
$password = "tu_contraseña";
$database = "tu_basededatos";

$conn = new mysqli($servername, $username, $password, $database);

if ($conn->connect_error) {
    die("Error de conexión: " . $conn->connect_error);
}
?>
Crear (create.php):

php
Copy code
<?php include 'config.php'; ?>

<form action="create.php" method="POST">
    Nombre: <input type="text" name="nombre">
    Email: <input type="email" name="email">
    <input type="submit" value="Agregar">
</form>

<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $nombre = $_POST["nombre"];
    $email = $_POST["email"];

    $sql = "INSERT INTO usuarios (nombre, email) VALUES ('$nombre', '$email')";

    if ($conn->query($sql) === TRUE) {
        echo "Usuario creado correctamente.";
    } else {
        echo "Error al crear usuario: " . $conn->error;
    }
}
?>
Leer (read.php):

php
Copy code
<?php include 'config.php'; ?>

<?php
$sql = "SELECT * FROM usuarios";
$result = $conn->query($sql);

if ($result->num_rows > 0) {
    while($row = $result->fetch_assoc()) {
        echo "ID: " . $row["id"]. " - Nombre: " . $row["nombre"]. " - Email: " . $row["email"]. "<br>";
    }
} else {
    echo "No se encontraron usuarios.";
}
?>
Actualizar (update.php):

php
Copy code
<?php include 'config.php'; ?>

<form action="update.php" method="POST">
    ID a actualizar: <input type="text" name="id">
    Nuevo nombre: <input type="text" name="nombre">
    Nuevo email: <input type="email" name="email">
    <input type="submit" value="Actualizar">
</form>

<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $id = $_POST["id"];
    $nombre = $_POST["nombre"];
    $email = $_POST["email"];

    $sql = "UPDATE usuarios SET nombre='$nombre', email='$email' WHERE id=$id";

    if ($conn->query($sql) === TRUE) {
        echo "Usuario actualizado correctamente.";
    } else {
        echo "Error al actualizar usuario: " . $conn->error;
    }
}
?>
Eliminar (delete.php):

php
Copy code
<?php include 'config.php'; ?>

<form action="delete.php" method="POST">
    ID a eliminar: <input type="text" name="id">
    <input type="submit" value="Eliminar">
</form>

<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $id = $_POST["id"];

    $sql = "DELETE FROM usuarios WHERE id=$id";

    if ($conn->query($sql) === TRUE) {
        echo "Usuario eliminado correctamente.";
    } else {
        echo "Error al eliminar usuario: " . $conn->error;
    }
}
?>
