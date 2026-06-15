<div style="padding: 1.5rem; border: 1px solid var(--lightgray); border-radius: 8px; background-color: var(--light); max-width: 650px; font-family: sans-serif;">
  <h3 style="margin-top: 0; margin-bottom: 15px;">Dynamic Background Character Creator</h3>

  <div style="margin-bottom: 20px;">
    <select id="backgroundSelect" style="width: 100%; padding: 8px; border-radius: 4px; background: var(--light); color: var(--dark); border: 1px solid var(--gray); font-size: 1.1em; cursor: pointer; font-weight: bold;">
      <option>Loading backgrounds from system...</option>
    </select>
  </div>

  <div id="backgroundDetails" style="padding: 15px; border-radius: 6px; background-color: rgba(0,0,0,0.02); border: 1px solid var(--lightgray); font-size: 0.95em; margin-bottom: 25px;">
    <p style="margin-top: 0; margin-bottom: 8px;"><strong style="color: var(--darkgray);">Ability Scores:</strong> <span id="bg_abilityScores" style="color: var(--dark);">--</span></p>
    <p style="margin-top: 0; margin-bottom: 8px;"><strong style="color: var(--darkgray);">Saving Throws:</strong> <span id="bg_savingThrows" style="color: var(--dark);">--</span></p>
    <p style="margin-top: 0; margin-bottom: 8px;"><strong style="color: var(--darkgray);">General Skill Ranks:</strong> <span id="bg_generalSkills" style="color: var(--dark);">--</span></p>
    <p style="margin-top: 0; margin-bottom: 8px;"><strong style="color: var(--darkgray);">Expert Skill Ranks:</strong> <span id="bg_expertSkills" style="color: var(--dark);">--</span></p>
    <p style="margin-top: 0; margin-bottom: 8px;"><strong style="color: var(--darkgray);">Talents:</strong> <span id="bg_talents">--</span></p>
    <p style="margin-top: 0; margin-bottom: 8px;"><strong style="color: var(--darkgray);">Equipment:</strong> <span id="bg_equipment" style="color: var(--dark);">--</span></p>
    <p style="margin-top: 0; margin-bottom: 0;"><strong style="color: var(--darkgray);">Initial Wealth:</strong> <span id="bg_wealth" style="color: var(--secondary); font-weight: bold;">--</span></p>
  </div>

  <h4 style="margin-top: 0; border-bottom: 2px solid var(--lightgray); padding-bottom: 5px; color: var(--dark);">Distribute Background Benefits</h4>

  <div style="display: flex; flex-direction: column; gap: 20px; margin-top: 15px;">
    <div style="padding: 12px; border: 1px solid var(--lightgray); border-radius: 6px; background: var(--light);">
      <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px;">
        <strong style="color: var(--darkgray);">1. Ability Scores</strong>
        <span style="font-size: 0.85em; background: var(--tertiary); color: white; padding: 2px 8px; border-radius: 10px;" id="abilityCounter">Select 3 (+1 each)</span>
      </div>
      <div id="choice_abilityScores" style="display: flex; flex-wrap: wrap; gap: 15px;"></div>
    </div>

```
<div style="padding: 12px; border: 1px solid var(--lightgray); border-radius: 6px; background: var(--light);">
  <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px;">
    <strong style="color: var(--darkgray);">2. Saving Throws</strong>
    <span style="font-size: 0.85em; background: var(--tertiary); color: white; padding: 2px 8px; border-radius: 10px;" id="savingCounter">Select 2 (+1 Rank each)</span>
  </div>
  <div id="choice_savingThrows" style="display: flex; flex-wrap: wrap; gap: 15px;"></div>
</div>

<div style="padding: 12px; border: 1px solid var(--lightgray); border-radius: 6px; background: var(--light);">
  <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px;">
    <strong style="color: var(--darkgray);">3. General Skill Ranks</strong>
    <span style="font-size: 0.85em; background: var(--secondary); color: white; padding: 2px 8px; border-radius: 10px;">Ranks Remaining: <span id="genPointsCounter">4</span></span>
  </div>
  <div id="choice_generalSkills" style="display: grid; grid-template-columns: repeat(auto-fill, minmax(180px, 1fr)); gap: 10px;"></div>
</div>

<div style="padding: 12px; border: 1px solid var(--lightgray); border-radius: 6px; background: var(--light);">
  <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px;">
    <strong style="color: var(--darkgray);">4. Expert Skill Ranks</strong>
    <span style="font-size: 0.85em; background: var(--secondary); color: white; padding: 2px 8px; border-radius: 10px;">Ranks Remaining: <span id="expPointsCounter">3</span></span>
  </div>
  <div id="choice_expertSkills" style="display: grid; grid-template-columns: repeat(auto-fill, minmax(180px, 1fr)); gap: 10px;"></div>
</div>
```

  </div>

  <script>
    // Global variable pathing setups
    let relativePrefix = '';

    function parseToArray(commaString) {
      if (!commaString || commaString === "None" || commaString === "--") return [];
      return commaString.split(',').map(s => s.trim()).filter(s => s.length > 0);
    }

    function extractField(text, fieldName) {
      const targetMap = ["Ability Scores", "Saving Throws", "General Skill Ranks", "Expert Skill Ranks", "Talents", "Equipment", "Initial Wealth"];
      const index = text.indexOf(fieldName + ":");
      if (index === -1) return "None";

      let start = index + fieldName.length + 1;
      let remainder = text.substring(start).trim();

      let cutIndex = remainder.length;
      targetMap.forEach(f => {
        const nextFieldPos = remainder.indexOf(f + ":");
        if (nextFieldPos !== -1 && nextFieldPos < cutIndex) {
          cutIndex = nextFieldPos;
        }
      });

      return remainder.substring(0, cutIndex).trim().replace(/[\r\n]+/g, ' ');
    }

    // New Function: Looks through global index data to build valid anchor tag elements
    function generateTalentLinks(talentsString) {
      const talentList = parseToArray(talentsString);
      if (talentList.length === 0) return "--";

      const linkedElements = talentList.map(talentName => {
        if (!window.fullQuartzIndex) return `<span style="color: var(--tertiary); font-weight: bold;">${talentName}</span>`;

        // Scan index looking for a note matching this exact title name string
        const match = Object.entries(window.fullQuartzIndex).find(([slug, pageData]) => {
          return pageData.title && pageData.title.toLowerCase().trim() === talentName.toLowerCase().trim();
        });

        if (match) {
          const targetSlug = match[0];
          return `<a href="${relativePrefix}${targetSlug}" style="color: var(--tertiary); font-weight: bold; text-decoration: underline;">${talentName}</a>`;
        }

        // Return clean fallback text style if talent wiki file isn't created/discovered yet
        return `<span style="color: var(--tertiary); font-weight: bold;">${talentName}</span>`;
      });

      return linkedElements.join(', ');
    }

    function buildCheckboxes(containerId, itemsArray, maxAllowed, counterId) {
      const container = document.getElementById(containerId);
      container.innerHTML = '';
      if(itemsArray.length === 0) {
        container.innerHTML = '<span style="color:var(--darkgray); font-size:0.9em;">No selections available.</span>';
        return;
      }
      itemsArray.forEach((item) => {
        const wrapper = document.createElement('label');
        wrapper.style.cssText = "display: flex; align-items: center; gap: 6px; cursor: pointer; font-size: 0.9em; padding: 4px 8px; border: 1px solid var(--lightgray); border-radius: 4px; background: rgba(0,0,0,0.01);";
        const cb = document.createElement('input');
        cb.type = 'checkbox';
        cb.value = item;
        cb.addEventListener('change', () => {
          const checkedBoxes = container.querySelectorAll('input[type="checkbox"]:checked');
          if (checkedBoxes.length > maxAllowed) cb.checked = false;
          const activeCount = container.querySelectorAll('input[type="checkbox"]:checked').length;
          document.getElementById(counterId).textContent = `Chosen: ${activeCount} / ${maxAllowed}`;
        });
        wrapper.appendChild(cb);
        wrapper.appendChild(document.createTextNode(item));
        container.appendChild(wrapper);
      });
      document.getElementById(counterId).textContent = `Chosen: 0 / ${maxAllowed}`;
    }

    function buildAllocators(containerId, itemsArray, totalPool, counterId) {
      const container = document.getElementById(containerId);
      container.innerHTML = '';
      if(itemsArray.length === 0) {
        container.innerHTML = '<span style="color:var(--darkgray); font-size:0.9em;">No skills available.</span>';
        document.getElementById(counterId).textContent = "0";
        return;
      }
      itemsArray.forEach(item => {
        const row = document.createElement('div');
        row.style.cssText = "display: flex; justify-content: space-between; align-items: center; padding: 4px 8px; border: 1px solid var(--lightgray); border-radius: 4px; background: rgba(0,0,0,0.01); font-size: 0.9em;";
        const label = document.createElement('span');
        label.textContent = item;
        const numInput = document.createElement('input');
        numInput.type = 'number';
        numInput.value = '0';
        numInput.min = '0';
        numInput.max = totalPool.toString();
        numInput.style.cssText = "width: 45px; text-align: center; padding: 2px; border: 1px solid var(--gray); border-radius: 4px;";
        numInput.addEventListener('input', () => {
          let currentAllocated = 0;
          const allInputs = container.querySelectorAll('input[type="number"]');
          allInputs.forEach(inp => currentAllocated += (parseInt(inp.value) || 0));
          if (currentAllocated > totalPool) {
            const overflow = currentAllocated - totalPool;
            numInput.value = (parseInt(numInput.value) || 0) - overflow;
            currentAllocated = totalPool;
          }
          document.getElementById(counterId).textContent = (totalPool - currentAllocated).toString();
        });
        row.appendChild(label);
        row.appendChild(numInput);
        container.appendChild(row);
      });
      document.getElementById(counterId).textContent = totalPool.toString();
    }

    function updateBackground() {
      const selected = document.getElementById('backgroundSelect').value;
      if (!window.allBackgroundData || !window.allBackgroundData[selected]) return;
      
      const data = window.allBackgroundData[selected];

      document.getElementById('bg_abilityScores').textContent = data.abilityScores;
      document.getElementById('bg_savingThrows').textContent = data.savingThrows;
      document.getElementById('bg_generalSkills').textContent = data.generalSkills;
      document.getElementById('bg_expertSkills').textContent = data.expertSkills;
      document.getElementById('bg_equipment').textContent = data.equipment;
      document.getElementById('bg_wealth').textContent = data.wealth;

      // Render the talent string into active HTML links
      document.getElementById('bg_talents').innerHTML = generateTalentLinks(data.talents);

      buildCheckboxes('choice_abilityScores', parseToArray(data.abilityScores), 3, 'abilityCounter');
      buildCheckboxes('choice_savingThrows', parseToArray(data.savingThrows), 2, 'savingCounter');
      buildAllocators('choice_generalSkills', parseToArray(data.generalSkills), 4, 'genPointsCounter');
      buildAllocators('choice_expertSkills', parseToArray(data.expertSkills), 3, 'expPointsCounter');
    }

    const slug = document.body.getAttribute('data-slug') || '';
    const depth = (slug.match(/\//g) || []).length;
    relativePrefix = depth > 0 ? '../'.repeat(depth) : '';
    const indexPath = relativePrefix + "static/contentIndex.json";

    fetch(indexPath)
      .then(res => {
        if (!res.ok) throw new Error("Index error code: " + res.status);
        return res.json();
      })
      .then(data => {
        window.fullQuartzIndex = data; // Store full index data globally for live lookup engine
        const selectEl = document.getElementById('backgroundSelect');
        const backgrounds = {};

        for (const [slug, pageData] of Object.entries(data)) {
          if (pageData.tags && pageData.tags.includes('background') && pageData.content) {
            const title = pageData.title || slug;
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
          selectEl.appendChild(opt);
        });

        window.allBackgroundData = backgrounds;
        updateBackground();
      })
      .catch(err => {
        console.error("Harvesting failed:", err);
        document.getElementById('backgroundSelect').innerHTML = '<option>Error harvesting system data</option>';
      });

    document.getElementById('backgroundSelect').addEventListener('change', updateBackground);
  </script>

</div>
