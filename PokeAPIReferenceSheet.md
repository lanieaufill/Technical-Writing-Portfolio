---
layout: home
title: api reference sheet from open access pokeapi
---

<style>
  body {
    background-color: #C1E1C1 !important; 
  }
  .container-lg, .wrapper, main, .page-content {
    background-color: #ffffff !important;
    padding: 40px !important;
    border-radius: 12px !important;
    box-shadow: 0px 4px 20px rgba(0, 0, 0, 0.05) !important;
    margin-top: 30px !important;
    margin-bottom: 30px !important;
  }
</style>

# Pokémon Data Fetcher

<div class="poke-container">
  <input type="text" id="poke-input" placeholder="e.g., pikachu, charizard">
  <button id="poke-btn">Fetch Pokémon</button>
  <div id="poke-result"></div>
</div>

<script>
document.getElementById('poke-btn').addEventListener('click', function() {
  const pokeName = document.getElementById('poke-input').value.toLowerCase().trim();
  const resultDiv = document.getElementById('poke-result');
  
  if (!pokeName) {
    resultDiv.innerHTML = '<p style="color: red;">Please enter a name!</p>';
    return;
  }

  resultDiv.innerHTML = '<p>Searching...</p>';

  fetch(`https://pokeapi.co{pokeName}`)
    .then(response => {
      if (!response.ok) {
        throw new Error('Pokémon not found');
      }
      return response.json();
    })
    .then(data => {
      resultDiv.innerHTML = `
        <div class="poke-card">
          <h3>${data.name.toUpperCase()}</h3>
          <img src="${data.sprites.front_default}" alt="${data.name}">
          <p><strong>Type:</strong> ${data.types.map(t => t.type.name).join(', ')}</p>
          <p><strong>Height:</strong> ${data.height / 10} m</p>
          <p><strong>Weight:</strong> ${data.weight / 10} kg</p>
        </div>
      `;
    })
    .catch(error => {
      resultDiv.innerHTML = `<p style="color: red;">Error: ${error.message}</p>`;
    });
});
</script>

<style>
.poke-container {
  margin: 20px 0;
  font-family: Arial, sans-serif;
}
#poke-input {
  padding: 10px;
  font-size: 16px;
  border: 2px solid #ccc;
  border-radius: 4px;
  width: 200px;
}
#poke-btn {
  padding: 10px 15px;
  font-size: 16px;
  background-color: #ef5350;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
}
#poke-btn:hover {
  background-color: #e53935;
}
.poke-card {
  margin-top: 20px;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
  max-width: 250px;
  text-align: center;
  background-color: #f9f9f9;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
}
.poke-card h3 {
  margin: 10px 0;
  color: #333;
}
.poke-card img {
  width: 120px;
  height: 120px;
}
</style>


## API Reference Sheet from Open Access PokeAPI
