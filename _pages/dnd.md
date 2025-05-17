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
    <option value="random">Random</option>
    <option value="blacksmith">Blacksmith</option>
    <option value="wizard">Wizard</option>
    <option value="merchant">Merchant</option>
    <option value="thief">Thief</option>
    <option value="bard">Bard</option>
    <option value="cleric">Cleric</option>
    <option value="ranger">Ranger</option>
    <option value="alchemist">Alchemist</option>
    <option value="archer">Archer</option>
    <option value="assassin">Assassin</option>
    <option value="barbarian">Barbarian</option>
    <option value="beastmaster">Beastmaster</option>
    <option value="blackguard">Blackguard</option>
    <option value="captain">Captain</option>
    <option value="cartographer">Cartographer</option>
    <option value="conjuror">Conjuror</option>
    <option value="courier">Courier</option>
    <option value="cook">Cook</option>
    <option value="druid">Druid</option>
    <option value="enchanter">Enchanter</option>
    <option value="fletcher">Fletcher</option>
    <option value="gladiator">Gladiator</option>
    <option value="healer">Healer</option>
    <option value="herbalist">Herbalist</option>
    <option value="historian">Historian</option>
    <option value="hunter">Hunter</option>
    <option value="innkeeper">Innkeeper</option>
    <option value="jester">Jester</option>
    <option value="knight">Knight</option>
    <option value="locksmith">Locksmith</option>
    <option value="mage">Mage</option>
    <option value="monk">Monk</option>
    <option value="navigator">Navigator</option>
    <option value="paladin">Paladin</option>
    <option value="pirate">Pirate</option>
    <option value="plague-doctor">Plague Doctor</option>
    <option value="priest">Priest</option>
    <option value="scout">Scout</option>
    <option value="sellsword">Sellsword</option>
    <option value="shaman">Shaman</option>
    <option value="squire">Squire</option>
    <option value="tinker">Tinker</option>
    <option value="trapper">Trapper</option>
    <option value="vagabond">Vagabond</option>
    <option value="vintner">Vintner</option>
    <option value="warlock">Warlock</option>
    <option value="watchman">Watchman</option>
    <option value="weaver">Weaver</option>
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

  const emesianConnections = [
  'Secretly a member of the clock',
  'Undercover member of the Grey Nails',
  'Deeply religious to Seldarine',
  'Deeply religious to Ioun',
  'Devout member of Brotherhood of the Book',
  'Escaped from Omber\'s slave pits',
  'Was briefly a slave master in the Omber Slave pits',
  'Had family die of starvation in the great voyage to EdlerGrove',
  'Survived the great voyage to EdlerGrove',
  'Travelled to the free cities of the south',
  'Previously worked as a smuggler in Bonrith',
  'Claims to be a bastard of a noble house',
  'Works in the Kraghammer Trading Company',
  'Spy for the Grandir Resistance, feeding intel from within the Emesian Alliance',
  'Tattooed with an illegal Lineage Mark, passing as noble',
  'Born in the ruins of Shrift during the siege, raised among mercenaries',
  'One of the first humans allowed to walk the spires of Evergrove',
  'Family perished in the fall of Garret, swears vengeance on the Kraghammer',
  'Grew up in the Outer Districts of Bonrith, under the Clock’s protection',
  'Wandered the war-torn Traust Fields as a caravan guard for halfling merchants',
  'Banished from Twon for striking an elven noble',
  'Studied time-magic under a rogue diviner linked to the Clock',
  'Former apprentice to the Council of the Seven, expelled for forbidden experimentation',
  'Came of age during the fall of Garret—still has nightmares of the Vorgaz',
  'Trained in ritual magic at the Atem University but failed final Trials',
  'Once tasked with delivering a forged noble Lineage Mark',
  'Smuggled relics out of the ruined city of Omber',
  'Worked as a salvager in the wreckage of Garret—lost something they can’t explain',
  'Illegitimate child of a voidmarked noble from Bonrith',
  'Last living heir of a disgraced merchant house from Omber',
  'Believes Ioun speaks directly to them through dreams',
  'Fought in the Battle of Severance, left for dead in the bloodstorm',
  'Escaped a Vorgaz raid with only a shard of their village’s temple',
  'Claims descent from Aster, the prophet-king of Da’Quan',
  'Survived an attempted ritual sacrifice by apocalyptic cultists in Bonrith',
  'Knows secret passageways beneath the Starvault from childhood exploring',
  'Carries a cursed relic believed to belong to Taenya Elatumal',
  'Once heard the Final Chime during a dream and woke up days later miles from home',
  'Served in a conscripted militia out of Bonrith, lost most of their company',
  'Sought passage to Evergrove for love, but was turned away at the gates',
  'Bears a glyph seared into their palm from a forbidden scroll',
  'Lost a sibling to Brotherhood of the Book zealotry',
  'Witnessed a dragon fly over the Emberdeep Mines as a child',
  'Hunted by bounty hunters for breaking a contract with a noble house',
  'Dreams in Emesian, despite never having studied the language',
  'Carries a journal they don’t remember writing',
  'Claims they died once and simply got up again',
  'Came face to face with a Vorgaz and survived',
  'Best friend was killed by an Owlbear while hunting in Twill Forest near Shrift',
  'Learned how to fight from a retired mercenary in the Emberrun Hills west of Bonrith',
  'Stole a sacred relic from a ruined temple in the Whispering Marsh, north of Twon',
  'Spent childhood tending sheep on the Cloudfen Ridge near Stamford',
  'Once got lost for three days in the Misty Spruce Woods outside Evergrove',
  'Trained as a monk at the Cragspire Monastery, high above the cliffs near Twon',
  'Parents were merchants slain by bandits on the Dustvale Road between Bonrith and Shrift',
  'Saw a falling star crash into the Hollow Peaks east of Shrift—still has the scorched stone',
  'Found a wounded griffon in the hills behind the Moonspire Citadel in Twon',
  'Was rescued from quicksand in the Pale Fen near Oralean by a passing druid',
  'Learned music in a halfling caravan that camped each spring in the Glades of Oldwood near Stamford',
  'Taught to read by a retired Brotherhood of the Book scribe in the Candlereach Hamlet south of Bonrith',
  'Grew up a salve collecting fire beetles from the sulfur caves near Omber’s ruins',
  'Once led a militia defense of a village on the border of the Traust Fields',
  'Hunted undead with a paladin near the grave-cursed ruins of Westgate outside Twon',
  'Sailed with smugglers off the coral-strewn Biting Coast west of Twon',
  'Witnessed a duel between two nobles in the Garden of Whispers near Bonrith’s Inner Ring',
  'Was held captive in a bandit fort hidden deep in the Scorchpine Woods east of Omber',
  'Studied celestial events from an abandoned observatory atop Starwatch Hill outside Oralean',
  'Fought alongside dwarves during a goblin raid on the collapsed mining town of Deepcrag near Garret',
  'Earned coin playing cards in the rowdy taverns of Docksdown, Twon’s lower harbor district',
  'Served time in the Tower of Windward Justice in Twon for a crime they didn’t commit',
  'Previously worked collecting tolls on the Sighing Bridge near Bonrith',
  'Was trained in stealth by a fugitive thief in the Whishbone Alley in Bonrith’s Outer Districts',
  'Joined a failed expedition to map the Deadlight Thicket near the edge of Mistwood, beyond Evergrove',
  'Spent a winter with rangers patrolling the burned forests south of Shrift',
  'Carried messages through the Slatedeep Mines beneath the cliffs outside Twon',
  'Suffered frostbite during a trek through the Stormcaller Pass near the northern border of the Alliance',
  'Once swam with nixies in the silver-green waters of Lake Ilenth near Stamford',
  'Delivered food to starving refugees in the ruined outskirts of Shrift during the siege',
  'Witnessed a dragon battle from the rooftops of Bonrith during a sky-cleaving storm',
  'Captured a runaway horse for a noble’s daughter in the Windward Fields outside Oralean',
  'Met a talking fox while lost in the Mossstep Paths near the Mistwood’s border',
  'Once duelled a minor noble with wooden swords in the training yard of the Starvault in Bonrith',
  'Worked as a fisher in the salt-choked shallows of Bleak Shoal outside Twon',
  'Found a glowing rune stone embedded in a tree in the Bloomheart Copse near Stamford',
  'Learned archery from a traveling elven hunter camped outside the Thornvale south of Twon',
  'Was robbed and left for dead on the Embertrail near Omber—but mysteriously healed overnight',
  'Joined a halfling festival in Grainwatch just before it was raided by goblins from the west',
  'Buried their sibling in a secret grove near the river-split village of Dathmere outside Bonrith',
  'Once saw a ghost ship drift silently past the cliffs of Twon on a windless night',
  'Woke up in a ring of mushrooms with no memory near the edge of Evergrove',
  'Rescued an old enemy from a sinkhole in the Windwhistle Downs near Stamford'
];


  const professions = [
    'blacksmith', 'wizard', 'merchant', 'thief', 'bard', 'cleric', 'ranger', 'alchemist',
    'archer', 'assassin', 'barbarian', 'beastmaster', 'blackguard', 'captain', 'cartographer',
    'conjuror', 'courier', 'cook', 'druid', 'enchanter', 'fletcher', 'gladiator', 'healer',
    'herbalist', 'historian', 'hunter', 'innkeeper', 'jester', 'knight', 'locksmith', 'mage',
    'monk', 'navigator', 'paladin', 'pirate', 'plague-doctor', 'priest', 'scout', 'sellsword',
    'shaman', 'squire', 'tinker', 'trapper', 'vagabond', 'vintner', 'warlock', 'watchman', 'weaver'
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

  async function loadLastNames(race) {
    if (!lastNameLists[race]) {
      try {
        const response = await fetch(`/assets/dndGenLists/lastNames/${race}.txt`);
        if (!response.ok) throw new Error('Failed to fetch names');
        const text = await response.text();
        lastNameLists[race] = text.split('\n').map(name => name.trim()).filter(name => name.length > 0);
      } catch (err) {
        console.error(err);
        alert(`Could not load last names for ${race}`);
        lastNameLists[race] = ['Nameless'];
      }
    }
  }

  async function generateNPC() {
    const race = document.getElementById('race').value;
    const profession = document.getElementById('profession').value;

    // If 'random' is selected, choose a random profession
    const selectedProfession = profession === 'random' ? randomFromArray(professions) : profession;

    await loadNames(race);
    await loadLastNames(race);
    const names = nameLists[race];
    const lastNames = lastNameLists[race];
    const name = randomFromArray(names);
    const lastName = randomFromArray(lastNames);

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
    const emesianConnection = randomFromArray(emesianConnections);

    const npcHTML = `
      <h2>${name} ${lastName}</h2>
      <p><strong>Race:</strong> ${race.charAt(0).toUpperCase() + race.slice(1)}</p>
      <p><strong>Profession:</strong> ${profession.charAt(0).toUpperCase() + profession.slice(1)}</p>
      <p><strong>Age:</strong> ${age}</p>
      <p><strong>Birth Place:</strong> ${birthPlace}</p>
      <p><strong>Personality:</strong> ${personality}</p>
      <p><strong>Quirk:</strong> ${quirk}</p>
      <p><strong>Hook:</strong> ${emesianConnection}</p>
    `;

    const npcDiv = document.getElementById('npcResult');
    npcDiv.innerHTML = npcHTML;
    npcDiv.style.display = 'block';
  }
</script>
