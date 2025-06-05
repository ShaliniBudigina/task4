<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Task 4 Project - ApexPlanet</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Poppins', sans-serif;
      margin: 0;
      padding: 0;
      background: #e8f0fe;
      color: #222;
    }
    header, footer {
      background: #1e3a8a;
      color: white;
      padding: 1rem;
      text-align: center;
    }
    nav a {
      margin: 0 1rem;
      color: #e0e0e0;
      text-decoration: none;
    }
    section {
      padding: 2rem;
      background: #f9fafb;
      border-bottom: 1px solid #ddd;
    }
    #taskList li {
      list-style: none;
      background: #dbeafe;
      margin: 0.5rem 0;
      padding: 0.5rem;
      border-radius: 4px;
      cursor: pointer;
    }
    .product {
      border: 1px solid #ccc;
      background: #ffffff;
      margin: 1rem;
      padding: 1rem;
      width: 250px;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    .products {
      display: flex;
      flex-wrap: wrap;
      gap: 1rem;
    }
    .dark-mode {
      background: #1f2937;
      color: white;
    }
    .dark-mode section {
      background: #374151;
    }
    .dark-mode .product {
      background: #4b5563;
      color: white;
    }
    img {
      max-width: 100%;
      border-radius: 8px;
      margin-top: 1rem;
    }
  </style>
</head>
<body>
  <header>
    <h1>Shalini's Task 4 Project</h1>
    <nav>
      <a href="#portfolio">Portfolio</a>
      <a href="#todo">To-Do List</a>
      <a href="#products">Product Listing</a>
      <button onclick="toggleTheme()">Toggle Theme</button>
    </nav>
  </header>

  <!-- Portfolio Section -->
  <section id="portfolio">
    <h2>About Me</h2>
    <p>Hello! I’m Shalini. I enjoy building beautiful websites and web apps.</p>
    <img src="https://via.placeholder.com/600x300?text=My+Portfolio+Banner" alt="Portfolio banner">
    <h3>Projects</h3>
    <ul>
      <li>To-Do App with Local Storage</li>
      <li>Product Listing with Filter & Sort</li>
    </ul>
    <h3>Contact</h3>
    <p>Email: shalini@example.com</p>
  </section>

  <!-- To-Do List Section -->
  <section id="todo">
    <h2>To-Do List</h2>
    <input type="text" id="taskInput" placeholder="Enter task" />
    <button onclick="addTask()">Add Task</button>
    <ul id="taskList"></ul>
    <img src="https://via.placeholder.com/600x200?text=Stay+Organized+with+Tasks" alt="To-Do List Image">
  </section>

  <!-- Product Listing Section -->
  <section id="products">
    <h2>Product Listing</h2>
    <label>Filter by Category:</label>
    <select id="categoryFilter" onchange="renderProducts()">
      <option value="all">All</option>
      <option value="electronics">Electronics</option>
      <option value="books">Books</option>
    </select>

    <label>Sort by:</label>
    <select id="sortFilter" onchange="renderProducts()">
      <option value="price">Price</option>
      <option value="rating">Rating</option>
    </select>

    <div class="products" id="productList"></div>
    <img src="https://via.placeholder.com/600x200?text=Our+Top+Products" alt="Products Banner">
  </section>

  <footer>
    <p>&copy; 2025 Shalini | ApexPlanet Project</p>
  </footer>

  <script>
    // Theme toggle
    function toggleTheme() {
      document.body.classList.toggle("dark-mode");
    }

    // To-Do App
    const taskList = document.getElementById("taskList");
    const taskInput = document.getElementById("taskInput");

    function loadTasks() {
      const tasks = JSON.parse(localStorage.getItem("tasks")) || [];
      tasks.forEach(task => createTaskElement(task));
    }

    function addTask() {
      const task = taskInput.value;
      if (!task) return;
      createTaskElement(task);
      saveTask(task);
      taskInput.value = "";
    }

    function createTaskElement(task) {
      const li = document.createElement("li");
      li.textContent = task;
      li.onclick = () => {
        li.remove();
        deleteTask(task);
      };
      taskList.appendChild(li);
    }

    function saveTask(task) {
      const tasks = JSON.parse(localStorage.getItem("tasks")) || [];
      tasks.push(task);
      localStorage.setItem("tasks", JSON.stringify(tasks));
    }

    function deleteTask(task) {
      const tasks = JSON.parse(localStorage.getItem("tasks")) || [];
      const newTasks = tasks.filter(t => t !== task);
      localStorage.setItem("tasks", JSON.stringify(newTasks));
    }

    loadTasks();

    // Product Listing
    const products = [
      { name: "Laptop", category: "electronics", price: 800, rating: 4.5 },
      { name: "Book A", category: "books", price: 20, rating: 4.8 },
      { name: "Headphones", category: "electronics", price: 100, rating: 4.1 },
      { name: "Book B", category: "books", price: 15, rating: 4.2 }
    ];

    function renderProducts() {
      const category = document.getElementById("categoryFilter").value;
      const sort = document.getElementById("sortFilter").value;

      let filtered = category === "all" ? products : products.filter(p => p.category === category);

      if (sort === "price") filtered.sort((a, b) => a.price - b.price);
      else filtered.sort((a, b) => b.rating - a.rating);

      const list = document.getElementById("productList");
      list.innerHTML = "";
      filtered.forEach(p => {
        list.innerHTML += `<div class="product">
          <h3>${p.name}</h3>
          <p>Category: ${p.category}</p>
          <p>Price: $${p.price}</p>
          <p>Rating: ${p.rating}</p>
        </div>`;
      });
    }

    renderProducts();
  </script>
</body>
</html
