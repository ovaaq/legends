<script>
    // --- CORE DATA CONFIG ---
    const ABILITIES = ["Strength", "Agility", "Precision", "Constitution", "Awareness", "Charisma", "Intelligence", "Sorcery"];
    const REQUIRED_ARRAY = [3, 2, 2, 1, 1, 0, -1, -2].sort();
    
    window.vaultData = {
      backgrounds: {},
      coreAncestries: [],
      addAncestries: [],
      generalSkills: [],
      expertSkills: []
    };

    // --- UI GENERATORS & HANDLERS ---
    function initStandardArray() {
      const container = document.getElementById('standardArrayInputs');
      ABILITIES.forEach(stat => {
        const div = document.createElement('div');
        div.innerHTML = `<label style="font-size: 0.85em; font-weight: bold; color: var(--darkgray); display:block;">${stat}</label>
                         <input type="number" id="arr_${stat}" class="calc-trigger arr-input" value="0" style="width:100%; padding:4px; border:1px solid var(--gray); border-radius:4px;">`;
        container.appendChild(div);
      });
    }

    function validateArray() {
      const inputs = Array.from(document.querySelectorAll('.arr-input')).map(i => parseInt(i.value) || 0).sort();
      const isValid = JSON.stringify(inputs) === JSON.stringify(REQUIRED_ARRAY);
      const warning = document.getElementById('arrayWarning');
      warning.textContent = isValid ? "" : "Warning: Values do not match standard array (+3, +2, +2, +1, +1, +0, -1, -2)";
    }

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
      bindCalcTriggers();
      calculateSummary();
    }

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

    function calculateSummary() {
      validateArray();
      
      const finalStats = {};
      ABILITIES.forEach(stat => finalStats[stat] = parseInt(document.getElementById('arr_' + stat).value) || 0);
      
      document.querySelectorAll('#choice_abilityScores input:checked').forEach(cb => {
        if(finalStats[cb.value] !== undefined) finalStats[cb.value] += 1;
      });

      const statUI = document.getElementById('summary_abilities');
      statUI.innerHTML = '';
      ABILITIES.forEach(stat => {
        statUI.innerHTML += `<div><strong>${stat}:</strong> <span style="float:right; margin-right:20px; color:var(--tertiary); font-weight:bold;">${finalStats[stat] > 0 ? '+'+finalStats[stat] : finalStats[stat]}</span></div>`;
      });

      const skillMap = {};
      const saves = [];
      
      document.querySelectorAll('.bg-alloc').forEach(inp => {
        const val = parseInt(inp.value) || 0;
        const skill = inp.getAttribute('data-skill');
        if (val > 0) skillMap[skill] = (skillMap[skill] || 0) + val;
      });

      ['fs_exp1', 'fs_gen1', 'fs_gen2', 'fs_gen3'].forEach(id => {
        const el = document.getElementById(id);
        if (el && el.value) skillMap[el.value] = (skillMap[el.value] || 0) + 1;
      });

      document.querySelectorAll('#choice_savingThrows input:checked').forEach(cb => saves.push(cb.value));

      const skillUI = document.getElementById('summary_skills');
      skillUI.innerHTML = Object.entries(skillMap).map(([sk, val]) => `<span style="background:var(--lightgray); padding:2px 6px; border-radius:10px; margin:0 4px 4px 0; display:inline-block;">${sk} (${val})</span>`).join('') 
        + '<br><br><strong>Saves:</strong> ' + (saves.length > 0 ? saves.join(', ') : 'None');

      const tHealth = parseInt(document.getElementById('tal_health').value) || 0;
      const tMana = parseInt(document.getElementById('tal_mana').value) || 0;
      const tStamina = parseInt(document.getElementById('tal_stamina').value) || 0;

      const con = finalStats.Constitution;
      const sorc = finalStats.Sorcery;
      const agi = finalStats.Agility;
      const maxStrPre = Math.max(finalStats.Strength, finalStats.Precision);
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
      document.querySelectorAll('input[name="freeSkillMode"]').forEach(radio => {
        radio.addEventListener('change', updateFreeSkillsUI);
      });
    }

    // --- BULLETPROOF TAG MATCHER ---
    // This checks tags regardless of uppercase, lowercase, or whether they have a "#" attached.
    function checkTag(tagsArray, targetTag) {
      if (!tagsArray) return false;
      return tagsArray.some(t => t.toLowerCase().replace('#', '') === targetTag.toLowerCase());
    }

    // --- DIAGNOSTIC UI GENERATOR ---
    function printDebug(msg, isError = false) {
      let debugBox = document.getElementById('debug_output');
      if (!debugBox) {
        debugBox = document.createElement('div');
        debugBox.id = 'debug_output';
        debugBox.style.cssText = "margin-bottom: 20px; padding: 10px; background: #1e1e1e; color: #00ff00; font-family: monospace; font-size: 0.85em; border-radius: 6px; border: 1px solid #444; max-height: 200px; overflow-y: auto;";
        document.querySelector('h2').insertAdjacentElement('afterend', debugBox);
      }
      const line = document.createElement('div');
      line.style.color = isError ? '#ff5555' : '#00ff00';
      line.textContent = `> ${msg}`;
      debugBox.appendChild(line);
    }

    // --- INIT & VAULT HARVESTING ---
    initStandardArray();
    bindCalcTriggers();
    updateFreeSkillsUI();

    // Try a direct absolute path first (most reliable for Quartz root deployments)
    const absoluteIndexPath = "/static/contentIndex.json";
    
    // Fallback relative path just in case
    const slug = document.body.getAttribute('data-slug') || '';
    const depth = (slug.match(/\//g) || []).length;
    const relativeIndexPath = (depth > 0 ? '../'.repeat(depth) : '') + "static/contentIndex.json";

    printDebug(`Starting Data Harvest...`);
    printDebug(`Attempting to fetch index from: ${absoluteIndexPath}`);

    // Fetch Execution
    fetch(absoluteIndexPath)
      .then(res => {
        if (!res.ok) {
          printDebug(`Absolute path failed (${res.status}). Trying relative: ${relativeIndexPath}`, true);
          return fetch(relativeIndexPath);
        }
        return res;
      })
      .then(res => {
        if (!res.ok) throw new Error(`HTTP Error: ${res.status}`);
        return res.json();
      })
      .then(data => {
        const pages = Object.entries(data);
        printDebug(`SUCCESS: Downloaded Quartz Index. Found ${pages.length} total pages in vault.`);
        
        let foundAnyBackgrounds = false;

        for (const [pageSlug, page] of pages) {
          const tags = page.tags || [];
          const title = page.title || pageSlug;
          
          if (checkTag(tags, 'ancestry')) {
            window.vaultData.addAncestries.push(title);
            if (checkTag(tags, 'common')) window.vaultData.coreAncestries.push(title);
          }
          if (checkTag(tags, 'expert_skill')) window.vaultData.expertSkills.push(title);
          if (checkTag(tags, 'general_skill')) window.vaultData.generalSkills.push(title);
          
          if (checkTag(tags, 'background') && title !== "Background Template" && title !== "Character Creation Guide") {
            foundAnyBackgrounds = true;
            if (!page.content) {
               printDebug(`WARNING: Found background "${title}", but Quartz did not provide the text content. Check quartz.config.ts`, true);
               continue;
            }
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

        printDebug(`Harvest Complete: ${window.vaultData.coreAncestries.length} Core Ancestries, ${window.vaultData.addAncestries.length} Add. Ancestries, ${Object.keys(window.vaultData.backgrounds).length} Backgrounds, ${window.vaultData.generalSkills.length} Gen Skills, ${window.vaultData.expertSkills.length} Exp Skills.`);

        if (!foundAnyBackgrounds) printDebug("CRITICAL: Found 0 backgrounds. Ensure your files have the '#background' tag.", true);

        // Populate Dropdowns
        const popSelect = (id, arr) => {
          const el = document.getElementById(id);
          el.innerHTML = '<option value="">-- Select --</option>' + arr.sort().map(i => `<option value="${i}">${i}</option>`).join('');
        };

        popSelect('coreAncestrySelect', window.vaultData.coreAncestries);
        popSelect('addAncestrySelect', window.vaultData.addAncestries);
        popSelect('backgroundSelect', Object.keys(window.vaultData.backgrounds));

        document.getElementById('backgroundSelect').addEventListener('change', updateBackground);
        updateFreeSkillsUI();
      })
      .catch(e => {
        printDebug(`FATAL ERROR: Could not load index file. Are you running this via 'npx quartz build --serve'?`, true);
        printDebug(e.toString(), true);
      });

  </script>
