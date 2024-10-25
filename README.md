# Como Crear una Lista de Tareas sin Bases de Datos SQL Redis ni MongoDB

### Introducción
Desarrollar aplicaciones web suele implicar el uso de bases de datos para almacenar y gestionar datos. Sin embargo, cuando trabajamos en aplicaciones ligeras, existen alternativas que evitan la necesidad de un servidor de base de datos. Este artículo presenta una manera de crear una aplicación de lista de tareas (*To-Do List*) sin SQL, MongoDB o Redis, aprovechando `localStorage` del navegador para la persistencia de datos y manteniendo la aplicación sencilla y eficiente.

### Características de la Aplicación

1. **Almacenamiento Local en el Navegador**: 
   - Esta aplicación utiliza `localStorage` para almacenar y cargar tareas. Al no requerir una base de datos, los datos se guardan directamente en el navegador del usuario, haciendo que esta solución sea adecuada para prototipos y aplicaciones pequeñas.

2. **Interfaz Intuitiva y Ligera**: 
   - Diseñada con HTML y CSS, la interfaz es simple pero efectiva. Permite al usuario agregar tareas en segundos y visualizarlas sin complicaciones.

3. **Fácil de Mantener y Extender**: 
   - Con lógica escrita en JavaScript puro, el código es fácil de entender y modificar, haciéndolo ideal para aquellos que buscan aprender sobre desarrollo de aplicaciones sin bases de datos complejas.

---

### 1. Estructura de Archivos

Para organizar la aplicación, utilizamos cuatro archivos:

- **`index.html`**: Define la estructura visual de la aplicación, con un formulario para añadir tareas y una lista donde se muestran las tareas guardadas.
- **`style.css`**: Contiene los estilos visuales, creando una apariencia limpia y amigable.
- **`script.js`**: Controla toda la lógica de la aplicación, como cargar y guardar tareas en `localStorage`.
- **`tasks.json`**: Este archivo incluye datos de ejemplo de tareas, que podrían integrarse en una futura actualización.

### 2. Creación de la Interfaz de Usuario (index.html)

Este archivo define la estructura básica de la aplicación y permite al usuario interactuar con la lista de tareas. Incluye un formulario que permite añadir tareas y una lista que muestra todas las tareas almacenadas.

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lista de Tareas sin Base de Datos</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>Lista de Tareas</h1>
    <form id="taskForm">
        <input type="text" id="newTask" placeholder="Nueva tarea...">
        <button type="submit">Agregar</button>
    </form>
    <ul id="taskList"></ul>
    <script src="script.js"></script>
</body>
</html>
