<html> <head> <title>D&D NPC Generator</title> <style> body { font-family: Arial, sans-serif; padding: 2rem; max-width: 600px; margin: auto; background: #f2f2f2; } select, button { margin: 0.5rem 0; padding: 0.5rem; } .npc-card { background: white; border-radius: 8px; padding: 1rem; margin-top: 1rem; box-shadow: 0 2px 5px rgba(0,0,0,0.1); } </style> </head> <body> <h1>D&D NPC Generator</h1>
<label for="race">Choose a race:</label>
<select id="race">
<option value="dwarf">Dwarf</option>
<option value="elf">Elf</option>
<option value="human">Human</option>
</select>

<br>
<label for="profession">Choose a profession:</label>
<select id="profession">
<option value="blacksmith">Blacksmith</option>
<option value="wizard">Wizard</option>
<option value="merchant">Merchant</option>
<option value="thief">Thief</option>
<option value="bard">Bard</option>
<option value="cleric">Cleric</option>
<option value="ranger">Ranger</option>
</select>

<br>
<button onclick="generateNPC()">Generate NPC</button>

<div id="npcResult" class="npc-card" style="display:none;"></div> <script> const nameLists = { dwarf: ['Thorin', 'Gimli', 'Dain', 'Balin', 'Dis', 'Oin', 'Gloin'], elf: ['Legolas', 'Elrond', 'Tauriel', 'Galadriel', 'Thranduil', 'Arwen'], human: ['Eddard', 'Arya', 'Jon', 'Brienne', 'Gendry', 'Catelyn'] }; const personalities = [ 'brave', 'cunning', 'greedy', 'kind', 'mysterious', 'noble', 'reckless', 'sarcastic', 'wise' ]; const quirks = [ 'hums constantly', 'has a pet mouse', 'speaks in rhymes', 'collects shiny stones', 'obsessed with soup', 'always wears a hat', 'afraid of ducks' ]; function randomFromArray(arr) { return arr[Math.floor(Math.random() * arr.length)]; } function generateNPC() { const race = document.getElementById('race').value; const profession = document.getElementById('profession').value; const names = nameLists[race] || []; if (names.length === 0) { alert("No names available for selected race."); return; } const name = randomFromArray(names); const age = race === 'elf' ? Math.floor(Math.random() * 282) + 18 : Math.floor(Math.random() * 82) + 18; const personality = randomFromArray(personalities); const quirk = randomFromArray(quirks); const npcHTML = ` <h2>${name}</h2> <p><strong>Race:</strong> ${race.charAt(0).toUpperCase() + race.slice(1)}</p> <p><strong>Profession:</strong> ${profession.charAt(0).toUpperCase() + profession.slice(1)}</p> <p><strong>Age:</strong> ${age}</p> <p><strong>Personality:</strong> ${personality}</p> <p><strong>Quirk:</strong> ${quirk}</p> `; const npcDiv = document.getElementById('npcResult'); npcDiv.innerHTML = npcHTML; npcDiv.style.display = 'block'; } </script> </body> </html>
