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

<div class="api-explorer-root">
  <div class="api-explorer-header">
    <h3>PokéAPI Live Endpoint Inspector</h3>
    <p>Construct, execute, and evaluate live HTTP GET queries across the global REST dataset.</p>
  </div>
  <div class="api-control-matrix">
    <select id="api-endpoint-selector">
      <option value="pokemon">/pokemon</option>
      <option value="ability">/ability</option>
      <option value="type">/type</option>
      <option value="move">/move</option>
      <option value="berry">/berry</option>
      <option value="generation">/generation</option>
    </select>
    <span class="api-url-slash">/</span>
    <input type="text" id="api-query-parameter" placeholder="id or name (e.g., charizard, static, 1)">
    <button id="api-execute-btn" onclick="runLiveApiQuery()">Send Request</button>
  </div>
  <div class="api-telemetry-bar">
    <div class="telemetry-item">Request URL: <span id="telemetry-url">None</span></div>
    <div class="telemetry-item">HTTP Status: <span id="telemetry-status">---</span></div>
  </div>
  <div class="api-response-console">
    <div class="console-title-tab">RESPONSE JSON PAYLOAD</div>
    <pre><code id="api-raw-json-output">Execute a query above to stream raw API server response data maps...</code></pre>
  </div>
</div>

<script>
document.getElementById('api-query-parameter')?.addEventListener('keypress', function(e) {
  if (e.key === 'Enter') {
    runLiveApiQuery();
  }
});

async function runLiveApiQuery() {
  const endpointSelect = document.getElementById('api-endpoint-selector');
  const queryParamInput = document.getElementById('api-query-parameter');
  const jsonOutputBlock = document.getElementById('api-raw-json-output');
  const telemetryUrl = document.getElementById('telemetry-url');
  const telemetryStatus = document.getElementById('telemetry-status');

  if (!endpointSelect || !queryParamInput || !jsonOutputBlock) return;

  const endpoint = endpointSelect.value;
  const parameter = queryParamInput.value.toLowerCase().trim();

  if (!parameter) {
    jsonOutputBlock.textContent = "Error: Missing URI path parameter. Please specify a resource ID or string name.";
    jsonOutputBlock.style.color = "#ff4444";
    return;
  }

  const targetUri = "https://pokeapi.co" + endpoint + "/" + parameter + "/";
  telemetryUrl.textContent = targetUri;
  telemetryStatus.textContent = "PENDING...";
  telemetryStatus.style.color = "#cca700";

  jsonOutputBlock.textContent = "Streaming stream chunk data from remote origin server...";
  jsonOutputBlock.style.color = "#888888";

  try {
    const apiResponse = await fetch(targetUri, {
      method: 'GET',
      headers: { 'Accept': 'application/json' }
    });

    telemetryStatus.textContent = apiResponse.status + " " + apiResponse.statusText;

    if (!apiResponse.ok) {
      telemetryStatus.style.color = "#ff4444";
      throw new Error("HTTP Network Error Status: " + apiResponse.status + " " + apiResponse.statusText);
    }

    telemetryStatus.style.color = "#28a745";
    const completeJsonData = await apiResponse.json();
    jsonOutputBlock.textContent = JSON.stringify(completeJsonData, null, 2);
    jsonOutputBlock.style.color = "#24292e";

  } catch (caughtError) {
    jsonOutputBlock.textContent = "{\n  \"error\": true,\n  \"message\": \"" + caughtError.message + "\",\n  \"context\": \"Ensure spelling accuracy or API endpoint availability.\"\n}";
    jsonOutputBlock.style.color = "#ff4444";
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
  gap: 8px;
  background: #ffffff;
  padding: 8px;
  border: 1px solid #e1e4e8;
  border-radius: 6px;
}
#api-endpoint-selector {
  padding: 6px 10px;
  font-size: 14px;
  font-family: monospace;
  background-color: #f1f1f1;
  border: 1px solid #d1d5da;
  border-radius: 4px;
  cursor: pointer;
}
.api-url-slash {
  font-family: monospace;
  font-weight: bold;
  color: #586069;
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
.api-response-console {
  margin-top: 16px;
  border: 1px solid #d1d5da;
  border-radius: 6px;
  overflow: hidden;
}
.console-title-tab {
  background: #24292e;
  color: #ffffff;
  padding: 6px 12px;
  font-size: 11px;
  font-weight: bold;
  letter-spacing: 0.5px;
  font-family: monospace;
}
.api-response-console pre {
  margin: 0;
  padding: 16px;
  background: #ffffff;
  max-height: 400px;
  overflow-y: auto;
  border-top: none;
}
.api-response-console code {
  font-family: "SFMono-Regular", Consolas, "Liberation Mono", Menlo, monospace;
  font-size: 12px;
  line-height: 1.5;
  white-space: pre-wrap;
  word-break: break-all;
  display: block;
}
</style>

## API Reference Sheet from Open Access PokeAPI
