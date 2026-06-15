1. Step base stats
   **Standard Array**: +3, +2, +2, +1, +1, +0, -1, -2
   to

|   [[Strength]]   |
| :--------------: |
|   [[Agility]]    |
|  [[Precision]]   |
| [[Constitution]] |
|  [[Awareness]]   |
|   [[Charisma]]   |
| [[Intelligence]] |
|   [[Sorcery]]    |

2. Step
   Select
   -Core Ancestry:
   -Additional Ancestry:

those determine Creature Size which alters stats

3. Step

<div style="padding: 1.5rem; border: 1px solid var(--lightgray); border-radius: 8px; background-color: var(--light); max-width: 600px;">
  <h3 style="margin-top: 0; margin-bottom: 15px;">Dynamic Background Selection</h3>

  <div style="margin-bottom: 20px;">
    <select id="backgroundSelect" style="width: 100%; padding: 8px; border-radius: 4px; background: var(--light); color: var(--dark); border: 1px solid var(--gray); font-size: 1.1em; cursor: pointer; font-weight: bold;">
      <option>Loading backgrounds from system...</option>
    </select>
  </div>

  <div id="backgroundDetails" style="padding: 15px; border-radius: 6px; background-color: rgba(0,0,0,0.03); border: 1px solid var(--lightgray);">
    <p style="margin-top: 0; margin-bottom: 8px;"><strong style="color: var(--darkgray);">Ability Scores:</strong> <span id="bg_abilityScores" style="color: var(--dark);">--</span></p>
    <p style="margin-top: 0; margin-bottom: 8px;"><strong style="color: var(--darkgray);">Saving Throws:</strong> <span id="bg_savingThrows" style="color: var(--dark);">--</span></p>
    <p style="margin-top: 0; margin-bottom: 8px;"><strong style="color: var(--darkgray);">General Skill Ranks:</strong> <span id="bg_generalSkills" style="color: var(--dark);">--</span></p>
    <p style="margin-top: 0; margin-bottom: 8px;"><strong style="color: var(--darkgray);">Expert Skill Ranks:</strong> <span id="bg_expertSkills" style="color: var(--dark);">--</span></p>
    <p style="margin-top: 0; margin-bottom: 8px;"><strong style="color: var(--darkgray);">Talents:</strong> <span id="bg_talents" style="color: var(--tertiary); font-weight: bold;">--</span></p>
    <p style="margin-top: 0; margin-bottom: 8px;"><strong style="color: var(--darkgray);">Equipment:</strong> <span id="bg_equipment" style="color: var(--dark);">--</span></p>
    <p style="margin-top: 0; margin-bottom: 0;"><strong style="color: var(--darkgray);">Initial Wealth:</strong> <span id="bg_wealth" style="color: var(--secondary); font-weight: bold;">--</span></p>
  </div>

  <script>
    // 1. Regex Slicer: Extracts data blocks based on your exact text line syntax
    function extractField(text, fieldName) {
      const targetMap = ["Ability Scores", "Saving Throws", "General Skill Ranks", "Expert Skill Ranks", "Talents", "Equipment", "Initial Wealth"];
      const index = text.indexOf(fieldName + ":");
      if (index === -1) return "None";

      let start = index + fieldName.length + 1;
      let remainder = text.substring(start).trim();

      // Look ahead to find where the next section block kicks off to slice accurately
      let cutIndex = remainder.length;
      targetMap.forEach(f => {
        const nextFieldPos = remainder.indexOf(f + ":");
        if (nextFieldPos !== -1 && nextFieldPos < cutIndex) {
          cutIndex = nextFieldPos;
        }
      });

      return remainder.substring(0, cutIndex).trim().replace(/[\r\n]+/g, ' ');
    }

    // 2. UI Painter
    function updateBackground() {
      const selected = document.getElementById('backgroundSelect').value;
      if (!window.allBackgroundData || !window.allBackgroundData[selected]) return;
      
      const data = window.allBackgroundData[selected];

      document.getElementById('bg_abilityScores').textContent = data.abilityScores;
      document.getElementById('bg_savingThrows').textContent = data.savingThrows;
      document.getElementById('bg_generalSkills').textContent = data.generalSkills;
      document.getElementById('bg_expertSkills').textContent = data.expertSkills;
      document.getElementById('bg_talents').textContent = data.talents;
      document.getElementById('bg_equipment').textContent = data.equipment;
      document.getElementById('bg_wealth').textContent = data.wealth;
    }

    // 3. Fetch Quartz's build index
    const indexPath = window.location.origin + "/static/contentIndex.json";

    fetch(indexPath)
      .then(res => {
        if (!res.ok) throw new Error("Index file not found");
        return res.json();
      })
      .then(data => {
        const selectEl = document.getElementById('backgroundSelect');
        const backgrounds = {};

        for (const [slug, pageData] of Object.entries(data)) {
          // Identify files categorized under your #background tag
          if (pageData.tags && pageData.tags.includes('background') && pageData.content) {
            const title = pageData.title || slug;
            
            // Skip the index/template documents cleanly
            if (title === "Background Template" || title === "Character Creation Guide") continue;

            const text = pageData.content;
            backgrounds[title] = {
              abilityScores: extractField(text, "Ability Scores"),
              savingThrows: extractField(text, "Saving Throws"),
              generalSkills: extractField(text, "General Skill Ranks"),
              expertSkills: extractField(text, "Expert Skill Ranks"),
              talents: extractField(text, "Talents"),
              equipment: extractField(text, "Equipment"),
              wealth: extractField(text, "Initial Wealth")
            };
          }
        }

        const sortedNames = Object.keys(backgrounds).sort();

        if (sortedNames.length === 0) {
          selectEl.innerHTML = '<option>No files found with the #background tag</option>';
          return;
        }

        selectEl.innerHTML = '';
        sortedNames.forEach(name => {
          const opt = document.createElement('option');
          opt.value = name;
          opt.textContent = name;
          backgroundSelect.appendChild(opt);
        });

        window.allBackgroundData = backgrounds;
        updateBackground();
      })
      .catch(err => {
        console.error("Failed to load backgrounds dynamically from Quartz index:", err);
        document.getElementById('backgroundSelect').innerHTML = '<option>Error harvesting system data</option>';
      });

    document.getElementById('backgroundSelect').addEventListener('change', updateBackground);
  </script>

</div>

<div style="padding: 1.5rem; border: 1px solid var(--lightgray); border-radius: 8px; background-color: var(--light); max-width: 450px;">
  <h3 style="margin-top: 0; margin-bottom: 5px;">Character Stats</h3>
  <p style="font-size: 0.9em; color: var(--darkgray); margin-top: 0; margin-bottom: 20px;">
    <strong>Standard Array:</strong> +3, +2, +2, +1, +1, +0, -1, -2
  </p>

  <div style="margin-bottom: 20px;">
    <label style="font-weight: bold; margin-right: 10px; color: var(--darkgray);">Creature Size:</label>
    <select id="creatureSize" style="padding: 6px; border-radius: 4px; background: var(--light); color: var(--dark); border: 1px solid var(--gray); font-size: 1em; cursor: pointer;">
      <option value="Tiny">Tiny</option>
      <option value="Small">Small</option>
      <option value="Medium" selected>Medium</option>
      <option value="Large">Large</option>
    </select>
  </div>

  <table style="width: 100%; border-collapse: collapse; text-align: center;">
    <thead>
      <tr style="border-bottom: 2px solid var(--lightgray); color: var(--darkgray);">
        <th style="text-align: left; padding-bottom: 8px;">Ability</th>
        <th style="padding-bottom: 8px;">Base</th>
        <th style="padding-bottom: 8px;">Size Mod</th>
        <th style="padding-bottom: 8px;">Final</th>
      </tr>
    </thead>
    <tbody id="statTableBody">
      <!-- Strength -->
      <tr style="border-bottom: 1px solid var(--lightgray);">
        <td style="text-align: left; padding: 8px 0; font-weight: bold;">Strength</td>
        <td><input type="number" id="base_Strength" value="3" style="width: 50px; text-align: center; padding: 4px; border: 1px solid var(--gray); border-radius: 4px;"></td>
        <td id="mod_Strength" style="color: var(--darkgray);">0</td>
        <td id="final_Strength" style="font-weight: bold; font-size: 1.1em; color: var(--tertiary);">0</td>
      </tr>
      <!-- Agility -->
      <tr style="border-bottom: 1px solid var(--lightgray);">
        <td style="text-align: left; padding: 8px 0; font-weight: bold;">Agility</td>
        <td><input type="number" id="base_Agility" value="2" style="width: 50px; text-align: center; padding: 4px; border: 1px solid var(--gray); border-radius: 4px;"></td>
        <td id="mod_Agility" style="color: var(--darkgray);">0</td>
        <td id="final_Agility" style="font-weight: bold; font-size: 1.1em; color: var(--tertiary);">0</td>
      </tr>
      <!-- Precision -->
      <tr style="border-bottom: 1px solid var(--lightgray);">
        <td style="text-align: left; padding: 8px 0; font-weight: bold;">Precision</td>
        <td><input type="number" id="base_Precision" value="2" style="width: 50px; text-align: center; padding: 4px; border: 1px solid var(--gray); border-radius: 4px;"></td>
        <td id="mod_Precision" style="color: var(--darkgray);">0</td>
        <td id="final_Precision" style="font-weight: bold; font-size: 1.1em; color: var(--tertiary);">0</td>
      </tr>
      <!-- Constitution -->
      <tr style="border-bottom: 1px solid var(--lightgray);">
        <td style="text-align: left; padding: 8px 0; font-weight: bold;">Constitution</td>
        <td><input type="number" id="base_Constitution" value="1" style="width: 50px; text-align: center; padding: 4px; border: 1px solid var(--gray); border-radius: 4px;"></td>
        <td id="mod_Constitution" style="color: var(--darkgray);">0</td>
        <td id="final_Constitution" style="font-weight: bold; font-size: 1.1em; color: var(--tertiary);">0</td>
      </tr>
      <!-- Awareness -->
      <tr style="border-bottom: 1px solid var(--lightgray);">
        <td style="text-align: left; padding: 8px 0; font-weight: bold;">Awareness</td>
        <td><input type="number" id="base_Awareness" value="1" style="width: 50px; text-align: center; padding: 4px; border: 1px solid var(--gray); border-radius: 4px;"></td>
        <td id="mod_Awareness" style="color: var(--darkgray);">0</td>
        <td id="final_Awareness" style="font-weight: bold; font-size: 1.1em; color: var(--tertiary);">0</td>
      </tr>
      <!-- Charisma -->
      <tr style="border-bottom: 1px solid var(--lightgray);">
        <td style="text-align: left; padding: 8px 0; font-weight: bold;">Charisma</td>
        <td><input type="number" id="base_Charisma" value="0" style="width: 50px; text-align: center; padding: 4px; border: 1px solid var(--gray); border-radius: 4px;"></td>
        <td id="mod_Charisma" style="color: var(--darkgray);">0</td>
        <td id="final_Charisma" style="font-weight: bold; font-size: 1.1em; color: var(--tertiary);">0</td>
      </tr>
      <!-- Intelligence -->
      <tr style="border-bottom: 1px solid var(--lightgray);">
        <td style="text-align: left; padding: 8px 0; font-weight: bold;">Intelligence</td>
        <td><input type="number" id="base_Intelligence" value="-1" style="width: 50px; text-align: center; padding: 4px; border: 1px solid var(--gray); border-radius: 4px;"></td>
        <td id="mod_Intelligence" style="color: var(--darkgray);">0</td>
        <td id="final_Intelligence" style="font-weight: bold; font-size: 1.1em; color: var(--tertiary);">0</td>
      </tr>
      <!-- Sorcery -->
      <tr>
        <td style="text-align: left; padding: 8px 0; font-weight: bold;">Sorcery</td>
        <td><input type="number" id="base_Sorcery" value="-2" style="width: 50px; text-align: center; padding: 4px; border: 1px solid var(--gray); border-radius: 4px;"></td>
        <td id="mod_Sorcery" style="color: var(--darkgray);">0</td>
        <td id="final_Sorcery" style="font-weight: bold; font-size: 1.1em; color: var(--tertiary);">0</td>
      </tr>
    </tbody>
  </table>

  <script>
    // 1. Define the size modifiers
    const sizeMods = {
      "Tiny":   { "Strength": -4, "Agility": 4,  "Precision": 2,  "Constitution": -2 },
      "Small":  { "Strength": -2, "Agility": 2,  "Precision": 1,  "Constitution": -1 },
      "Medium": { "Strength": 0,  "Agility": 0,  "Precision": 0,  "Constitution": 0 },
      "Large":  { "Strength": 2,  "Agility": -2, "Precision": -1, "Constitution": 1 }
    };

    const statsList = ['Strength', 'Agility', 'Precision', 'Constitution', 'Awareness', 'Charisma', 'Intelligence', 'Sorcery'];

    // Helper to format numbers with a plus sign (e.g., +3 instead of just 3)
    function formatStat(num) {
      if (num > 0) return "+" + num;
      return num;
    }

    // 2. The Calculation Engine
    function calculateStats() {
      const size = document.getElementById('creatureSize').value;
      const currentMods = sizeMods[size];

      statsList.forEach(stat => {
        // Get the base value from the input box
        const baseInput = document.getElementById('base_' + stat).value;
        const base = baseInput === "" ? 0 : parseInt(baseInput);

        // Get the size modifier (defaults to 0 for mental stats that aren't affected)
        const mod = currentMods[stat] || 0;

        // Calculate final score
        const final = base + mod;

        // Update the HTML
        document.getElementById('mod_' + stat).textContent = formatStat(mod);
        document.getElementById('final_' + stat).textContent = formatStat(final);
      });
    }

    // 3. Attach Listeners so it updates automatically
    document.getElementById('creatureSize').addEventListener('change', calculateStats);
    
    statsList.forEach(stat => {
      document.getElementById('base_' + stat).addEventListener('input', calculateStats);
    });

    // 4. Run once on load to populate the initial table
    calculateStats();
  </script>

</div>

**Ability Scores.** A background lists four [[Ability Score|Ability Scores]]. Increase three of them by 1.

**Saving Throws.** A background lists three [[Saving Throw|Saving Throws]]. Increase two of them by 1 [[Rank]].

**General Skill Ranks.** Distribute 4 [[Rank|Ranks]] among a list of [[General Skill|General Skills]] listed in background.

**Expert Skill Ranks.** Distribute 3 [[Rank|Ranks]] among a list of [[Expert Skill|Expert Skills]] listed in background.

1. Creature Size
2. Standard Array: **Standard Array**: +3, +2, +2, +1, +1, +0, -1, -2
3. Background stats
4. Increase Ability: +
5.

drop down: creature size
options:

|  [[Tiny]]  |
| :--------: |
| [[Small]]  |
| [[Medium]] |
| [[Large]]  |
