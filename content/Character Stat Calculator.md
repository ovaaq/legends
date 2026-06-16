```dataviewjs
// 1. DATA SETUP
const stats = ["Strength", "Agility", "Precision", "Constitution", "Awareness", "Charisma", "Intelligence", "Sorcery"];

const coreAncestryPages = Array.from(dv.pages("#ancestry and #common")).sort((a,b) => a.file.name.localeCompare(b.file.name));
const addAncestryPages = Array.from(dv.pages("#ancestry and (#common or #rare)")).sort((a,b) => a.file.name.localeCompare(b.file.name));
const bgPages = Array.from(dv.pages("#background")).sort((a,b) => a.file.name.localeCompare(b.file.name));

// 2. HELPER TO BUILD DROPDOWN MENUS
function buildDropdown(id, label, pages, usePathForValue = false) {
    let selectHtml = `
    <div style="margin-bottom: 15px;">
        <label for="${id}" style="display: block; margin-bottom: 5px; font-weight: bold;">${label}</label>
        <select id="${id}" name="${id}" style="width: 100%; max-width: 400px; padding: 8px; border-radius: 4px; background: var(--background-primary);">
            <option value="" disabled selected>-- Choose an option --</option>`;
    
    for (let p of pages) { 
        let val = usePathForValue ? p.file.path : p.file.name;
        selectHtml += `<option value="${val}">${p.file.name}</option>`; 
    }
    return selectHtml + `</select></div>`;
}

// 3. CONSTRUCT THE HTML STRING
let htmlContent = `
<style>
    .char-section { margin-bottom: 30px; }
    .char-section h3 { border-bottom: 1px solid var(--background-modifier-border); padding-bottom: 5px; }
    .selectable-btn {
        display: inline-block;
        border: 2px solid var(--background-modifier-border);
        background-color: var(--background-secondary);
        color: var(--text-normal);
        padding: 8px 12px;
        margin: 4px;
        border-radius: 6px;
        cursor: pointer;
        transition: all 0.2s ease;
        user-select: none;
    }
    .selectable-btn:hover { background-color: var(--background-modifier-hover); }
    .selectable-btn.selected { border-color: #e53935 !important; background-color: var(--background-primary-alt); }
    .selectable-btn input[type="checkbox"] { display: none; }
    .skill-row { display: flex; justify-content: space-between; align-items: center; max-width: 300px; margin-bottom: 8px; padding: 4px 8px; background: var(--background-secondary); border-radius: 4px; }
    .skill-row input { width: 60px; text-align: center; }
</style>

<div class="obsidian-character-builder" id="char-builder-root">
    <div class="char-section">
        <h3>Attribute Distribution</h3>
        <table style="width: 100%; max-width: 300px;">
            <thead><tr><th style="text-align: left;">Attribute</th><th style="text-align: right;">Score</th></tr></thead>
            <tbody>
`;

stats.forEach(stat => {
    htmlContent += `<tr>
        <td><strong>${stat}</strong></td>
        <td style="text-align: right;"><input type="number" id="stat-${stat.toLowerCase()}" value="10" style="width: 70px;"></td>
    </tr>`;
});

htmlContent += `
            </tbody>
        </table>
    </div>
    
    <div class="char-section">
        <h3>Ancestry</h3>
        ${buildDropdown("core-ancestry", "Select Core Ancestry", coreAncestryPages)}
        ${buildDropdown("add-ancestry", "Select Additional Ancestry", addAncestryPages)}
    </div>
    
    <div class="char-section">
        <h3>Background</h3>
        ${buildDropdown("background-select", "Select Background", bgPages, true)}
        <div id="dynamic-bg-content" style="margin-top: 20px; padding: 15px; border: 1px solid var(--background-modifier-border); border-radius: 8px; display: none;"></div>
    </div>
</div>`;

// 4. RENDER TO OBSIDIAN
dv.container.innerHTML = htmlContent;

// 5. INTERACTIVE LOGIC
setTimeout(() => {
    const root = dv.container.querySelector("#char-builder-root");
    if(!root) return;
    
    const bgSelect = root.querySelector("#background-select");
    const dynamicContent = root.querySelector("#dynamic-bg-content");

    // NEW CLEANUP LOGIC: Strips markdown and repetitive words
    function extractList(text, key) {
        const regex = new RegExp(`${key}:\\s*(.*)`, 'i');
        const match = text.match(regex);
        if (match && match[1]) {
            return match[1].split(',').map(s => {
                // Remove [[, ]], and **
                let cleaned = s.replace(/\[\[|\]\]|\*\*/g, '');
                // Remove " Saving Throw" (case-insensitive)
                cleaned = cleaned.replace(/ saving throw/gi, '');
                // Trim extra spaces
                return cleaned.trim();
            }).filter(s => s.length > 0);
        }
        return [];
    }

    bgSelect.addEventListener("change", async (e) => {
        const filePath = e.target.value;
        const bgName = e.target.options[e.target.selectedIndex].text;
        
        const content = await dv.io.load(filePath);
        if(!content) return;
        
        const abilities = extractList(content, "Ability Scores");
        const saves = extractList(content, "Saving Throws");
        const general = extractList(content, "General Skill Ranks");
        const expert = extractList(content, "Expert Skill Ranks");
        
        dynamicContent.style.display = "block";
        let contentHtml = `<h4>Options for: ${bgName}</h4>`;

        if (abilities.length > 0) {
            contentHtml += `<p><strong>Ability Scores</strong> (Increase 3 of them by 1):</p><div style="margin-bottom: 15px;">`;
            abilities.forEach(ab => { contentHtml += `<label class="selectable-btn"><input type="checkbox" value="${ab}"> ${ab}</label>`; });
            contentHtml += `</div>`;
        }

        if (saves.length > 0) {
            contentHtml += `<p><strong>Saving Throws</strong> (Increase 2 of them by 1 Rank):</p><div style="margin-bottom: 15px;">`;
            saves.forEach(sv => { contentHtml += `<label class="selectable-btn"><input type="checkbox" value="${sv}"> ${sv}</label>`; });
            contentHtml += `</div>`;
        }

        if (general.length > 0) {
            contentHtml += `<p><strong>General Skill Ranks</strong> (Distribute 4 Ranks):</p><div style="margin-bottom: 15px;">`;
            general.forEach(sk => { contentHtml += `<div class="skill-row"><span>${sk}</span><input type="number" min="0" max="4" value="0"></div>`; });
            contentHtml += `</div>`;
        }

        if (expert.length > 0) {
            contentHtml += `<p><strong>Expert Skill Ranks</strong> (Distribute 3 Ranks):</p><div>`;
            expert.forEach(sk => { contentHtml += `<div class="skill-row"><span>${sk}</span><input type="number" min="0" max="3" value="0"></div>`; });
            contentHtml += `</div>`;
        }

        dynamicContent.innerHTML = contentHtml;

        // Bind clickable toggle for the red borders
        const checkboxes = dynamicContent.querySelectorAll('.selectable-btn input[type="checkbox"]');
        checkboxes.forEach(box => {
            box.addEventListener('change', function() {
                if(this.checked) {
                    this.parentElement.classList.add('selected');
                } else {
                    this.parentElement.classList.remove('selected');
                }
            });
        });
    });
}, 150);
```
