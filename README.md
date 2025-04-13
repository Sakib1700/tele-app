# tele-app
<!DOCTYPE html>
   <html>
   <head>
       <title>Telegram To-Do List</title>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <script src="https://telegram.org/js/telegram-web-app.js"></script>
       <style>
           body { font-family: Arial, sans-serif; padding: 10px; }
           #todo-input { width: 70%; padding: 8px; }
           #add-btn { padding: 8px 12px; background: #0088cc; color: white; border: none; }
           ul { list-style: none; padding: 0; }
           li { padding: 8px; border-bottom: 1px solid #eee; }
       </style>
   </head>
   <body>
       <h1>My To-Do List</h1>
       <div>
           <input type="text" id="todo-input" placeholder="Add a task...">
           <button id="add-btn">Add</button>
       </div>
       <ul id="todo-list"></ul>

       <script>
           const tg = window.Telegram.WebApp;
           tg.expand(); // Expand the app to full screen
           tg.MainButton.setText("Save").show();

           const todoList = document.getElementById('todo-list');
           const todoInput = document.getElementById('todo-input');
           const addBtn = document.getElementById('add-btn');

           // Load saved tasks (if any)
           let tasks = JSON.parse(localStorage.getItem('tasks')) || [];

           function renderTasks() {
               todoList.innerHTML = '';
               tasks.forEach((task, index) => {
                   const li = document.createElement('li');
                   li.textContent = task;
                   todoList.appendChild(li);
               });
           }

           addBtn.addEventListener('click', () => {
               if (todoInput.value.trim() !== '') {
                   tasks.push(todoInput.value);
                   localStorage.setItem('tasks', JSON.stringify(tasks));
                   todoInput.value = '';
                   renderTasks();
               }
           });

           renderTasks();
       </script>
   </body>
   </html>
   
