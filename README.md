<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To-Do List Manager</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body, html {
            height: 100%;
            font-family: 'Arial', sans-serif;
            overflow: hidden;
        }

        .video-background {
            position: fixed; /* Ensure it stays in the background */
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0; /* Set behind other elements */
            overflow: hidden;
            opacity: 1; /* Full opacity to see the video */
        }

        .video-background video {
            width: 100%; /* Cover full width */
            height: 100%; /* Cover full height */
            object-fit: cover; /* Maintain aspect ratio */
            opacity: 50%;
        }

        .navbar {
            position: sticky;
            top: 0;
            background-color: rgba(0, 123, 255, 0.8);
            padding: 15px;
            text-align: center;
            z-index: 10;
        }

        .navbar a {
            color: white;
            margin: 0 15px;
            text-decoration: none;
            font-weight: bold;
            position: relative;
            transition: color 0.3s, transform 0.3s;
        }

        .navbar a:hover {
            color: #ffd700;
            transform: scale(1.1);
        }

        .tooltip {
            display: none;
            position: absolute;
            background: rgba(255, 255, 255, 0.9);
            border: 1px solid #ddd;
            border-radius: 5px;
            padding: 10px;
            color: #333;
            z-index: 20;
            white-space: nowrap;
            top: 100%;
            left: 50%;
            transform: translateX(-50%);
            width: 200px;
            text-align: center;
            opacity: 0;
            transition: opacity 0.3s ease;
        }

        .navbar a:hover + .tooltip {
            display: block;
            opacity: 1;
        }

        .container {
            display: flex;
            background: rgba(255, 255, 255, 0.8);
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            width: 800px;
            margin: 50px auto;
            position: relative;
            z-index: 1; /* Ensure it is above the video */
            animation: fadeIn 1.5s ease-out;
            min-height: 400px; /* Set a minimum height */
        }

        h1 {
            text-align: center;
            color: #333;
            margin-bottom: 20px;
        }

        #taskInput, #taskTime {
            width: calc(100% - 20px);
            padding: 10px;
            margin-bottom: 10px;
            border: 2px solid #007bff;
            border-radius: 5px;
        }

        .add-btn {
            width: 100%;
            padding: 10px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s, transform 0.3s;
        }

        .add-btn:hover {
            background-color: #0056b3;
            transform: scale(1.05);
        }

        ul {
            list-style: none;
            margin-top: 20px;
        }

        li {
            background-color: #f9f9f9;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
            margin-bottom: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            opacity: 0;
            transform: translateY(20px);
            animation: slideIn 0.5s forwards;
            flex-direction: column;
        }

        .delete-btn {
            background-color: red;
            color: white;
            border: none;
            padding: 5px;
            border-radius: 5px;
            cursor: pointer;
        }

        .due-time {
            color: #007bff;
            font-size: 14px;
        }

        .task-summary-container {
            background: rgba(255, 255, 255, 0.8);
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            width: 300px;
        }

        table {
            border-collapse: collapse;
            width: 100%;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            background: white;
        }

        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
        }

        th {
            background-color: #007bff;
            color: white;
        }

        .motivation {
            margin-top: 20px;
            font-size: 16px;
            color: green;
            text-align: center;
            opacity: 0;
            transition: opacity 0.5s ease;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: scale(0.9);
            }
            to {
                opacity: 1;
                transform: scale(1);
            }
        }

        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        footer {
            text-align: center;
            padding: 20px;
            background-color: rgba(0, 123, 255, 0.8);
            color: white;
            position: absolute;
            bottom: 0;
            width: 100%;
            left: 0;
        }
    </style>
</head>
<body>
    <div class="video-background">
        <video autoplay loop muted>
            <source src="Underwater Effect with Particles Free Background Videos, No Copyright .mp4" type="video/mp4">
            Your browser does not support the video tag.
        </video>
    </div>

    <div class="navbar">
        <a href="#about" onclick="scrollToSection('about')">About Us</a>
        <div class="tooltip">Learn more about us!</div>
        <a href="#contact" onclick="scrollToSection('contact')">Contact</a>
        <div class="tooltip">Get in touch!</div>
        <a href="#tutorial" onclick="scrollToSection('tutorial')">Tutorial</a>
        <div class="tooltip">See how it works!</div>
    </div>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
    <div class="container">
        <div class="todo-list">
            <h1>TO-DO LIST</h1>
            <input type="text" id="taskInput" placeholder="Add a new task...">
            <input type="datetime-local" id="taskTime" placeholder="Set due time">
            <button class="add-btn" onclick="addTask()">Add Task</button>
            <ul id="taskList"></ul>
            <div id="motivation" class="motivation"></div>
        </div>

        <div class="task-summary-container" id="about">
            <h2>All Tasks</h2>
            <table>
                <thead>
                    <tr>
                        <th>Task</th>
                        <th>Due Time</th>
                    </tr>
                </thead>
                <tbody id="taskSummary">
                    <!-- Tasks will be listed here -->
                </tbody>
            </table>
        </div>
    </div>

    <footer>
        &copy; 2024 Group 6
    </footer>

    <script>
        let tasks = [];
        let motivationalMessages = [
            "Great job! Keep going!",
            "You're unstoppable!",
            "One step closer to your goal!",
            "Amazing progress!",
            "Keep shining!"
        ];

        function addTask() {
            const taskInput = document.getElementById('taskInput');
            const taskTime = document.getElementById('taskTime');
            const taskValue = taskInput.value.trim();
            const taskDueTime = taskTime.value;

            if (taskValue) {
                const task = {
                    name: taskValue,
                    dueTime: taskDueTime,
                };

                tasks.push(task);
                taskInput.value = '';
                taskTime.value = '';
                updateTaskList();
                updateTaskSummary();
                showMotivation();
            }
        }

        function updateTaskList() {
            const taskList = document.getElementById('taskList');
            taskList.innerHTML = '';

            tasks.forEach((task, index) => {
                const li = document.createElement('li');
                li.innerHTML = `
                    ${task.name} <span class="due-time">${task.dueTime}</span>
                    <button class="delete-btn" onclick="deleteTask(${index})">Delete</button>
                `;
                taskList.appendChild(li);
            });
        }

        function updateTaskSummary() {
            const taskSummary = document.getElementById('taskSummary');
            taskSummary.innerHTML = '';

            tasks.forEach(task => {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${task.name}</td>
                    <td>${task.dueTime}</td>
                `;
                taskSummary.appendChild(row);
            });
        }

        function deleteTask(index) {
            tasks.splice(index, 1);
            updateTaskList();
            updateTaskSummary();
        }

        function showMotivation() {
            const motivationDiv = document.getElementById('motivation');
            const randomIndex = Math.floor(Math.random() * motivationalMessages.length);
            motivationDiv.innerText = motivationalMessages[randomIndex];
            motivationDiv.style.opacity = 1;

            setTimeout(() => {
                motivationDiv.style.opacity = 0;
            }, 3000);
        }

        function scrollToSection(sectionId) {
            const section = document.getElementById(sectionId);
            section.scrollIntoView({ behavior: 'smooth' });
        }
    </script>
</body>
</html>
