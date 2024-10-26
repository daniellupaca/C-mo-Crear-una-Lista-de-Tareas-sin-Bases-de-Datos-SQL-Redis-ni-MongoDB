
# Creating an Application with Firestore: A NoSQL Alternative from Google

**Author:** [Ronal Daniel Lupaca Mamani]    
---

### Introduction

Today, mobile and web applications increasingly require a database that enables real-time synchronization without the complexity of an SQL server. Google Firestore, a NoSQL cloud database, offers exactly that: real-time storage and scalability without the need to manage servers. In this article, I want to show you how to create a simple To-Do List application using Firestore to perform CRUD operations (Create, Read, Update, and Delete).

Firestore is ideal for this type of application as it allows data to be stored and synchronized in real-time across multiple devices. Moreover, its integration with Firebase makes it a powerful tool for web and mobile applications.

---

### What is Firestore?

Firestore is part of Google's Firebase platform and is a NoSQL cloud database that allows real-time data storage and synchronization. Firestore organizes data into documents and collections, which is ideal for structured data and allows us to have a serverless database. Some key features include:

- **Real-time synchronization:** Data is instantly updated on all connected devices.
- **Automatic scalability:** It can handle large volumes of data and traffic seamlessly.
- **Integration with Firebase and Google Cloud Platform:** It is easy to add authentication and permissions.

---

### Project Goal

In this project, I want to create a To-Do List application where we can:

- Add new tasks.
- View all stored tasks.
- Edit and delete tasks.
- Automatically synchronize data in real-time.

---

### Project Structure

We organize the application into the following files:

1. **`index.html`**: The application's user interface.
2. **`style.css`**: The application's styles.
3. **`app.js`**: The application logic and Firestore connection.

---

### Step 1: Firestore Setup in Firebase

1. **Create a Project in Firebase**:
   - Log in to the [Firebase Console](https://console.firebase.google.com/) and create a new project.

2. **Enable Firestore**:
   - In the Firebase console, go to the Firestore Database section and enable it in test mode (for development).

3. **Download the Configuration File**:
   - In the project settings, select "Add web app" to obtain the configuration file (`firebaseConfig`), necessary to connect the application to Firebase.

---

### Step 2: Create the User Interface (index.html)

In `index.html`, we set up a simple interface with a form to add tasks and a list where stored tasks will be displayed:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To-Do List with Firestore</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>To-Do List</h1>
    <form id="taskForm">
        <input type="text" id="newTask" placeholder="New task..." required>
        <button type="submit">Add</button>
    </form>
    <ul id="taskList"></ul>
    <script src="https://www.gstatic.com/firebasejs/9.6.0/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.6.0/firebase-firestore.js"></script>
    <script src="app.js"></script>
</body>
</html>
```

---

### Step 3: Application Styles (style.css)

This file provides a simple design for the application:

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
    display: flex;
    justify-content: space-between;
}
```

---

### Step 4: Application Logic and Firestore Connection (app.js)

This file contains the application logic and the CRUD functions that interact with Firestore:

```javascript
// Firebase Configuration
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_AUTH_DOMAIN",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_STORAGE_BUCKET",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
    appId: "YOUR_APP_ID"
};

// Initialize Firebase
firebase.initializeApp(firebaseConfig);
const db = firebase.firestore();

// Function to load all tasks
function loadTasks() {
    const taskList = document.getElementById("taskList");
    taskList.innerHTML = "";

    db.collection("tasks").onSnapshot((snapshot) => {
        snapshot.forEach((doc) => {
            const task = doc.data().task;
            const li = document.createElement("li");
            li.textContent = task;
            li.appendChild(createDeleteButton(doc.id));
            taskList.appendChild(li);
        });
    });
}

// Function to add a new task
document.getElementById("taskForm").addEventListener("submit", async (e) => {
    e.preventDefault();
    const newTaskInput = document.getElementById("newTask");
    const newTask = newTaskInput.value.trim();

    if (newTask) {
        await db.collection("tasks").add({ task: newTask });
        newTaskInput.value = "";
    }
});

// Function to delete a task
function createDeleteButton(id) {
    const btn = document.createElement("button");
    btn.textContent = "Delete";
    btn.onclick = async () => {
        await db.collection("tasks").doc(id).delete();
    };
    return btn;
}

// Load tasks when the application starts
document.addEventListener("DOMContentLoaded", loadTasks);
```

---

### Advantages of Using Firestore

- **Real-time Synchronization**: Firestore allows all connected devices to synchronize data automatically.
- **Automatic Scalability**: Firestore handles large amounts of data and traffic without manual adjustments.
- **Built-in Security**: With Firebase Authentication integration, it's easy to apply access rules and protect data.

---

### Conclusion

Creating this To-Do List application with Firestore allowed me to explore a NoSQL cloud database that is excellent for storing and synchronizing data in real-time. Thanks to Firestore, I can avoid setting up an SQL server and simplify the development process, which is ideal for collaborative or lightweight applications.

**GitHub Code Link**: [GitHub Repository](https://github.com/your-username/my-firestore-project)

**References**  
- Google Developers. (n.d.). *Firebase Firestore Documentation*. Firebase.  
- Firebase. (n.d.). *Firestore Introduction*. Google Cloud Platform.  

---

This article shows how to use Firestore to develop a web application that synchronizes data in real-time, without the maintenance and scalability challenges of an SQL database.
