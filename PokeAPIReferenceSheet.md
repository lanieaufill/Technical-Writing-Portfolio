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

<!-- === THE INTERFACE (HTML) === -->
<div class="poke-container">
  <input type="text" id="poke-input" placeholder="e.g., pikachu, charizard">
  <!-- Inline onclick ensures the button always connects to the function -->
  <button id="poke-btn" onclick="getPokemonData()">Fetch Pokémon</button>
  <div id="poke-result"></div>
</div>

<!-- === THE LOGIC (JAVASCRIPT) === -->
<script>
function getPokemonData() {
  const pokeInput = document.getElementById('poke-input');
  const resultDiv = document.getElementById('poke-result');
  
  if (!pokeInput || !resultDiv) {
    console.error("Missing elements!");
    return;
  }

  const pokeName = pokeInput.value.toLowerCase().trim();
  
  if (!pokeName) {
    resultDiv.innerHTML = '<p style="color: red; font-weight: bold;">Please enter a name!</p>';
    return;
  }

  resultDiv.innerHTML = '<p style="color: #666;">Searching the Pokédex...</p>';

  fetch(`https://pokeapi.co{pokeName}`)
    .then(response => {
      if (!response.ok) {
        throw new Error('Pokémon not found. Double check the spelling!');
      }
      return response.json();
    })
    .then(data => {
      resultDiv.innerHTML = `
        <div class="poke-card">
          <h3 style="text-transform: uppercase; margin: 10px 0; color: #333;">${data.name}</h3>
          <img src="${data.sprites.front_default}" alt="${data.name}" style="width: 120px; height: 120px;">
          <p><strong>Type:</strong> ${data.types.map(t => t.type.name).join(', ')}</p>
          <p><strong>Height:</strong> ${data.height / 10} m</p>
          <p><strong>Weight:</strong> ${data.weight / 10} kg</p>
        </div>
      `;
    })
    .catch(error => {
      resultDiv.innerHTML = `<p style="color: red; font-weight: bold;">Error: ${error.message}</p>`;
    });
}
</script>



## API Reference Sheet from Open Access PokeAPI
