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

### 3. Estilo Visual de la Aplicación (style.css)

El diseño de la aplicación es simple para garantizar una experiencia clara y fácil de usar. Usamos CSS básico para los elementos de la página y definimos colores y márgenes para hacerla más atractiva visualmente.

```css
body {
    font-family: Arial, sans-serif;
    display: flex;
    flex-direction: column;
    align-items: center;
    background-color: #f4f4f9;
}
h1 {
    color: #333;
}
form {
    margin: 15px;
}
input, button {
    padding: 10px;
    margin: 5px;
}
ul {
    list-style: none;
    padding: 0;
    width: 300px;
}
li {
    background-color: #ececec;
    margin: 5px;
    padding: 10px;
}


### 4. Lógica de la Aplicación (script.js)

Toda la lógica de la aplicación se controla desde este archivo JavaScript, que incluye funciones para cargar las tareas desde `localStorage`, agregar nuevas tareas y mantener los datos actualizados.

- **`loadTasks()`**: Se ejecuta al cargar la página, obtiene las tareas de `localStorage` y las muestra en la lista de tareas.
- **`saveTask(task)`**: Guarda una nueva tarea en `localStorage`.
- **Formulario de Tareas**: Captura el evento `submit` para agregar tareas sin recargar la página.

```javascript
document.addEventListener('DOMContentLoaded', loadTasks);

function loadTasks() {
    const taskList = document.getElementById('taskList');
    const tasks = JSON.parse(localStorage.getItem('tasks')) || [];
    taskList.innerHTML = '';
    tasks.forEach(task => {
        const li = document.createElement('li');
        li.textContent = task;
        taskList.appendChild(li);
    });
}

document.getElementById('taskForm').addEventListener('submit', function (e) {
    e.preventDefault();
    const newTaskInput = document.getElementById('newTask');
    const newTask = newTaskInput.value.trim();
    if (newTask) {
        saveTask(newTask);
        newTaskInput.value = '';
        loadTasks();
    }
});

function saveTask(task) {
    const tasks = JSON.parse(localStorage.getItem('tasks')) || [];
    tasks.push(task);
    localStorage.setItem('tasks', JSON.stringify(tasks));
}

### 5. Archivo JSON con Datos Iniciales (tasks.json)

Este archivo contiene datos de ejemplo que podrían utilizarse para poblar la lista de tareas en una versión futura de la aplicación. Aunque no se carga dinámicamente en esta versión, proporciona un ejemplo de cómo se podrían almacenar las tareas inicialmente.

```json
[
    "Completar proyecto de la universidad",
    "Leer un libro de ciencia ficción",
    "Hacer ejercicio"
]

### Explicación del Uso de localStorage

En lugar de una base de datos de servidor, esta aplicación utiliza `localStorage`, una API de almacenamiento en el navegador que permite guardar datos de manera simple y rápida.

- **Simplicidad**: `localStorage` permite guardar datos en formato JSON directamente en el navegador, evitando la configuración de una base de datos.
- **Persistencia Local**: Los datos guardados en `localStorage` permanecen disponibles mientras no se borren manualmente los datos del navegador, proporcionando persistencia sin necesidad de conexión al servidor.

#### En esta aplicación:

1. **Carga de Tareas**: `loadTasks()` recupera las tareas guardadas y las muestra al usuario.
2. **Agregar Nuevas Tareas**: `saveTask()` guarda cada tarea nueva en `localStorage`.
3. **Sesiones Persistentes**: Las tareas se mantienen entre sesiones, siempre que el usuario no borre los datos de su navegador.

### Ventajas del Uso de localStorage

1. **Fácil de Implementar**: No requiere configuraciones adicionales, por lo que es ideal para aplicaciones pequeñas.
2. **Persistencia entre Sesiones**: Las tareas se mantienen en `localStorage` entre sesiones, lo cual es útil para datos no sensibles.
3. **Rendimiento Rápido**: `localStorage` funciona directamente en el navegador, eliminando la necesidad de llamadas a un servidor y mejorando la velocidad.

### Conclusión

Este artículo ha demostrado cómo crear una aplicación de lista de tareas sin depender de bases de datos de servidor. `localStorage` ofrece una solución sencilla para almacenar y recuperar datos, lo que convierte esta aplicación en una excelente opción para prototipos y aplicaciones pequeñas.



