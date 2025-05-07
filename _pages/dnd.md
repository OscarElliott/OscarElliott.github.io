---
layout: page
permalink: /dnd/
title: NPC Generator
description: Generate NPC's for Emesia
nav: false
nav_order: 8
---

<style>
  :root {
    --bg: #1a1a1a;
    --card-bg: #2a2a2a;
    --text: #f4f4f4;
    --accent: #4caf50;
    --button-bg: #333;
    --button-hover: #555;
  }

  #npc-generator {
    font-family: Arial, sans-serif;
    padding: 2rem;
    max-width: 600px;
    margin: auto;
    background: var(--bg);
    border-radius: 12px;
    color: var(--text);
  }

  select, button {
    margin: 0.5rem 0;
    padding: 0.5rem;
    background: var(--button-bg);
    color: var(--text);
    border: 1px solid #444;
    border-radius: 6px;
  }

  button:hover {
    background: var(--button-hover);
    cursor: pointer;
  }

  .npc-card {
    background: var(--card-bg);
    border-radius: 8px;
    padding: 1rem;
    margin-top: 1rem;
    box-shadow: 0 2px 5px rgba(0,0,0,0.3);
    color: var(--text);
  }

  h1, h2 {
    color: var(--accent);
  }
</style>

<div id="npc-generator">
  <h1>D&D NPC Generator</h1>
  <label for="race">Choose a race:</label>
  <select id="race">
    <option value="dwarf">Dwarf</option>
    <option value="elf">Elf</option>
    <option value="human">Human</option>
    <option value="halfElf">Half-Elf</option>
    <option value="hobbit">Hobbit</option>
    <option value="goblin">Goblin</option>
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
    <option value="random">Random</option>
  </select>

  <br>
  <button onclick="generateNPC()">Generate NPC</button>

  <div id="npcResult" class="npc-card" style="display:none;"></div>
</div>

<script>
  const nameLists = {};
  const lastNameLists = {};
  const personalities = [
    'brave', 'cunning', 'greedy', 'kind', 'mysterious', 'noble', 'reckless', 'sarcastic', 'wise'
  ];
  const quirks = [
    'hums constantly', 'has a pet mouse', 'speaks in rhymes', 'collects shiny stones',
    'obsessed with soup', 'always wears a hat', 'afraid of ducks'
  ];

  function randomFromArray(arr) {
    return arr[Math.floor(Math.random() * arr.length)];
  }

  async function loadNames(race) {
    if (!nameLists[race]) {
      try {
        const response = await fetch(`/assets/dndGenLists/names/${race}.txt`);
        if (!response.ok) throw new Error('Failed to fetch names');
        const text = await response.text();
        nameLists[race] = text.split('\n').map(name => name.trim()).filter(name => name.length > 0);
      } catch (err) {
        console.error(err);
        alert(`Could not load names for ${race}`);
        nameLists[race] = ['Nameless'];
      }
    }
  }

  async function generateNPC() {
    const race = document.getElementById('race').value;
    const profession = document.getElementById('profession').value;

    await loadNames(race);
    const names = nameLists[race];
    const name = randomFromArray(names);

    let age;
    switch (race) {
      case 'elf': age = Math.floor(Math.random() * 3982) + 18; break;
      case 'dwarf': age = Math.floor(Math.random() * 483) + 18; break;
      case 'halfElf': age = Math.floor(Math.random() * 12) + 15; break;
      case 'goblin': age = Math.floor(Math.random() * 38) + 8; break;
      case 'hobbit': age = Math.floor(Math.random() * 60) + 18; break;
      case 'human':
      default: age = Math.floor(Math.random() * 82) + 18; break;
    }

    let birthPlaces;
    switch (race) {
      case 'elf':
        birthPlaces = ['ElderGrove','Evergrove','Iilyseum','Hellivita','Hellivita','Hellivita'];
        break;
      case 'dwarf':
        birthPlaces = ['Twon','Omber','Garret','Traust','Bonrith','Garret','Omber'];
        break;
      case 'hobbit':
        birthPlaces = ['Twon','Omber','Garret','Traust','Harnford','Bonrith','Harnford','Umbra Hills'];
        break;
      case 'halfElf':
        birthPlaces = ['Evergrove','Twon','Shrift','Bonrith'];
        break;
      case 'human':
      default:
        birthPlaces = ['Twon','Omber','Garret','Bonrith','Traust','Free Cities','Ivory Isles','Umbra Hills','Khari Desert','Stamford'];
        break;
    }

    const birthPlace = randomFromArray(birthPlaces);
    const personality = randomFromArray(personalities);
    const quirk = randomFromArray(quirks);

    const npcHTML = `
      <h2>${name}</h2>
      <p><strong>Race:</strong> ${race.charAt(0).toUpperCase() + race.slice(1)}</p>
      <p><strong>Profession:</strong> ${profession.charAt(0).toUpperCase() + profession.slice(1)}</p>
      <p><strong>Age:</strong> ${age}</p>
      <p><strong>Birth Place:</strong> ${birthPlace}</p>
      <p><strong>Personality:</strong> ${personality}</p>
      <p><strong>Quirk:</strong> ${quirk}</p>
    `;

    const npcDiv = document.getElementById('npcResult');
    npcDiv.innerHTML = npcHTML;
    npcDiv.style.display = 'block';
  }
</script>
