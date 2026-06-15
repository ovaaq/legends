<div style="padding: 1.5rem; border: 1px solid var(--lightgray); border-radius: 8px; background-color: var(--light); max-width: 800px; font-family: sans-serif;">
  <h2 style="margin-top: 0; border-bottom: 2px solid var(--tertiary); padding-bottom: 10px;">Legends Character Builder</h2>

  <div style="margin-bottom: 25px; padding: 15px; border: 1px solid var(--lightgray); border-radius: 6px; background: rgba(0,0,0,0.02);">
    <h3 style="margin-top: 0;">1. Standard Array</h3>
    <p style="font-size: 0.9em; color: var(--darkgray);">Distribute these values into your abilities: <strong>+3, +2, +2, +1, +1, +0, -1, -2</strong></p>
    <div id="arrayWarning" style="color: red; font-size: 0.85em; font-weight: bold; margin-bottom: 10px;"></div>
    <div style="display: grid; grid-template-columns: repeat(4, 1fr); gap: 10px;" id="standardArrayInputs">
      </div>
  </div>

  <div style="margin-bottom: 25px; padding: 15px; border: 1px solid var(--lightgray); border-radius: 6px; background: rgba(0,0,0,0.02);">
    <h3 style="margin-top: 0;">2. Select Ancestry</h3>
    <div style="display: flex; gap: 15px; flex-wrap: wrap;">
      <div style="flex: 1; min-width: 200px;">
        <label style="font-weight: bold; font-size: 0.9em; color: var(--darkgray);">Core Ancestry</label>
        <select id="coreAncestrySelect" class="calc-trigger" style="width: 100%; padding: 8px; border-radius: 4px; border: 1px solid var(--gray);"></select>
      </div>
      <div style="flex: 1; min-width: 200px;">
        <label style="font-weight: bold; font-size: 0.9em; color: var(--darkgray);">Additional Ancestry</label>
        <select id="addAncestrySelect" class="calc-trigger" style="width: 100%; padding: 8px; border-radius: 4px; border: 1px solid var(--gray);"></select>
      </div>
    </div>
  </div>

  <div style="margin-bottom: 25px; padding: 15px; border: 1px solid var(--lightgray); border-radius: 6px; background: rgba(0,0,0,0.02);">
    <h3 style="margin-top: 0;">3. Background</h3>
    <select id="backgroundSelect" class="calc-trigger" style="width: 100%; padding: 8px; margin-bottom: 15px; border-radius: 4px; font-weight: bold;"></select>

```
<div id="backgroundDetails" style="font-size: 0.9em; border-left: 3px solid var(--secondary); padding-left: 10px; margin-bottom: 15px;">
  <p style="margin: 4px 0;"><strong>Talents:</strong> <span id="bg_talents">--</span> | <strong>Wealth:</strong> <span id="bg_wealth">--</span></p>
  <p style="margin: 4px 0;"><strong>Equipment:</strong> <span id="bg_equipment">--</span></p>
</div>

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px;">
  <div style="background: var(--light); padding: 10px; border-radius: 6px; border: 1px solid var(--lightgray);">
    <div style="font-weight: bold; margin-bottom: 8px; font-size: 0.9em;">Ability Scores <span id="abilityCounter" style="color: var(--tertiary); float: right;">0/3</span></div>
    <div id="choice_abilityScores" style="display: flex; flex-direction: column; gap: 5px;"></div>
  </div>
  <div style="background: var(--light); padding: 10px; border-radius: 6px; border: 1px solid var(--lightgray);">
    <div style="font-weight: bold; margin-bottom: 8px; font-size: 0.9em;">Saving Throws <span id="savingCounter" style="color: var(--tertiary); float: right;">0/2</span></div>
    <div id="choice_savingThrows" style="display: flex; flex-direction: column; gap: 5px;"></div>
  </div>
  <div style="background: var(--light); padding: 10px; border-radius: 6px; border: 1px solid var(--lightgray);">
    <div style="font-weight: bold; margin-bottom: 8px; font-size: 0.9em;">Gen Skills (Ranks: <span id="genPointsCounter">4</span>)</div>
    <div id="choice_generalSkills" style="display: flex; flex-direction: column; gap: 5px;"></div>
  </div>
  <div style="background: var(--light); padding: 10px; border-radius: 6px; border: 1px solid var(--lightgray);">
    <div style="font-weight: bold; margin-bottom: 8px; font-size: 0.9em;">Exp Skills (Ranks: <span id="expPointsCounter">3</span>)</div>
    <div id="choice_expertSkills" style="display: flex; flex-direction: column; gap: 5px;"></div>
  </div>
</div>
```

  </div>

  <div style="margin-bottom: 25px; padding: 15px; border: 1px solid var(--lightgray); border-radius: 6px; background: rgba(0,0,0,0.02);">
    <h3 style="margin-top: 0;">4. Free Skills</h3>
    <div style="margin-bottom: 10px;">
      <label><input type="radio" name="freeSkillMode" value="mixed" checked class="calc-trigger"> 1 Expert & 1 General Rank</label>
      <label style="margin-left: 15px;"><input type="radio" name="freeSkillMode" value="general" class="calc-trigger"> 3 General Ranks</label>
    </div>
    <div id="freeSkillContainer" style="display: flex; gap: 10px; flex-wrap: wrap;">
      </div>
  </div>

  <div style="margin-bottom: 25px; padding: 15px; border: 1px solid var(--lightgray); border-radius: 6px; background: rgba(0,0,0,0.02);">
    <h3 style="margin-top: 0;">5. Base Talents</h3>
    <div style="display: flex; gap: 15px;">
      <label style="font-size: 0.9em;">Inc. Health <input type="number" id="tal_health" value="0" min="0" style="width:50px;" class="calc-trigger"></label>
      <label style="font-size: 0.9em;">Inc. Mana <input type="number" id="tal_mana" value="0" min="0" style="width:50px;" class="calc-trigger"></label>
      <label style="font-size: 0.9em;">Inc. Stamina <input type="number" id="tal_stamina" value="0" min="0" style="width:50px;" class="calc-trigger"></label>
    </div>
  </div>

  <div style="padding: 15px; border: 2px solid var(--dark); border-radius: 6px; background: var(--light);">
    <h3 style="margin-top: 0; color: var(--tertiary);">6. Character Summary</h3>

```
<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px;">
  
  <div>
    <h4 style="margin: 0 0 5px 0; border-bottom: 1px solid var(--gray);">Final Ability Scores</h4>
    <div id="summary_abilities" style="display: grid; grid-template-columns: 1fr 1fr; font-size: 0.9em; margin-bottom: 15px;"></div>
    
    <h4 style="margin: 0 0 5px 0; border-bottom: 1px solid var(--gray);">Final Skills & Saves</h4>
    <div id="summary_skills" style="font-size: 0.85em;"></div>
  </div>

  <div style="background: rgba(0,0,0,0.03); padding: 10px; border-radius: 6px;">
    <h4 style="margin: 0 0 10px 0; border-bottom: 1px solid var(--gray);">Combat Statistics</h4>
    <table style="width: 100%; font-size: 0.85em; border-collapse: collapse;">
      <tbody id="summary_combat"></tbody>
    </table>
  </div>

</div>
```

  </div>

  <script>
    // --- CORE DATA CONFIG ---
    const ABILITIES = ["Strength", "Agility", "Precision", "Constitution", "Awareness", "Charisma", "Intelligence", "Sorcery"];
    const REQUIRED_ARRAY = [3, 2, 2, 1, 1, 0, -1, -2].sort();
    
    // Global Vault Storage
    window.vaultData = {
      backgrounds: {},
      coreAncestries: [],
      addAncestries: [],
      generalSkills: [],
      expertSkills: []
    };

    // --- UI GENERATORS & HANDLERS ---
    
    // 1. Standard Array Builder
    function initStandardArray() {
      const container = document.getElementById('standardArrayInputs');
      ABILITIES.forEach(stat => {
        const div = document.createElement('div');
        div.innerHTML = `<label style="font-size: 0.85em; font-weight: bold; color: var(--darkgray); display:block;">${stat}</label>
                         <input type="number" id="arr_${stat}" class="calc-trigger arr-input" value="0" style="width:100%; padding:4px; border:1px solid var(--gray); border-radius:4px;">`;
        container.appendChild(div);
      });
    }

    // Array Validation check
    function validateArray() {
      const inputs = Array.from(document.querySelectorAll('.arr-input')).map(i => parseInt(i.value) || 0).sort();
      const isValid = JSON.stringify(inputs) === JSON.stringify(REQUIRED_ARRAY);
      const warning = document.getElementById('arrayWarning');
      if (!isValid) {
        warning.textContent = "Warning: Values do not match standard array (+3, +2, +2, +1, +1, +0, -1, -2)";
      } else {
        warning.textContent = "";
      }
    }

    // Free Skills Form Rebuilder
    function updateFreeSkillsUI() {
      const mode = document.querySelector('input[name="freeSkillMode"]:checked').value;
      const container = document.getElementById('freeSkillContainer');
      container.innerHTML = '';
      
      const makeSelect = (id, options) => {
        const sel = document.createElement('select');
        sel.id = id;
        sel.className = 'calc-trigger';
        sel.style.cssText = "padding: 6px; border-radius: 4px; border: 1px solid var(--gray);";
        sel.innerHTML = `<option value="">-- Select Skill --</option>` + 
          options.map(o => `<option value="${o}">${o}</option>`).join('');
        return sel;
      };

      if (mode === 'mixed') {
        container.appendChild(makeSelect('fs_exp1', window.vaultData.expertSkills));
        container.appendChild(makeSelect('fs_gen1', window.vaultData.generalSkills));
      } else {
        container.appendChild(makeSelect('fs_gen1', window.vaultData.generalSkills));
        container.appendChild(makeSelect('fs_gen2', window.vaultData.generalSkills));
        container.appendChild(makeSelect('fs_gen3', window.vaultData.generalSkills));
      }
      bindCalcTriggers(); // Rebind new selects to main update loop
      calculateSummary();
    }

    // Setup Background Fetching Engine (from your previous prompt)
    function parseToArray(str) { return (!str || str === "None" || str === "--") ? [] : str.split(',').map(s => s.trim()).filter(s=>s); }
    
    function extractField(text, fieldName) {
      const targetMap = ["Ability Scores", "Saving Throws", "General Skill Ranks", "Expert Skill Ranks", "Talents", "Equipment", "Initial Wealth"];
      const index = text.indexOf(fieldName + ":");
      if (index === -1) return "None";
      let remainder = text.substring(index + fieldName.length + 1).trim();
      let cutIndex = remainder.length;
      targetMap.forEach(f => {
        const nextPos = remainder.indexOf(f + ":");
        if (nextPos !== -1 && nextPos < cutIndex) cutIndex = nextPos;
      });
      return remainder.substring(0, cutIndex).trim().replace(/[\r\n]+/g, ' ');
    }

    function buildCheckboxes(containerId, items, max, counterId) {
      const container = document.getElementById(containerId);
      container.innerHTML = '';
      if(!items.length) return;
      items.forEach(item => {
        const lbl = document.createElement('label');
        lbl.style.cssText = "display: flex; gap: 5px; font-size: 0.85em;";
        lbl.innerHTML = `<input type="checkbox" value="${item}" class="bg-cb calc-trigger" data-max="${max}"> ${item}`;
        container.appendChild(lbl);
      });
      
      // Enforce Max Checkboxes logic
      container.querySelectorAll('input').forEach(cb => {
        cb.addEventListener('change', (e) => {
          const checked = container.querySelectorAll('input:checked');
          if (checked.length > max) e.target.checked = false;
          document.getElementById(counterId).textContent = `${container.querySelectorAll('input:checked').length}/${max}`;
          calculateSummary();
        });
      });
    }

    function buildAllocators(containerId, items, max, counterId) {
      const container = document.getElementById(containerId);
      container.innerHTML = '';
      if(!items.length) { document.getElementById(counterId).textContent = "0"; return; }
      items.forEach(item => {
        const div = document.createElement('div');
        div.style.cssText = "display:flex; justify-content:space-between; font-size:0.85em; margin-bottom:2px;";
        div.innerHTML = `<span>${item}</span> <input type="number" class="bg-alloc calc-trigger" data-skill="${item}" min="0" max="${max}" value="0" style="width:40px; text-align:center; padding:1px;">`;
        container.appendChild(div);
      });

      // Enforce Point Pool Logic
      container.querySelectorAll('input').forEach(input => {
        input.addEventListener('input', () => {
          let total = 0;
          container.querySelectorAll('input').forEach(inp => total += (parseInt(inp.value)||0));
          if (total > max) {
            input.value = (parseInt(input.value)||0) - (total - max);
            total = max;
          }
          document.getElementById(counterId).textContent = (max - total).toString();
          calculateSummary();
        });
      });
    }

    function updateBackground() {
      const sel = document.getElementById('backgroundSelect').value;
      const data = window.vaultData.backgrounds[sel];
      if(!data) return;

      document.getElementById('bg_talents').textContent = data.talents;
      document.getElementById('bg_equipment').textContent = data.equipment;
      document.getElementById('bg_wealth').textContent = data.wealth;

      buildCheckboxes('choice_abilityScores', parseToArray(data.abilityScores), 3, 'abilityCounter');
      buildCheckboxes('choice_savingThrows', parseToArray(data.savingThrows), 2, 'savingCounter');
      buildAllocators('choice_generalSkills', parseToArray(data.generalSkills), 4, 'genPointsCounter');
      buildAllocators('choice_expertSkills', parseToArray(data.expertSkills), 3, 'expPointsCounter');
      bindCalcTriggers();
      calculateSummary();
    }

    // --- THE MASTER CALCULATOR ---
    function calculateSummary() {
      validateArray();
      
      // 1. Gather Final Ability Scores
      const finalStats = {};
      ABILITIES.forEach(stat => finalStats[stat] = parseInt(document.getElementById('arr_' + stat).value) || 0);
      
      // Add Background Boosts
      document.querySelectorAll('#choice_abilityScores input:checked').forEach(cb => {
        if(finalStats[cb.value] !== undefined) finalStats[cb.value] += 1;
      });

      // Render Final Stats
      const statUI = document.getElementById('summary_abilities');
      statUI.innerHTML = '';
      ABILITIES.forEach(stat => {
        statUI.innerHTML += `<div><strong>${stat}:</strong> <span style="float:right; margin-right:20px; color:var(--tertiary); font-weight:bold;">${finalStats[stat] > 0 ? '+'+finalStats[stat] : finalStats[stat]}</span></div>`;
      });

      // 2. Gather Skills & Saves
      const skillMap = {};
      const saves = [];
      
      // Allocators (Background)
      document.querySelectorAll('.bg-alloc').forEach(inp => {
        const val = parseInt(inp.value) || 0;
        const skill = inp.getAttribute('data-skill');
        if (val > 0) skillMap[skill] = (skillMap[skill] || 0) + val;
      });

      // Free Skills
      ['fs_exp1', 'fs_gen1', 'fs_gen2', 'fs_gen3'].forEach(id => {
        const el = document.getElementById(id);
        if (el && el.value) skillMap[el.value] = (skillMap[el.value] || 0) + 1;
      });

      // Saving Throws
      document.querySelectorAll('#choice_savingThrows input:checked').forEach(cb => saves.push(cb.value));

      // Render Skills
      const skillUI = document.getElementById('summary_skills');
      skillUI.innerHTML = Object.entries(skillMap).map(([sk, val]) => `<span style="background:var(--lightgray); padding:2px 6px; border-radius:10px; margin:0 4px 4px 0; display:inline-block;">${sk} (${val})</span>`).join('') 
        + '<br><br><strong>Saves:</strong> ' + (saves.length > 0 ? saves.join(', ') : 'None');

      // 3. Derived Combat Stats
      const tHealth = parseInt(document.getElementById('tal_health').value) || 0;
      const tMana = parseInt(document.getElementById('tal_mana').value) || 0;
      const tStamina = parseInt(document.getElementById('tal_stamina').value) || 0;

      // Variables for math
      const con = finalStats.Constitution;
      const sorc = finalStats.Sorcery;
      const agi = finalStats.Agility;
      const maxStrPre = Math.max(finalStats.Strength, finalStats.Precision);
      
      // Assumption: Rank is 1 for character creation calculation. 
      const rank = 1; 
      const martialSkill = 2 * rank;
      const spellSkill = 2 * rank;

      const combatData = [
        ["Hit Points", 12 + con + tHealth],
        ["Mana", sorc + tMana],
        ["Stamina", 0 + tStamina],
        ["Initiative", agi > 0 ? '+'+agi : agi],
        ["Hit Dice", tHealth],
        ["Armour Class", 8],
        ["Evasion Class", 10 + agi],
        ["Martial Save DC", 8 + martialSkill + maxStrPre],
        ["Spell Save DC", 8 + spellSkill + sorc],
        ["Weapon Attack Mod", `+${martialSkill + maxStrPre}`],
        ["Spell Attack Mod", `+${spellSkill + sorc}`],
        ["Short Rest HP", con > 0 ? '+'+con : con],
        ["Long Rest HP", 7 * con],
        ["Short Rest Mana", sorc > 0 ? '+'+sorc : sorc],
        ["Long Rest Mana", 7 * sorc]
      ];

      const combatUI = document.getElementById('summary_combat');
      combatUI.innerHTML = combatData.map(row => `
        <tr>
          <td style="padding:4px; border-bottom:1px solid var(--lightgray); color:var(--darkgray);"><strong>${row[0]}</strong></td>
          <td style="padding:4px; border-bottom:1px solid var(--lightgray); text-align:right; font-weight:bold; color:var(--dark);">${row[1]}</td>
        </tr>
      `).join('');
    }

    function bindCalcTriggers() {
      document.querySelectorAll('.calc-trigger').forEach(el => {
        el.removeEventListener('change', calculateSummary);
        el.removeEventListener('input', calculateSummary);
        el.addEventListener('change', calculateSummary);
        el.addEventListener('input', calculateSummary);
      });
      // Handle Free Skill Radio swaps specifically
      document.querySelectorAll('input[name="freeSkillMode"]').forEach(radio => {
        radio.addEventListener('change', updateFreeSkillsUI);
      });
    }

    // --- INIT & VAULT HARVESTING ---
    initStandardArray();
    bindCalcTriggers();
    updateFreeSkillsUI();

    const slug = document.body.getAttribute('data-slug') || '';
    const depth = (slug.match(/\//g) || []).length;
    const indexPath = (depth > 0 ? '../'.repeat(depth) : '') + "static/contentIndex.json";

    fetch(indexPath)
      .then(res => res.ok ? res.json() : {})
      .then(data => {
        // Parse whole vault
        for (const [slug, page] of Object.entries(data)) {
          const tags = page.tags || [];
          const title = page.title || slug;
          
          if (tags.includes('ancestry')) {
            window.vaultData.addAncestries.push(title);
            if (tags.includes('common')) window.vaultData.coreAncestries.push(title);
          }
          if (tags.includes('expert_skill')) window.vaultData.expertSkills.push(title);
          if (tags.includes('general_skill')) window.vaultData.generalSkills.push(title);
          
          if (tags.includes('background') && page.content && title !== "Background Template" && title !== "Character Creation Guide") {
            const text = page.content;
            window.vaultData.backgrounds[title] = {
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

        // Populate Dropdowns
        const popSelect = (id, arr) => {
          const el = document.getElementById(id);
          el.innerHTML = '<option value="">-- Select --</option>' + arr.sort().map(i => `<option value="${i}">${i}</option>`).join('');
        };

        popSelect('coreAncestrySelect', window.vaultData.coreAncestries);
        popSelect('addAncestrySelect', window.vaultData.addAncestries);
        popSelect('backgroundSelect', Object.keys(window.vaultData.backgrounds));

        document.getElementById('backgroundSelect').addEventListener('change', updateBackground);
        
        // Rebuild free skills dropdowns now that data is loaded
        updateFreeSkillsUI();
      })
      .catch(e => console.error("Index load failed", e));

  </script>

</div>
