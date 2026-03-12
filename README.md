<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Recipe Vault</title>

<link rel="manifest" href="manifest.json">

<style>
body{
font-family:Arial;
background:#fff6f8;
padding:20px;
}

h1{
color:#c94f7c;
}

textarea{
width:100%;
height:120px;
margin-top:10px;
padding:10px;
border-radius:10px;
border:1px solid #ccc;
}

button{
margin-top:10px;
padding:12px;
width:100%;
background:#ff4f8b;
color:white;
border:none;
border-radius:10px;
font-size:16px;
}

.recipe{
background:white;
padding:15px;
border-radius:10px;
margin-top:10px;
box-shadow:0 2px 5px rgba(0,0,0,.1);
}
</style>
</head>

<body>

<h1>🍓 My Recipe Vault</h1>

<textarea id="recipeInput" placeholder="Paste a recipe here..."></textarea>

<button onclick="saveRecipe()">Save Recipe</button>

<h2>Saved Recipes</h2>

<div id="recipeList"></div>

<script>

function saveRecipe(){

let recipe=document.getElementById("recipeInput").value;

if(!recipe) return;

let recipes=JSON.parse(localStorage.getItem("recipes"))||[];

recipes.push(recipe);

localStorage.setItem("recipes",JSON.stringify(recipes));

document.getElementById("recipeInput").value="";

displayRecipes();

}

function displayRecipes(){

let recipes=JSON.parse(localStorage.getItem("recipes"))||[];

let list=document.getElementById("recipeList");

list.innerHTML="";

recipes.forEach(function(r){

let div=document.createElement("div");

div.className="recipe";

div.innerText=r;

list.appendChild(div);

});

}

displayRecipes();

if('serviceWorker' in navigator){
navigator.serviceWorker.register('sw.js');
}

</script>

</body>
</html>
