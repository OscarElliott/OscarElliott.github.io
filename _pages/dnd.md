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
    'ambitious',
    'apathetic',
    'arrogant',
    'articulate',
    'awkward',
    'boastful',
    'bold',
    'brave',
    'brooding',
    'calm',
    'carefree',
    'charismatic',
    'cheerful',
    'clever',
    'clumsy',
    'compassionate',
    'courageous',
    'cowardly',
    'coy',
    'cruel',
    'cunning',
    'curious',
    'cynical',
    'decisive',
    'dedicated',
    'diplomatic',
    'dreamy',
    'driven',
    'eccentric',
    'empathetic',
    'energetic',
    'enigmatic',
    'fierce',
    'flirtatious',
    'focused',
    'forgetful',
    'friendly',
    'generous',
    'gentle',
    'grumpy',
    'gullible',
    'hardy',
    'haughty',
    'heroic',
    'honest',
    'hopeful',
    'hot-headed',
    'humble',
    'idealistic',
    'impulsive',
    'inquisitive',
    'intense',
    'intuitive',
    'jaded',
    'jovial',
    'judgmental',
    'kind',
    'lazy',
    'loyal',
    'melancholic',
    'methodical',
    'mischievous',
    'moody',
    'mysterious',
    'naive',
    'nervous',
    'noble',
    'obsessive',
    'optimistic',
    'ornery',
    'outspoken',
    'paranoid',
    'patient',
    'peaceful',
    'persistent',
    'pessimistic',
    'playful',
    'polite',
    'pragmatic',
    'protective',
    'quiet',
    'rash',
    'reckless',
    'reliable',
    'reserved',
    'resourceful',
    'romantic',
    'rude',
    'sarcastic',
    'scheming',
    'secretive',
    'selfish',
    'serious',
    'shy',
    'silly',
    'sly',
    'snarky',
    'stoic',
    'stubborn',
    'superstitious',
    'suspicious',
    'sweet',
    'tactful',
    'tenacious',
    'thoughtful',
    'timid',
    'trusting',
    'vengeful',
    'wise',
    'witty',
    'zealous'
  ];
  const quirks = [
    'hums constantly',
    'has a pet mouse',
    'speaks in rhymes',
    'collects shiny stones',
    'obsessed with soup',
    'always wears a hat',
    'afraid of ducks',
    'taps their foot when nervous',
    'never goes anywhere without a book',
    'has an odd obsession with mirrors',
    'collects feathers from different birds',
    'always quotes ancient texts',
    'talks to animals',
    'loves to dance but has two left feet',
    'sings to plants to help them grow',
    'writes cryptic notes to themselves',
    'never leaves home without a lucky charm',
    'is always late for everything',
    'has a pet rock they carry everywhere',
    'hates the color green',
    'loves to carve intricate patterns into wood',
    'obsessed with collecting keys',
    'speaks in a whisper most of the time',
    'always has a pocket full of breadcrumbs',
    'spends hours staring at the sky',
    'is terrified of thunder',
    'can’t stand the sound of loud noises',
    'writes secret messages in their journal',
    'always carries a candle, even in daylight',
    'is convinced they have a twin somewhere',
    'has a collection of mismatched socks',
    'refuses to eat anything blue',
    'has an extremely high tolerance for spicy food',
    'never travels without a lucky coin',
    'wears mismatched shoes on purpose',
    'has a fear of mirrors',
    'constantly draws on their hands',
    'only speaks in riddles',
    'is convinced that their reflection is following them',
    'collects old coins from around the world',
    'often forgets where they put things',
    'can’t sleep without a lullaby',
    'is always looking for hidden messages in signs',
    'speaks to plants and insists they talk back',
    'has a secret love for playing pranks',
    'pauses to count steps before entering a building',
    'collects empty bottles from various locations',
    'always picks up fallen feathers',
    'wears a mask even in the most mundane situations',
    'always seems to be lost in thought',
    'speaks in an ancient dialect no one understands',
    'knows all the lyrics to old songs',
    'talks to inanimate objects',
    'refuses to walk in a straight line',
    'can never make a decision without flipping a coin',
    'always makes weird noises when they think',
    'insists on eating food in a specific order',
    'is always talking about their dreams',
    'is afraid of small, insignificant things',
    'has a constant desire to rearrange things',
    'always wears mismatched gloves',
    'writes down everything in a secret code',
    'keeps a collection of locks and keys',
    'can’t resist touching anything shiny',
    'is afraid of shadows',
    'talks to strangers like they’re old friends',
    'is addicted to collecting old maps',
    'speaks with their hands a lot',
    'always keeps a handkerchief with them',
    'has a strange affection for clouds',
    'has a knack for accidentally breaking things',
    'can’t stop laughing at their own jokes',
    'believes they’re cursed by a mischievous spirit',
    'refuses to walk under ladders',
    'has a collection of strange hats',
    'writes poetry about everyday objects',
    'never sleeps without a blanket over their head',
    'is obsessed with keeping everything in perfect symmetry',
    'loves to make random sound effects',
    'insists on wearing only one color at a time',
    'collects broken mirrors',
    'keeps a lucky rabbit’s foot they swear brings them good fortune',
    'has a secret stash of candles they hoard',
    'always carries around a tiny notebook',
    'has a special song they hum when stressed',
    'believes in aliens',
    'is terrified of all insects, no matter how small',
    'cannot stop tapping their fingers',
    'collects antique figurines',
    'always looks for hidden treasure wherever they go',
    'spends too much time studying the stars',
    'is terrified of the dark but refuses to use a light source',
    'has an odd attachment to an old, beaten-up book',
    'obsesses over small details and can’t stop fixing them',
    'can’t make eye contact for more than a few seconds',
    'loves to make extravagant entrances',
    'insists on adding “-ington” to the end of their name',
    'talks to their reflection in the water',
    'can never say no to free food',
    'spends too much time organizing their things',
    'has a weird fascination with shoes',
    'refuses to step on cracks in the pavement',
    'always hums when they’re happy',
    'talks to themselves when they’re thinking',
    'has a secret identity they pretend to be',
    'always looks for signs in nature',
    'can’t walk past a bakery without buying something',
    'has a secret love for wearing scarves',
    'talks to the moon like it’s their best friend',
    'can never sit still for too long',
    'keeps a collection of old scrolls with unknown writing on them'
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
