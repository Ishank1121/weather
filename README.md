Creating a responsive dynamic website called "Recipe Finder" requires a combination of front-end and back-end technologies. Below is a breakdown of how to implement it using HTML, CSS, JavaScript, AJAX, JSON, jQuery, and Node.js.

Tech Stack:

Front-end: HTML, CSS, JavaScript, jQuery, AJAX
Back-end: Node.js (Express.js)
Database: JSON file (or MongoDB for scalability)
API: Custom API serving dish names, recipes, images, and videos
Features:

✔ Search recipes dynamically using AJAX
✔ Fetch recipe details including ingredients, images, and videos
✔ Responsive UI with Navbar, Sidebar, and Footer
✔ Use of jQuery for smooth interactions
✔ Node.js + Express.js for API handling

Folder Structure:

recipe-finder/
│── public/
│   ├── css/style.css
│   ├── js/script.js
│   ├── images/
│── views/
│   ├── index.html
│── server/
│   ├── data/recipes.json
│   ├── server.js
│── package.json
│── README.md
Step 1: Setup Project

Initialize a Node.js project:

mkdir recipe-finder
cd recipe-finder
npm init -y
npm install express cors body-parser
Step 2: Create API in Node.js

Create a folder server and inside it, create a file server.js.

const express = require("express");
const cors = require("cors");
const app = express();
const PORT = 3000;

app.use(cors());
app.use(express.json());

// Sample Recipe Data (You can replace this with a database)
const recipes = [
  {
    id: 1,
    name: "Pasta Alfredo",
    image: "https://via.placeholder.com/200",
    video: "https://www.youtube.com/embed/VIDEO_ID",
    ingredients: ["Pasta", "Cream", "Garlic", "Cheese", "Butter"],
    instructions: "Boil pasta, cook with sauce, mix well, and serve hot.",
  },
  {
    id: 2,
    name: "Chicken Biryani",
    image: "https://via.placeholder.com/200",
    video: "https://www.youtube.com/embed/VIDEO_ID",
    ingredients: ["Rice", "Chicken", "Spices", "Onions", "Yogurt"],
    instructions: "Cook rice, add chicken and spices, mix well, and serve.",
  },
];

// API Endpoint
app.get("/api/recipes", (req, res) => {
  res.json(recipes);
});

// Search API
app.get("/api/recipes/search", (req, res) => {
  const query = req.query.name.toLowerCase();
  const result = recipes.filter((recipe) =>
    recipe.name.toLowerCase().includes(query)
  );
  res.json(result);
});

app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
Step 3: Create Frontend UI

Inside views/index.html:

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Recipe Finder</title>
    <link rel="stylesheet" href="/public/css/style.css">
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>
    <nav class="navbar">
        <h1>Recipe Finder</h1>
    </nav>
    
    <div class="container">
        <aside class="sidebar">
            <h2>Categories</h2>
            <ul>
                <li>Vegetarian</li>
                <li>Non-Vegetarian</li>
                <li>Desserts</li>
                <li>Snacks</li>
            </ul>
        </aside>

        <main>
            <input type="text" id="search" placeholder="Search for a recipe...">
            <div id="recipes"></div>
        </main>
    </div>

    <footer class="footer">
        <p>&copy; 2025 Recipe Finder</p>
    </footer>

    <script src="/public/js/script.js"></script>
</body>
</html>
Step 4: Add CSS Styles

Inside public/css/style.css:

body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f5f5f5;
}

.navbar {
    background-color: #333;
    color: white;
    padding: 15px;
    text-align: center;
}

.container {
    display: flex;
    padding: 20px;
}

.sidebar {
    width: 20%;
    background: #ddd;
    padding: 15px;
}

.sidebar ul {
    list-style-type: none;
    padding: 0;
}

main {
    width: 80%;
    padding: 20px;
}

input {
    width: 100%;
    padding: 10px;
    margin-bottom: 20px;
}

#recipes {
    display: flex;
    flex-wrap: wrap;
}

.recipe-card {
    background: white;
    padding: 15px;
    margin: 10px;
    border-radius: 8px;
    width: 200px;
    box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
    text-align: center;
}

.recipe-card img {
    width: 100%;
    height: auto;
}

.footer {
    background-color: #333;
    color: white;
    text-align: center;
    padding: 10px;
    position: fixed;
    bottom: 0;
    width: 100%;
}
Step 5: Fetch API Data Using AJAX & jQuery

Inside public/js/script.js:

$(document).ready(function () {
    $("#search").on("input", function () {
        let query = $(this).val();

        if (query.length > 1) {
            $.ajax({
                url: `/api/recipes/search?name=${query}`,
                method: "GET",
                success: function (data) {
                    displayRecipes(data);
                },
                error: function () {
                    $("#recipes").html("<p>No recipes found</p>");
                },
            });
        } else {
            $("#recipes").html("");
        }
    });

    function displayRecipes(recipes) {
        $("#recipes").html("");
        recipes.forEach((recipe) => {
            $("#recipes").append(`
                <div class="recipe-card">
                    <h3>${recipe.name}</h3>
                    <img src="${recipe.image}" alt="${recipe.name}">
                    <p><strong>Ingredients:</strong> ${recipe.ingredients.join(", ")}</p>
                    <p><strong>Instructions:</strong> ${recipe.instructions}</p>
                    <iframe width="200" height="150" src="${recipe.video}" frameborder="0" allowfullscreen></iframe>
                </div>
            `);
        });
    }
});
Step 6: Run the Application

Start the server:
node server/server.js
Open index.html in the browser.
Final Features:

✅ Live search for recipes using AJAX
✅ Displays recipe details with images and videos
✅ Sidebar for categories
✅ Responsive layout with navbar, sidebar, and footer
✅ Smooth interactions with jQuery

Would you like me to add database support (MongoDB) or deploy it on a cloud platform?
