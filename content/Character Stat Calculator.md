<div style="padding: 1.5rem; border: 1px solid var(--lightgray); border-radius: 8px; background-color: var(--light); max-width: 450px;">
  <h3 style="margin-top: 0; margin-bottom: 5px;">Character Stats</h3>
  <p style="font-size: 0.9em; color: var(--darkgray); margin-top: 0; margin-bottom: 20px;">
    <strong>Standard Array:</strong> +3, +2, +2, +1, +1, +0, -1, -2
  </p>

  <div style="margin-bottom: 20px;">
    <label style="font-weight: bold; margin-right: 10px; color: var(--darkgray);">Creature Size:</label>
    <select id="creatureSize" style="padding: 6px; border-radius: 4px; background: var(--light); color: var(--dark); border: 1px solid var(--gray); font-size: 1em; cursor: pointer;">
      <option value="Tiny">Tiny (Cat, Fairy)</option>
      <option value="Small">Small (Halfling, Wolf)</option>
      <option value="Medium" selected>Medium (Human)</option>
      <option value="Large">Large (Half-Giant)</option>
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
