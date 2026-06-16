<div style="padding: 1.5rem; border: 1px solid var(--lightgray); border-radius: 8px; background-color: var(--light); max-width: 800px; font-family: sans-serif;">
  <h2 style="margin-top: 0; border-bottom: 2px solid var(--tertiary); padding-bottom: 10px; color: var(--dark);">Character Creator</h2>
  <!-- 1. BASE ABILITY SCORES -->
  <div style="margin-bottom: 25px; padding: 15px; border: 1px solid var(--lightgray); border-radius: 6px; background: rgba(0,0,0,0.02);">
    <h3 style="margin-top: 0; margin-bottom: 15px; color: var(--darkgray);">Distribute Ability Scores</h3>
        <p><strong>Standard Array:</strong> +3, +2, +2, +1, +1, +0, -1, -2</p>
    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(140px, 1fr)); gap: 10px;">
      <label style="display:flex; justify-content:space-between; align-items:center; background:var(--light); padding:6px; border:1px solid var(--gray); border-radius:4px;"><span style="font-size:0.9em; font-weight:bold;">Strength</span><input type="number" id="base_attr_Strength" value="0" style="width:45px; text-align:center; border:1px solid var(--gray); border-radius:4px;"></label>
      <label style="display:flex; justify-content:space-between; align-items:center; background:var(--light); padding:6px; border:1px solid var(--gray); border-radius:4px;"><span style="font-size:0.9em; font-weight:bold;">Agility</span><input type="number" id="base_attr_Agility" value="0" style="width:45px; text-align:center; border:1px solid var(--gray); border-radius:4px;"></label>
      <label style="display:flex; justify-content:space-between; align-items:center; background:var(--light); padding:6px; border:1px solid var(--gray); border-radius:4px;"><span style="font-size:0.9em; font-weight:bold;">Precision</span><input type="number" id="base_attr_Precision" value="0" style="width:45px; text-align:center; border:1px solid var(--gray); border-radius:4px;"></label>
      <label style="display:flex; justify-content:space-between; align-items:center; background:var(--light); padding:6px; border:1px solid var(--gray); border-radius:4px;"><span style="font-size:0.9em; font-weight:bold;">Constitution</span><input type="number" id="base_attr_Constitution" value="0" style="width:45px; text-align:center; border:1px solid var(--gray); border-radius:4px;"></label>
      <label style="display:flex; justify-content:space-between; align-items:center; background:var(--light); padding:6px; border:1px solid var(--gray); border-radius:4px;"><span style="font-size:0.9em; font-weight:bold;">Awareness</span><input type="number" id="base_attr_Awareness" value="0" style="width:45px; text-align:center; border:1px solid var(--gray); border-radius:4px;"></label>
      <label style="display:flex; justify-content:space-between; align-items:center; background:var(--light); padding:6px; border:1px solid var(--gray); border-radius:4px;"><span style="font-size:0.9em; font-weight:bold;">Charisma</span><input type="number" id="base_attr_Charisma" value="0" style="width:45px; text-align:center; border:1px solid var(--gray); border-radius:4px;"></label>
      <label style="display:flex; justify-content:space-between; align-items:center; background:var(--light); padding:6px; border:1px solid var(--gray); border-radius:4px;"><span style="font-size:0.9em; font-weight:bold;">Intelligence</span><input type="number" id="base_attr_Intelligence" value="0" style="width:45px; text-align:center; border:1px solid var(--gray); border-radius:4px;"></label>
      <label style="display:flex; justify-content:space-between; align-items:center; background:var(--light); padding:6px; border:1px solid var(--gray); border-radius:4px;"><span style="font-size:0.9em; font-weight:bold;">Sorcery</span><input type="number" id="base_attr_Sorcery" value="0" style="width:45px; text-align:center; border:1px solid var(--gray); border-radius:4px;"></label>
    </div>
  </div>
  <!-- 2. ANCESTRY -->
  <div style="margin-bottom: 25px; padding: 15px; border: 1px solid var(--lightgray); border-radius: 6px; background: rgba(0,0,0,0.02);">
    <div style="display: flex; gap: 15px; flex-wrap: wrap;">
      <div style="flex: 1; min-width: 250px;">
        <h3 style="margin-top: 0; margin-bottom: 10px; color: var(--darkgray);">Select Core Ancestry</h3>
        <select id="coreAncestrySelect" style="width: 100%; padding: 8px; border-radius: 4px; border: 1px solid var(--gray); font-size: 1em;"><option value="">Loading system data...</option></select>
      </div>
      <div style="flex: 1; min-width: 250px;">
        <h3 style="margin-top: 0; margin-bottom: 10px; color: var(--darkgray);">Select Additional Ancestry</h3>
        <select id="addAncestrySelect" style="width: 100%; padding: 8px; border-radius: 4px; border: 1px solid var(--gray); font-size: 1em;"><option value="">No Additional Ancestry</option></select>
      </div>
    </div>
  </div>
  <!-- 3. BACKGROUND -->
  <div style="margin-bottom: 25px; padding: 15px; border: 1px solid var(--lightgray); border-radius: 6px; background: rgba(0,0,0,0.02);">
    <h3 style="margin-top: 0; margin-bottom: 10px; color: var(--darkgray);">Select Background</h3>
    <select id="backgroundSelect" style="width: 100%; padding: 8px; border-radius: 4px; border: 1px solid var(--gray); font-size: 1.05em; font-weight: bold; margin-bottom: 15px;"><option value="">-- Please choose an option --</option></select>
    <div id="backgroundContainer" style="display: none; flex-direction: column; gap: 15px;">
      <div style="padding: 10px; border: 1px solid var(--lightgray); border-radius: 6px; background: var(--light);">
        <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px;">
          <strong style="color: var(--darkgray); font-size: 0.95em;">Background's Ability Score Improvements</strong>
          <span style="font-size: 0.8em; background: var(--tertiary); color: white; padding: 2px 8px; border-radius: 10px;" id="bg_abilityCounter">Select 3 (+1 each)</span>
        </div>
        <div id="bg_choice_abilityScores" style="display: flex; flex-wrap: wrap; gap: 10px;"></div>
      </div>
      <div style="padding: 10px; border: 1px solid var(--lightgray); border-radius: 6px; background: var(--light);">
        <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px;">
          <strong style="color: var(--darkgray); font-size: 0.95em;">Background's Saving Throw Improvements</strong>
          <span style="font-size: 0.8em; background: var(--tertiary); color: white; padding: 2px 8px; border-radius: 10px;" id="bg_savingCounter">Select 2 (+1 each)</span>
        </div>
        <div id="bg_choice_savingThrows" style="display: flex; flex-wrap: wrap; gap: 10px;"></div>
      </div>
      <div style="padding: 10px; border: 1px solid var(--lightgray); border-radius: 6px; background: var(--light);">
        <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px;">
          <strong style="color: var(--darkgray); font-size: 0.95em;">Background's General Skill Improvements</strong>
          <span style="font-size: 0.8em; background: var(--secondary); color: white; padding: 2px 8px; border-radius: 10px;">Ranks Remaining: <span id="bg_genPointsCounter">4</span></span>
        </div>
        <div id="bg_choice_generalSkills" style="display: grid; grid-template-columns: repeat(auto-fill, minmax(180px, 1fr)); gap: 10px;"></div>
      </div>
      <div style="padding: 10px; border: 1px solid var(--lightgray); border-radius: 6px; background: var(--light);">
        <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px;">
          <strong style="color: var(--darkgray); font-size: 0.95em;">Background's Expert Skill Improvements</strong>
          <span style="font-size: 0.8em; background: var(--secondary); color: white; padding: 2px 8px; border-radius: 10px;">Ranks Remaining: <span id="bg_expPointsCounter">3</span></span>
        </div>
        <div id="bg_choice_expertSkills" style="display: grid; grid-template-columns: repeat(auto-fill, minmax(180px, 1fr)); gap: 10px;"></div>
      </div>
    </div>
  </div>
  <!-- 4. FREE SKILLS -->
  <div style="margin-bottom: 25px; padding: 15px; border: 1px solid var(--lightgray); border-radius: 6px; background: rgba(0,0,0,0.02);">
    <h3 style="margin-top: 0; margin-bottom: 15px; color: var(--darkgray);">Select Free Skills</h3>
    <div style="margin-bottom: 20px; display: flex; gap: 20px;">
      <label style="cursor: pointer; font-weight: bold; font-size: 0.95em;"><input type="radio" name="freeSkillMode" value="3gen" checked style="cursor: pointer;"> 3 General Skill Ranks</label>
      <label style="cursor: pointer; font-weight: bold; font-size: 0.95em;"><input type="radio" name="freeSkillMode" value="1gen1exp" style="cursor: pointer;"> 1 General & 1 Expert Skill Rank</label>
    </div>
    <div style="display: flex; flex-direction: column; gap: 15px;">
      <div style="padding: 10px; border: 1px solid var(--lightgray); border-radius: 6px; background: var(--light);">
        <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px;">
          <strong style="color: var(--darkgray); font-size: 0.95em;">General Skills <span style="font-weight:normal; font-size:0.85em; color:var(--gray);">(All #general_skill)</span></strong>
          <span style="font-size: 0.8em; background: var(--secondary); color: white; padding: 2px 8px; border-radius: 10px;">Ranks Remaining: <span id="free_genPointsCounter">3</span></span>
        </div>
        <div id="free_generalSkills" style="display: grid; grid-template-columns: repeat(auto-fill, minmax(180px, 1fr)); gap: 10px; max-height: 250px; overflow-y: auto; padding-right: 5px;"></div>
      </div>
      <div id="free_expertSkills_container" style="padding: 10px; border: 1px solid var(--lightgray); border-radius: 6px; background: var(--light); display: none;">
        <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px;">
          <strong style="color: var(--darkgray); font-size: 0.95em;">Expert Skills <span style="font-weight:normal; font-size:0.85em; color:var(--gray);">(All #expert_skill)</span></strong>
          <span style="font-size: 0.8em; background: var(--secondary); color: white; padding: 2px 8px; border-radius: 10px;">Ranks Remaining: <span id="free_expPointsCounter">1</span></span>
        </div>
        <div id="free_expertSkills" style="display: grid; grid-template-columns: repeat(auto-fill, minmax(180px, 1fr)); gap: 10px; max-height: 250px; overflow-y: auto; padding-right: 5px;"></div>
      </div>
    </div>
  </div>
  <!-- 5. LIVE SUMMARY DASHBOARD -->
  <div style="padding: 20px; border: 2px solid var(--tertiary); border-radius: 8px; background: var(--light);">
    <h3 style="margin-top:0; border-bottom:1px solid var(--lightgray); padding-bottom:8px; color:var(--dark);">Character Summary</h3>
    <h4 style="margin: 15px 0 8px 0; color:var(--darkgray);">Ability Score Computations</h4>
    <table style="width:100%; border-collapse:collapse; font-size:0.9em; text-align:left; margin-bottom:20px;">
      <thead>
        <tr style="background:rgba(0,0,0,0.04); border-bottom:2px solid var(--lightgray);">
          <th style="padding:8px;">Ability</th>
          <th style="padding:8px; text-align:center;">Base</th>
          <th style="padding:8px; text-align:center;">Ancestry</th>
          <th style="padding:8px; text-align:center;">Background</th>
          <th style="padding:8px; text-align:center; font-weight:bold; color:var(--tertiary);">Total</th>
        </tr>
      </thead>
      <tbody id="summary_ability_rows"></tbody>
    </table>
    <h4 style="margin: 15px 0 8px 0; color:var(--darkgray);">General Skills</h4>
    <div id="summary_general_skills" style="margin-bottom:20px; width:100%; overflow-x:auto;"></div>
    <h4 style="margin: 15px 0 8px 0; color:var(--darkgray);">Expert Skills</h4>
    <div id="summary_expert_skills" style="width:100%; overflow-x:auto;"></div>
  </div>

  <script>
    window.charData = {
      coreAncestries: [], addAncestries: [], backgrounds: {}, generalSkills: [], expertSkills: [], skillModifiers: {}
    };
    const attributesMasterList = ["Strength", "Agility", "Precision", "Constitution", "Awareness", "Charisma", "Intelligence", "Sorcery"];

    function parseToArray(commaString) {
      if (!commaString || commaString === "None" || commaString === "--") return [];
      return commaString.split(',').map(s => s.trim()).filter(s => s.length > 0);
    }

    function checkTag(tagsArr, targetTag) {
      if (!tagsArr) return false;
      return tagsArr.some(t => t.toLowerCase() === targetTag.toLowerCase());
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
        if (nextFieldPos !== -1 && nextFieldPos < cutIndex) cutIndex = nextFieldPos;
      });
      return remainder.substring(0, cutIndex).trim().replace(/[\r\n]+/g, ' ');
    }

    function buildCheckboxes(containerId, itemsArray, maxAllowed, counterId) {
      const container = document.getElementById(containerId);
      container.innerHTML = '';
      if(itemsArray.length === 0) {
        container.innerHTML = '<span style="color:var(--darkgray); font-size:0.9em;">No selections available.</span>';
        document.getElementById(counterId).textContent = `Chosen: 0 / ${maxAllowed}`;
        return;
      }
      itemsArray.forEach((item) => {
        const wrapper = document.createElement('label');
        wrapper.style.cssText = "display: flex; align-items: center; gap: 6px; cursor: pointer; font-size: 0.9em; padding: 4px 8px; border: 1px solid var(--lightgray); border-radius: 4px; background: rgba(0,0,0,0.01);";
        const cb = document.createElement('input');
        cb.type = 'checkbox';
        cb.value = item;
        cb.className = "cb-node-" + containerId;
        cb.style.cursor = 'pointer';
        cb.addEventListener('change', () => {
          const checkedBoxes = container.querySelectorAll('input[type="checkbox"]:checked');
          if (checkedBoxes.length > maxAllowed) cb.checked = false; 
          const activeCount = container.querySelectorAll('input[type="checkbox"]:checked').length;
          document.getElementById(counterId).textContent = `Chosen: ${activeCount} / ${maxAllowed}`;
          updateSummaryDashboard();
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
        label.style.cssText = "overflow: hidden; text-overflow: ellipsis; white-space: nowrap; margin-right: 5px;";
        const numInput = document.createElement('input');
        numInput.type = 'number';
        numInput.value = '0';
        numInput.min = '0';
        numInput.max = totalPool.toString();
        numInput.className = "alloc-node-" + containerId;
        numInput.setAttribute("data-skill-target", item);
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
          updateSummaryDashboard();
        });
        row.appendChild(label);
        row.appendChild(numInput);
        container.appendChild(row);
      });
      document.getElementById(counterId).textContent = totalPool.toString();
    }

    function updateSummaryDashboard() {
      let totalsMap = {};
      let calculatedTableHTML = "";
      
      attributesMasterList.forEach(attr => {
        let baseVal = parseInt(document.getElementById("base_attr_" + attr).value) || 0;
        let ancestryVal = 0;
        let coreChoice = document.getElementById("coreAncestrySelect").value;
        let addChoice = document.getElementById("addAncestrySelect").value;
        
        if (coreChoice === "Halfling") {
          if (attr === "Agility") ancestryVal += 2;
          if (attr === "Strength") ancestryVal -= 2;
          if (attr === "Precision") ancestryVal += 1;
          if (attr === "Constitution") ancestryVal -= 1;
        }
        if (addChoice === "Giant") {
          if (attr === "Agility") ancestryVal -= 2;
          if (attr === "Strength") ancestryVal += 2;
          if (attr === "Precision") ancestryVal -= 1;
          if (attr === "Constitution") ancestryVal += 1;
        }

        let bgVal = 0;
        const checkedBgAttrs = document.querySelectorAll("#bg_choice_abilityScores input[type='checkbox']:checked");
        checkedBgAttrs.forEach(cb => { if(cb.value === attr) bgVal += 1; });

        let finalTotal = baseVal + ancestryVal + bgVal;
        totalsMap[attr] = finalTotal;

        calculatedTableHTML += `<tr style="border-bottom:1px solid var(--lightgray);">
          <td style="padding:6px; font-weight:bold;">${attr}</td>
          <td style="padding:6px; text-align:center;">${baseVal}</td>
          <td style="padding:6px; text-align:center; color:${ancestryVal >= 0 ? 'green':'red'};">${ancestryVal >= 0 ? '+' : ''}${ancestryVal}</td>
          <td style="padding:6px; text-align:center; color:green;">+${bgVal}</td>
          <td style="padding:6px; text-align:center; font-weight:bold; color:var(--tertiary); background:rgba(0,0,0,0.01);">${finalTotal}</td>
        </tr>`;
      });
      document.getElementById("summary_ability_rows").innerHTML = calculatedTableHTML;

      const getSkillRank = (containerId, name) => {
        let matchedInput = document.querySelector(`#${containerId} input[data-skill-target="${name}"]`);
        return matchedInput ? (parseInt(matchedInput.value) || 0) : 0;
      };

      // General Skills Table
      let genTableStart = `<table style="width:100%; border-collapse:collapse; font-size:0.9em; text-align:left;">
        <thead>
          <tr style="background:rgba(0,0,0,0.04); border-bottom:2px solid var(--lightgray);">
            <th style="padding:8px;">General Skill</th>
            <th style="padding:8px; text-align:center;">Rank</th>
            <th style="padding:8px; text-align:center;">Ability Score</th>
            <th style="padding:8px; text-align:center;">Total Modifier</th>
          </tr>
        </thead>
        <tbody>`;
      let genRows = "";
      window.charData.generalSkills.forEach(skill => {
        let rBg = getSkillRank("bg_choice_generalSkills", skill);
        let rFree = getSkillRank("free_generalSkills", skill);
        let totalRank = rBg + rFree;
        let linkedAttr = window.charData.skillModifiers[skill] || "Strength";
        let attrScoreValue = totalsMap[linkedAttr] || 0;
        let grandModifier = (2 * totalRank) + attrScoreValue;

        genRows += `<tr style="border-bottom:1px solid var(--lightgray);">
          <td style="padding:6px; font-weight:bold;">${skill}</td>
          <td style="padding:6px; text-align:center;">${totalRank} <span style="font-size:0.85em; color:var(--gray); font-weight:normal;">(${rBg} bg / ${rFree} free)</span></td>
          <td style="padding:6px; text-align:center;">${linkedAttr} (${attrScoreValue})</td>
          <td style="padding:6px; text-align:center; font-weight:bold; color:var(--secondary); font-size:1.05em;">${grandModifier >= 0 ? '+':''}${grandModifier}</td>
        </tr>`;
      });
      let genTableEnd = `</tbody></table>`;
      document.getElementById("summary_general_skills").innerHTML = genRows ? (genTableStart + genRows + genTableEnd) : '<span style="color:var(--gray); font-size:0.9em;">No general skills available.</span>';

      // Expert Skills Table
      let expTableStart = `<table style="width:100%; border-collapse:collapse; font-size:0.9em; text-align:left;">
        <thead>
          <tr style="background:rgba(0,0,0,0.04); border-bottom:2px solid var(--lightgray);">
            <th style="padding:8px;">Expert Skill</th>
            <th style="padding:8px; text-align:center;">Rank</th>
            <th style="padding:8px; text-align:center;">Total Modifier</th>
          </tr>
        </thead>
        <tbody>`;
      let expRows = "";
      window.charData.expertSkills.forEach(skill => {
        let rBg = getSkillRank("bg_choice_expertSkills", skill);
        let rFree = getSkillRank("free_expertSkills", skill);
        let totalRank = rBg + rFree;

        if (totalRank > 0) {
          let grandModifier = 2 * totalRank;
          expRows += `<tr style="border-bottom:1px solid var(--lightgray);">
            <td style="padding:6px; font-weight:bold;">${skill}</td>
            <td style="padding:6px; text-align:center;">${totalRank} <span style="font-size:0.85em; color:var(--gray); font-weight:normal;">(${rBg} bg / ${rFree} free)</span></td>
            <td style="padding:6px; text-align:center; font-weight:bold; color:var(--secondary); font-size:1.05em;">+${grandModifier}</td>
          </tr>`;
        }
      });
      let expTableEnd = `</tbody></table>`;
      document.getElementById("summary_expert_skills").innerHTML = expRows ? (expTableStart + expRows + expTableEnd) : '<span style="color:var(--gray); font-size:0.9em; padding:8px; display:inline-block;">No expert skills trained yet (Rank > 0 required).</span>';
    }

    function updateBackgroundFields() {
      const selected = document.getElementById('backgroundSelect').value;
      const bgContainer = document.getElementById('backgroundContainer');
      if (!selected || !window.charData.backgrounds[selected]) {
        bgContainer.style.display = 'none';
        updateSummaryDashboard();
        return;
      }
      bgContainer.style.display = 'flex';
      const data = window.charData.backgrounds[selected];
      buildCheckboxes('bg_choice_abilityScores', parseToArray(data.abilityScores), 3, 'bg_abilityCounter');
      buildCheckboxes('bg_choice_savingThrows', parseToArray(data.savingThrows), 2, 'bg_savingCounter');
      buildAllocators('bg_choice_generalSkills', parseToArray(data.generalSkills), 4, 'bg_genPointsCounter');
      buildAllocators('bg_choice_expertSkills', parseToArray(data.expertSkills), 3, 'bg_expPointsCounter');
      updateSummaryDashboard();
    }

    function updateFreeSkills() {
      const mode = document.querySelector('input[name="freeSkillMode"]:checked').value;
      const expContainer = document.getElementById('free_expertSkills_container');
      if (mode === '3gen') {
        buildAllocators('free_generalSkills', window.charData.generalSkills, 3, 'free_genPointsCounter');
        expContainer.style.display = 'none'; 
      } else if (mode === '1gen1exp') {
        buildAllocators('free_generalSkills', window.charData.generalSkills, 1, 'free_genPointsCounter');
        buildAllocators('free_expertSkills', window.charData.expertSkills, 1, 'free_expPointsCounter');
        expContainer.style.display = 'block'; 
      }
      updateSummaryDashboard();
    }

    attributesMasterList.forEach(attr => {
      document.getElementById("base_attr_" + attr).addEventListener("input", updateSummaryDashboard);
    });
    document.getElementById("coreAncestrySelect").addEventListener("change", updateSummaryDashboard);
    document.getElementById("addAncestrySelect").addEventListener("change", updateSummaryDashboard);
    document.querySelectorAll('input[name="freeSkillMode"]').forEach(radio => {
      radio.addEventListener('change', updateFreeSkills);
    });
    document.getElementById('backgroundSelect').addEventListener('change', updateBackgroundFields);

    async function loadIndexData() {
      const pathsToTry = ["static/contentIndex.json", "../static/contentIndex.json", "../../static/contentIndex.json", "../../../static/contentIndex.json", "/static/contentIndex.json"];
      for (let path of pathsToTry) {
        try {
          const res = await fetch(path);
          if (res.ok) return await res.json();
        } catch (e) {}
      }
      throw new Error("Could not locate contentIndex.json.");
    }

    loadIndexData().then(data => {
      for (const [slug, pageData] of Object.entries(data)) {
        const tags = pageData.tags || [];
        const title = pageData.title || slug;
        
        if (checkTag(tags, 'ancestry')) {
          if (checkTag(tags, 'common')) window.charData.coreAncestries.push(title);
          if (checkTag(tags, 'common')) window.charData.addAncestries.push(title);
          if (checkTag(tags, 'rare')) window.charData.addAncestries.push(title);
        }
        if (checkTag(tags, 'general_skill')) {
          window.charData.generalSkills.push(title);
          let detectedAttr = "Strength";
          if (pageData.content) {
            let modMatch = pageData.content.match(/Modifier::\s*([A-Za-z]+)/i);
            if (modMatch) {
              let parsedAttr = modMatch[1].trim();
              let matchedLabel = attributesMasterList.find(a => a.toLowerCase() === parsedAttr.toLowerCase());
              if (matchedLabel) detectedAttr = matchedLabel;
            }
          }
          window.charData.skillModifiers[title] = detectedAttr;
        }
        if (checkTag(tags, 'expert_skill')) {
          window.charData.expertSkills.push(title);
        }
        if (checkTag(tags, 'background') && pageData.content) {
          if (title === "Background Template" || title === "Character Creation Guide") continue;
          const text = pageData.content;
          window.charData.backgrounds[title] = {
            abilityScores: extractField(text, "Ability Scores"),
            savingThrows: extractField(text, "Saving Throws"),
            generalSkills: extractField(text, "General Skill Ranks"),
            expertSkills: extractField(text, "Expert Skill Ranks"),
          };
        }
      }

      window.charData.coreAncestries.sort();
      window.charData.addAncestries.sort();
      window.charData.generalSkills.sort();
      window.charData.expertSkills.sort();
      const sortedBackgrounds = Object.keys(window.charData.backgrounds).sort();

      const popSelect = (id, arr, defaultText) => {
        const el = document.getElementById(id);
        el.innerHTML = `<option value="">${defaultText}</option>` + arr.map(i => `<option value="${i}">${i}</option>`).join('');
      };

      popSelect('coreAncestrySelect', window.charData.coreAncestries, '-- Please choose an option --');
      popSelect('addAncestrySelect', window.charData.addAncestries, 'No Additional Ancestry');
      popSelect('backgroundSelect', sortedBackgrounds, '-- Please choose an option --');

      updateFreeSkills();
      updateBackgroundFields();
    }).catch(err => {
      console.error("Harvesting error: ", err);
      document.getElementById('coreAncestrySelect').innerHTML = '<option>Error loading data</option>';
      document.getElementById('addAncestrySelect').innerHTML = '<option>Error loading data</option>';
      document.getElementById('backgroundSelect').innerHTML = '<option>Error loading data</option>';
    });
  </script>

</div>
