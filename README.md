APLICACION CRUD

Tecnologías Utilizadas
PHP: Es un lenguaje de script del lado del servidor ampliamente utilizado en el desarrollo web debido a su capacidad para generar contenido dinámico.

MySQL: Se emplea como sistema de gestión de base de datos relacional para almacenar y administrar los datos de los usuarios. Es popular por su confiabilidad y velocidad.

HTML & CSS: Se utilizan para estructurar las páginas web y darles estilo, respectivamente. HTML define la estructura del contenido y CSS controla su presentación.

Tailwind CSS: Es un framework de CSS utilitario que proporciona clases predefinidas para diseñar interfaces de usuario de manera rápida y eficiente. Ayuda a mantener un código más limpio y modular.

Páginas y Funcionalidades
Página de Inicio (display.php): Muestra una tabla con todos los usuarios registrados en la base de datos. Permite ver todos los usuarios y ofrece enlaces de navegación para agregar, editar o eliminar información de usuario.

Agregar Usuario (user.php): Proporciona un formulario para ingresar los detalles de un nuevo usuario, como nombre, correo electrónico, teléfono móvil y contraseña. Valida los datos ingresados antes de enviarlos a la base de datos.

Editar Usuario (edit.php): Permite modificar los detalles de un usuario existente. El formulario se rellena automáticamente con la información actual del usuario y se actualiza en la base de datos después de la edición.

Eliminar Usuario (delete.php): Facilita la eliminación de un usuario de la base de datos basada en su ID.

Conexión a la Base de Datos (connect.php)
Propósito: Establece una conexión con la base de datos MySQL.
Credenciales: Utiliza el nombre de host, nombre de usuario, contraseña y nombre de la base de datos para la conexión.
Ejecución
Clonación del Repositorio: Se requiere clonar el repositorio en la máquina local donde se ejecutará la aplicación.

Configuración del Entorno PHP y MySQL: Se necesita un entorno de desarrollo local, como XAMPP, que incluya PHP y MySQL.

Creación de la Base de Datos: Utilizando phpMyAdmin u otra herramienta similar, se debe crear la base de datos necesaria para almacenar los datos de usuario.

Ejecución de la Aplicación: Una vez configurado el entorno y la base de datos, la aplicación puede ser ejecutada en un servidor local para su funcionamiento.

Nota de Seguridad
Se advierte que esta aplicación es una demostración básica y no implementa medidas avanzadas de seguridad. Se recomienda utilizar declaraciones preparadas (prepared statements) u ORM para las interacciones con la base de datos a fin de prevenir ataques de inyección SQL.

Ejemplo básico de un CRUD (Crear, Leer, Actualizar, Eliminar) utilizando PHP y MySQL en un entorno LAMP (Linux, Apache, MySQL, PHP) en un servidor AWS:

1.Crear la base de datos y la tabla en MySQL:

CREATE DATABASE IF NOT EXISTS mi_base_de_datos;
USE mi_base_de_datos;

CREATE TABLE IF NOT EXISTS usuarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(50),
    email VARCHAR(50)
);

2.Conexión a la base de datos en PHP:

<?php
$servidor = "localhost";
$usuario = "nombre_de_usuario";
$password = "contraseña";
$base_de_datos = "mi_base_de_datos";

$conexion = mysqli_connect($servidor, $usuario, $password, $base_de_datos);

if (!$conexion) {
    die("Error al conectar con la base de datos: " . mysqli_connect_error());
}
?>
3.Crear (Create):

<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $nombre = $_POST["nombre"];
    $email = $_POST["email"];

    $sql = "INSERT INTO usuarios (nombre, email) VALUES ('$nombre', '$email')";

    if (mysqli_query($conexion, $sql)) {
        echo "Usuario creado correctamente.";
    } else {
        echo "Error al crear usuario: " . mysqli_error($conexion);
    }
}
?>

<?php
$sql = "SELECT * FROM usuarios";
$resultado = mysqli_query($conexion, $sql);

if (mysqli_num_rows($resultado) > 0) {
    while ($fila = mysqli_fetch_assoc($resultado)) {
        echo "ID: " . $fila["id"] . " - Nombre: " . $fila["nombre"] . " - Email: " . $fila["email"] . "<br>";
    }
} else {
    echo "No se encontraron usuarios.";
}
?>

5.Actualizar (Update):
<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $id = $_POST["id"];
    $nombre = $_POST["nombre"];
    $email = $_POST["email"];

    $sql = "UPDATE usuarios SET nombre='$nombre', email='$email' WHERE id=$id";

    if (mysqli_query($conexion, $sql)) {
        echo "Usuario actualizado correctamente.";
    } else {
        echo "Error al actualizar usuario: " . mysqli_error($conexion);
    }
}
?>


6.Eliminar (Delete):
<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $id = $_POST["id"];

    $sql = "DELETE FROM usuarios WHERE id=$id";

    if (mysqli_query($conexion, $sql)) {
        echo "Usuario eliminado correctamente.";
    } else {
        echo "Error al eliminar usuario: " . mysqli_error($conexion);
    }
}
?>
