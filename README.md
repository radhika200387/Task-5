<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Full Web Project</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 0; padding: 0; background: #f2f2f2; color: #333; }
    nav ul { list-style: none; display: flex; background: #4CAF50; padding: 10px; margin: 0; }
    nav ul li { margin-right: 20px; }
    nav ul li a { color: white; text-decoration: none; font-weight: bold; }
    section { padding: 20px; }
    h2 { color: #4CAF50; }

    .project-card { background: #fff; padding: 10px; margin: 10px 0; border-radius: 8px; box-shadow: 0 0 8px rgba(0,0,0,0.1); }

    #taskInput { padding: 10px; width: 60%; }
    #taskList li { background: #fff; margin: 5px 0; padding: 10px; border-radius: 5px; }

    #productContainer div { background: #fff; padding: 10px; margin: 5px 0; border-radius: 5px; }

    @media (max-width: 768px) {
      nav ul { flex-direction: column; align-items: flex-start; }
    }
  </style>
</head>
<body>

  <!-- Navigation -->
  <nav>
    <ul>
      <li><a href="#about">About</a></li>
      <li><a href="#projects">Projects</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
  </nav>

  <!-- About Section -->
  <section id="about">
    <h2>About Me</h2>
    <p>I am a web developer passionate about building clean and responsive websites.</p>
  </section>

  <!-- Projects Section -->
  <section id="projects">
    <h2>Projects</h2>
    <div class="project-card">To-Do App with Local Storage</div>
    <div class="project-card">Product Listing Page</div>
  </section>

  <!-- Contact Section -->
  <section id="contact">
    <h2>Contact</h2>
    <p>Email: yourname@example.com</p>
  </section>

  <!-- To-Do App Section -->
  <section>
    <h2>📝 To-Do List</h2>
    <input type="text" id="taskInput" placeholder="Add a task">
    <button onclick="addTask()">Add</button>
    <ul id="taskList"></ul>
  </section>

  <!-- Product Listing Section -->
  <section>
    <h2>🛒 Product Listing</h2>
    <label>Category:
      <select id="categoryFilter" onchange="filterProducts()">
        <option value="all">All</option>
        <option value="electronics">Electronics</option>
        <option value="clothing">Clothing</option>
      </select>
    </label>
    <label>Sort By:
      <select id="sortBy" onchange="filterProducts()">
        <option value="price">Price</option>
        <option value="rating">Rating</option>
      </select>
    </label>
    <div id="productContainer"></div>
  </section>

  <!-- JavaScript -->
  <script>
    // To-Do App
    function loadTasks() {
      const tasks = JSON.parse(localStorage.getItem("tasks")) || [];
      const list = document.getElementById("taskList");
      list.innerHTML = '';
      tasks.forEach(task => {
        const li = document.createElement("li");
        li.textContent = task;
        list.appendChild(li);
      });
    }

    function addTask() {
      const input = document.getElementById("taskInput");
      const tasks = JSON.parse(localStorage.getItem("tasks")) || [];
      if (input.value.trim() !== "") {
        tasks.push(input.value.trim());
        localStorage.setItem("tasks", JSON.stringify(tasks));
        input.value = '';
        loadTasks();
      }
    }

    loadTasks();

    // Product Listing
    const products = [
      { name: "Phone", category: "electronics", price: 299, rating: 4.5 },
      { name: "Laptop", category: "electronics", price: 999, rating: 4.7 },
      { name: "Shirt", category: "clothing", price: 25, rating: 4.1 },
      { name: "Jeans", category: "clothing", price: 45, rating: 4.3 }
    ];

    function filterProducts() {
      const category = document.getElementById("categoryFilter").value;
      const sort = document.getElementById("sortBy").value;

      let filtered = category === "all" ? products : products.filter(p => p.category === category);
      filtered.sort((a, b) => a[sort] - b[sort]);

      const container = document.getElementById("productContainer");
      container.innerHTML = '';
      filtered.forEach(p => {
        const div = document.createElement("div");
        div.textContent = `${p.name} - $${p.price} - ⭐${p.rating}`;
        container.appendChild(div);
      });
    }

    filterProducts();
  </script>

</body>
</html>
