<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Task Management App</title>
<style>
body{
    font-family: Arial, sans-serif;
    background:#f4f4f4;
    margin:0;
    padding:20px;
}
.container{
    max-width:600px;
    margin:auto;
    background:white;
    padding:20px;
    border-radius:10px;
    box-shadow:0 0 10px rgba(0,0,0,0.1);
}
h1{
    text-align:center;
}
input{
    width:70%;
    padding:10px;
}
button{
    padding:10px 15px;
    background:#007bff;
    color:white;
    border:none;
    border-radius:5px;
    cursor:pointer;
}
ul{
    list-style:none;
    padding:0;
}
li{
    display:flex;
    justify-content:space-between;
    align-items:center;
    padding:10px;
    margin-top:10px;
    background:#eee;
    border-radius:5px;
}
.completed{
    text-decoration:line-through;
    color:gray;
}
</style>
</head>
<body>

<div class="container">
    <h1>Task Management App</h1>

    <input type="text" id="taskInput" placeholder="Enter Task">
    <button onclick="addTask()">Add</button>

    <ul id="taskList"></ul>
</div>

<script>
let tasks = JSON.parse(localStorage.getItem("tasks")) || [];

function saveTasks(){
    localStorage.setItem("tasks", JSON.stringify(tasks));
}

function displayTasks(){
    let taskList = document.getElementById("taskList");
    taskList.innerHTML = "";

    tasks.forEach((task,index)=>{
        let li = document.createElement("li");

        li.innerHTML = `
            <span class="${task.completed ? 'completed' : ''}"
             onclick="toggleTask(${index})">
             ${task.name}
            </span>
            <button onclick="deleteTask(${index})">Delete</button>
        `;

        taskList.appendChild(li);
    });
}

function addTask(){
    let input = document.getElementById("taskInput");

    if(input.value.trim() === "") return;

    tasks.push({
        name: input.value,
        completed:false
    });

    input.value="";
    saveTasks();
    displayTasks();
}

function toggleTask(index){
    tasks[index].completed = !tasks[index].completed;
    saveTasks();
    displayTasks();
}

function deleteTask(index){
    tasks.splice(index,1);
    saveTasks();
    displayTasks();
}

displayTasks();
</script>

</body>
</html>
