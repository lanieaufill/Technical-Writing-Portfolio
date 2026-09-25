---
layout: home
title: Poke API v2 Reference Sheet - An Open Access API
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
  <style>

layout: home
title: Poke API v2 Reference Sheet - An Open Access API
---

<style>
  body { background-color: #C1E1C1 !important; }
  .container-lg, .wrapper, main, .page-content {
    background-color: #ffffff !important;
    padding: 40px !important;
    border-radius: 12px !important;
    box-shadow: 0px 4px 20px rgba(0, 0, 0, 0.05) !important;
    margin-top: 30px !important;
    margin-bottom: 30px !important;
  }
</style>

# Poke API v2 Reference Sheet: An Open Access API

This reference guide provides developers with the structural parameters, data schemas, and URL path conventions needed to successfully query the global PokéAPI v2 database.

## Request Architecture

* **HTTP Method:** `GET`
* **Base URL:** `https://pokeapi.co`
* **Authentication Requirements:** None (Public Open Access)

### Request Parameters

#### Path Parameters
Path parameters are append-only directories attached directly to the base origin URL to drill down into resource nodes.

* **`api/v2/pokemon/{name_or_id}/`** *(string/integer)*: Pulls structural creature profiles. Strings must be lowercase (e.g., `ditto`). Integers reference the index key (e.g., `132`).
* **`api/v2/type/{name_or_id}/`** *(string/integer)*: Exposes elemental matrix balancing nodes (e.g., `fire` or `3`).
* **`api/v2/ability/{name_or_id}/`** *(string/integer)*: Isolates passive combat rule modifiers (e.g., `static` or `9`).

#### Query Parameters
Query parameters allow client applications to control pagination for collection requests. Appended after a `?` delimiter shortcut.

* **`limit`** *(integer)*: Dictates the maximum number of record summaries returned per transaction window. Default value is `20`.
* **`offset`** *(integer)*: Specifies the index position at which the returned record set begins. Default value is `0`.

#### Header Parameters
* **`Accept`**: `application/json`

#### Request Body Payload
* **`None`**: The `GET` method reads target resource records directly from the cloud schema. Unbound body payloads are dropped.

---

## Schema Constraints

Successful endpoint executions return complete structural JSON object maps.

###  Pokémon Node Schema (`api/v2/pokemon/`)
* **`id`** *(integer, Non-Nullable)*: The official unique national database index key.
* **`name`** *(string, Non-Nullable)*: The canonical lowercase lookup name of the creature.
* **`height`** *(integer, Non-Nullable)*: Entity tracking height calculated in decimeters.
* **`weight`** *(integer, Non-Nullable)*: Entity tracking mass calculated in hectograms.
* **`sprites.front_default`** *(string, Nullable)*: Absolute web destination path routing link to the default sprite sheet graphic.
* **`abilities`** *(array, Non-Nullable)*: Map array tracing trait properties, system slot settings, and hidden tags.

###  Type Node Schema (`api/v2/type/`)
* **`id`** *(integer)*: Database identifier for the specified element node.
* **`name`** *(string)*: The unique lookup name tracking the element classification (e.g., `water`).
* **`damage_relations`** *(object)*: Sub-arrays mapping systemic tracking lists like `double_damage_to` and `half_damage_to`.
* **`pokemon`** *(array)*: Comprehensive lookup list matching every animal profile assigned to this type node.

###  Ability Node Schema (`api/v2/ability/`)
* **`id`** *(integer)*: System transaction index for the target capability constraint.
* **`name`** *(string)*: Structural lowercase label string for the passive trigger (e.g., `imposter`).
* **`effect_entries`** *(array)*: Localization array containing string blocks detailing exact rule calculations.

## HTTP Status Codes & Network Error 

The network interface maps error logs to standard HTTP status codes. Review this matrix when validating payload states:

* **`200 OK`** *(Success)*: The target path matches a valid resource, and the server returns the requested resource data.
* **`404 Not Found`** *(Client Error)*: The requested path resource cannot be located. This occurs when an endpoint name or database ID does not correspond to an available resource.
* **`Network Failure`**: The browser or client fails to establish or maintain the outbound connection before receiving an HTTP response. This may result from local nework conditions, browser extensions, privacy settings, or an invalid destination conficuration.

## Example Payload Manifests

###  Success Payload (HTTP 200 OK)
When a valid path string (e.g., `api/v2/pokemon/ditto`) is successfully resolved, the server returns the fully initialized resource node dictionary:

```json
{
  "id": 132,
  "name": "ditto",
  "height": 3,
  "weight": 40,
  "sprites": {
    "front_default": "https://githubusercontent.com"
  },
  "abilities": [
    {
      "ability": {
        "name": "limber",
        "url": "https://pokeapi.co"
      },
      "is_hidden": false,
      "slot": 1
    }
  ]
}
```

###  Error Payload (HTTP 404 Not Found)
When a client application submits a path parameter that fails formatting validation rules or does not match a database record, the catch block outputs a structured validation error signature:

```json
{
  "error": true,
  "message": "HTTP Network Error Status: 404 Not Found",
  "context": "Verify spelling routes match the official PokéAPI syntax parameters."
}
```

###  Type Node Schema (`api/v2/type/`)

Successful executions targeting element nodes return deep structural relationship matrices mapping elemental data.

#### Success Payload (HTTP 200 OK Example)
```json
{
  "id": 3,
  "name": "flying",
  "damage_relations": {
    "double_damage_from": [
      { "name": "rock", "url": "https://pokeapi.co" },
      { "name": "electric", "url": "https://pokeapi.co" }
    ],
    "double_damage_to": [
      { "name": "fighting", "url": "https://pokeapi.co" },
      { "name": "bug", "url": "https://pokeapi.co" }
    ]
  },
  "pokemon": [
    {
      "pokemon": { "name": "charizard", "url": "https://pokeapi.co" },
      "slot": 2
    }
  ]
}
```

#### Error Payload (HTTP 404 Not Found Example)
```json
{
  "error": true,
  "message": "HTTP Network Error Status: 404 Not Found",
  "context": "Verify spelling routes match the official PokéAPI syntax parameters."
}
```

---

###  Ability Node Schema (`api/v2/ability/`)

Isolating a specific combat trait mapping reveals translation strings and historical rule descriptions.

#### Success Payload (HTTP 200 OK Example)
```json
{
  "id": 150,
  "name": "imposter",
  "effect_entries": [
    {
      "effect": "Transforms upon entering battle.",
      "language": { "name": "en", "url": "https://pokeapi.co" }
    }
  ],
  "pokemon": [
    {
      "is_hidden": true,
      "pokemon": { "name": "ditto", "url": "https://pokeapi.co" },
      "slot": 3
    }
  ]
}
```

#### Error Payload (HTTP 404 Not Found Example)
```json
{
  "error": true,
  "message": "HTTP Network Error Status: 404 Not Found",
  "context": "Verify spelling routes match the official PokéAPI syntax parameters."
}
```




<div class="api-explorer-root">
  <div class="api-explorer-header">
    <h3>PokéAPI Live Endpoint Inspector</h3>
    <p>Construct and execute live HTTP GET queries across the global REST dataset.</p>
  </div>

  <div class="api-control-matrix">
    <span class="api-url-base">https://pokeapi.co/api/v2/</span>
    <input type="text" id="api-query-parameter" placeholder="e.g., pokemon/ditto, type/3, ability/1">
    <button id="api-execute-btn" onclick="runLiveApiQuery()">Send Request</button>
  </div>

  <div class="api-telemetry-bar">
    <div class="telemetry-item">Request URL: <span id="telemetry-url">None</span></div>
    <div class="telemetry-item">HTTP Status: <span id="telemetry-status">---</span></div>
  </div>

  <div class="api-view-tabs" id="api-view-tabs-container" style="display: none;">
    <button class="tab-btn active" id="tab-pretty" onclick="switchConsoleView('pretty')">Pretty Text</button>
    <button class="tab-btn" id="tab-raw" onclick="switchConsoleView('raw')">Raw JSON</button>
  </div>

  <div class="api-response-wrapper">
    <div id="console-pretty-view" class="console-pane active-pane">
      <div class="placeholder-msg">Enter an endpoint route path above to execute a live query request...</div>
    </div>
    
    <div id="console-raw-view" class="console-pane" style="display: none;">
      <pre><code id="api-raw-json-output"></code></pre>
    </div>
  </div>
</div>

<script>
let globalResponsePayload = null;

document.getElementById('api-query-parameter')?.addEventListener('keypress', function(e) {
  if (e.key === 'Enter') {
    runLiveApiQuery();
  }
});

function switchConsoleView(viewType) {
  const prettyPane = document.getElementById('console-pretty-view');
  const rawPane = document.getElementById('console-raw-view');
  const prettyTab = document.getElementById('tab-pretty');
  const rawTab = document.getElementById('tab-raw');

  if (viewType === 'pretty') {
    prettyPane.style.display = 'block';
    rawPane.style.display = 'none';
    prettyTab.classList.add('active');
    rawTab.classList.remove('active');
  } else {
    prettyPane.style.display = 'none';
    rawPane.style.display = 'block';
    prettyTab.classList.remove('active');
    rawTab.classList.add('active');
  }
}

async function runLiveApiQuery() {
  const queryParamInput = document.getElementById('api-query-parameter');
  const jsonOutputBlock = document.getElementById('api-raw-json-output');
  const prettyViewBlock = document.getElementById('console-pretty-view');
  const telemetryUrl = document.getElementById('telemetry-url');
  const telemetryStatus = document.getElementById('telemetry-status');
  const tabsContainer = document.getElementById('api-view-tabs-container');

  if (!queryParamInput || !jsonOutputBlock || !prettyViewBlock) return;

  let pathString = queryParamInput.value.toLowerCase().trim();

  if (!pathString) {
    prettyViewBlock.innerHTML = '<div class="api-error-text">Error: Input path string cannot be blank.</div>';
    tabsContainer.style.display = 'none';
    return;
  }

  if (pathString.startsWith('/')) {
    pathString = pathString.substring(1);
  }

  const targetUri = "https://pokeapi.co/api/v2/" + pathString;
  telemetryUrl.textContent = targetUri;
  telemetryStatus.textContent = "PENDING...";
  telemetryStatus.style.color = "#cca700";
  
  tabsContainer.style.display = 'none';
  prettyViewBlock.innerHTML = '<div class="placeholder-msg">Streaming data maps from destination host...</div>';
  jsonOutputBlock.textContent = "";

  try {
    const apiResponse = await fetch(targetUri);
    telemetryStatus.textContent = apiResponse.status + " " + apiResponse.statusText;

    if (!apiResponse.ok) {
      telemetryStatus.style.color = "#ff4444";
      throw new Error("HTTP Network Error Status: " + apiResponse.status + " " + apiResponse.statusText);
    }

    telemetryStatus.style.color = "#28a745";
    globalResponsePayload = await apiResponse.json();
    tabsContainer.style.display = 'flex';
    switchConsoleView('pretty');

    jsonOutputBlock.textContent = JSON.stringify(globalResponsePayload, null, 2);
    
    renderPrettyView(pathString, globalResponsePayload, prettyViewBlock);

  } catch (caughtError) {
    telemetryStatus.textContent = "FAILED";
    telemetryStatus.style.color = "#ff4444";
    tabsContainer.style.display = 'none';
    prettyViewBlock.innerHTML = '<div class="api-error-text"><strong>API Network Call Failed</strong><br>' + caughtError.message + '</div>';
  }
}

function renderPrettyView(path, data, container) {
  if (path.includes('pokemon/')) {
    let typesList = data.types.map(t => '<span class="type-badge ' + t.type.name + '">' + t.type.name + '</span>').join(' ');
    let statsList = data.stats.map(s => '<li><strong>' + s.stat.name + ':</strong> ' + s.base_stat + '</li>').join('');
    
    container.innerHTML = `
      <div class="pretty-pokemon-card">
        <div class="card-hero">
          <img src="${data.sprites.front_default || ''}" alt="${data.name}">
          <h4>${data.name.toUpperCase()} (ID: #${data.id})</h4>
          <div class="type-container">${typesList}</div>
        </div>
        <div class="card-details">
          <h5>Core Physical Attributes</h5>
          <p><strong>Height:</strong> ${data.height / 10} m &nbsp;|&nbsp; <strong>Weight:</strong> ${data.weight / 10} kg</p>
          <h5>Base Statistics Map</h5>
          <ul>${statsList}</ul>
        </div>
      </div>
    `;
  } else if (path.includes('type/')) {
    let pokemonList = data.pokemon.slice(0, 10).map(p => '<li>' + p.pokemon.name + '</li>').join('');
    container.innerHTML = `
      <div class="pretty-generic-card">
        <h4>Type Resource: ${data.name.toUpperCase()}</h4>
        <h5>Damage Relations Context</h5>
        <p><strong>Double Damage To:</strong> ${data.damage_relations.double_damage_to.map(d => d.name).join(', ') || 'None'}</p>
        <p><strong>Half Damage To:</strong> ${data.damage_relations.half_damage_to.map(d => d.name).join(', ') || 'None'}</p>
        <h5>Sample Pokémon (${data.pokemon.length} Total)</h5>
        <ul>${pokemonList}</ul>
      </div>
    `;
  } else if (path.includes('ability/')) {
    let effectEntry = data.effect_entries.find(e => e.language.name === 'en')?.effect || 'No English description provided.';
    let usersList = data.pokemon.slice(0, 8).map(p => '<li>' + p.pokemon.name + '</li>').join('');
    container.innerHTML = `
      <div class="pretty-generic-card">
        <h4>Ability Resource: ${data.name.toUpperCase()}</h4>
        <h5>System Rule Effect</h5>
        <p class="effect-text">${effectEntry}</p>
        <h5>Common Resource Users</h5>
        <ul>${usersList}</ul>
      </div>
    `;
  } else {
    let mainKeys = Object.keys(data).slice(0, 6).map(k => '<li><strong>' + k + ':</strong> ' + (typeof data[k] === 'object' ? '[Object/Array]' : data[k]) + '</li>').join('');
    container.innerHTML = `
      <div class="pretty-generic-card">
        <h4>Endpoint Node: ${path.replace(/\/$/, '')}</h4>
        <p>Generic layout generated for unknown path structures.</p>
        <h5>Top-Level Schema Sample</h5>
        <ul>${mainKeys}</ul>
        <p class="tab-hint">💡 Switch to the <strong>Raw JSON</strong> tab above to audit the complete data arrays for this specific endpoint response.</p>
      </div>
    `;
  }
}
</script>

<style>
.api-explorer-root {
  margin: 24px auto;
  padding: 20px;
  background: #f6f8fa;
  border: 1px solid #d1d5da;
  border-radius: 6px;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif;
  color: #24292e;
}
.api-explorer-header h3 {
  margin: 0 0 4px 0;
  font-size: 18px;
  color: #0366d6;
}
.api-explorer-header p {
  margin: 0 0 16px 0;
  font-size: 13px;
  color: #586069;
}
.api-control-matrix {
  display: flex;
  align-items: center;
  gap: 4px;
  background: #ffffff;
  padding: 8px;
  border: 1px solid #e1e4e8;
  border-radius: 6px;
}
.api-url-base {
  font-family: monospace;
  font-size: 14px;
  color: #586069;
  user-select: none;
  background-color: #f1f1f1;
  padding: 6px 8px;
  border-radius: 4px;
  border: 1px solid #d1d5da;
}
#api-query-parameter {
  flex-grow: 1;
  padding: 6px 12px;
  font-size: 14px;
  font-family: monospace;
  border: 1px solid #d1d5da;
  border-radius: 4px;
  outline: none;
}
#api-query-parameter:focus {
  border-color: #0366d6;
}
#api-execute-btn {
  padding: 6px 16px;
  font-size: 14px;
  font-weight: 600;
  color: #ffffff;
  background-color: #0366d6;
  border: 1px solid rgba(27,31,35,0.15);
  border-radius: 4px;
  cursor: pointer;
  white-space: nowrap;
}
#api-execute-btn:hover {
  background-color: #0255b3;
}
.api-telemetry-bar {
  margin-top: 12px;
  padding: 8px 12px;
  background: #e1e4e8;
  border-radius: 4px;
  display: flex;
  justify-content: space-between;
  font-size: 12px;
  font-family: monospace;
  color: #444d56;
}
.telemetry-item span {
  font-weight: bold;
  color: #24292e;
}
.api-view-tabs {
  display: flex;
  margin-top: 16px;
  gap: 4px;
  border-bottom: 2px solid #e1e4e8;
}
.tab-btn {
  padding: 6px 16px;
  font-size: 13px;
  font-weight: 500;
  background: #e1e4e8;
  border: 1px solid #d1d5da;
  border-bottom: none;
  border-radius: 6px 6px 0 0;
  cursor: pointer;
  color: #586069;
}
.tab-btn.active {
  background: #ffffff;
  border-color: #d1d5da;
  color: #24292e;
  font-weight: 600;
  position: relative;
  top: 2px;
}
.api-response-wrapper {
  margin-top: -1px;
  border: 1px solid #d1d5da;
  border-radius: 0 0 6px 6px;
  background: #ffffff;
  min-height: 200px;
}
.console-pane {
  padding: 16px;
}
.placeholder-msg {
  color: #888888;
  font-size: 14px;
}
.api-error-text {
  color: #ff4444;
  font-size: 14px;
}
#console-raw-view pre {
  margin: 0;
  padding: 0;
  background: transparent;
  max-height: 500px;
  overflow-y: auto;
}
#console-raw-view code {
  font-family: "SFMono-Regular", Consolas, "Liberation Mono", Menlo, monospace;
  font-size: 12px;
  line-height: 1.5;
  white-space: pre-wrap;
  word-break: break-all;display: block;color: #24292e;}
  .pretty-pokemon-card, .pretty-generic-card {font-size: 14px;}
  .pretty-pokemon-card h4, .pretty-generic-card h4 {margin: 0 0 10px 0;color: #0366d6;font-size: 16px;}
  .card-hero {text-align: center;border-bottom: 1px dashed #e1e4e8;padding-bottom: 12px;margin-bottom: 12px;}
  .card-hero img {width: 96px;height: 96px;background: #f6f8fa;border-radius: 50%;border: 1px solid #e1e4e8;}
  .type-container {margin-top: 6px;}
  .type-badge {display: inline-block;padding: 2px 8px;font-size: 11px;font-weight: 600;color: #ffffff;border-radius: 4px;text-transform: uppercase;background: #68a090;}
  .type-badge.fire { background: #f08030; }
  .type-badge.water { background: #6890f0; }
  .type-badge.grass { background: #78c850; }
  .type-badge.electric { background: #f8d030; }
  .type-badge.psychic { background: #f85888; }
  .type-badge.ice { background: #98d8d8; }
  .type-badge.dragon { background: #7038f8; }
  .type-badge.dark { background: #705848; }
  .type-badge.fairy { background: #ee99ac; }
  .pretty-pokemon-card h5, .pretty-generic-card h5 {margin: 12px 0 6px 0;font-size: 13px;color: #586069;border-bottom: 1px solid #f6f8fa;}
  .pretty-pokemon-card ul, .pretty-generic-card ul {margin: 0;padding-left: 20px;}
  .effect-text {background: #f6f8fa;padding: 10px;border-left: 3px solid #0366d6;font-style: italic;}
  .tab-hint {margin-top: 16px;font-size: 12px;color: #586069;background: #f1f8ff;padding: 8px;border-radius: 4px;}

## API Reference Sheet from Open Access PokeAPI
