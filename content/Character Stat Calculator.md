<div id="char-builder-root" style="padding: 1.5rem; border: 1px solid var(--lightgray); border-radius: 8px; background: var(--light); max-width: 800px; font-family: sans-serif;">

  <h3>Obsidian Character Builder</h3>

  <!-- ATTRIBUTES -->

  <div style="margin-bottom: 20px;">
    <h4>Attributes</h4>
    <table style="width:100%; max-width:400px;">
      <tbody id="stat-table"></tbody>
    </table>
  </div>

  <!-- ANCESTRY -->

  <div style="margin-bottom: 20px;">
    <h4>Ancestry</h4>

```
<select id="core-ancestry" style="width:100%; padding:8px;">
  <option>Loading...</option>
</select>

<br><br>

<select id="add-ancestry" style="width:100%; padding:8px;">
  <option>Loading...</option>
</select>
```

  </div>

  <!-- BACKGROUND -->

  <div style="margin-bottom: 20px;">
    <h4>Background</h4>

```
<select id="background-select" style="width:100%; padding:8px;">
  <option>Loading backgrounds...</option>
</select>

<div id="dynamic-bg-content" style="margin-top:15px; display:none;"></div>
```

  </div>

</div>

<script>
/* =========================
   1. CONFIG
========================= */

const stats = [
  "Strength","Agility","Precision","Constitution",
  "Awareness","Charisma","Intelligence","Sorcery"
];

/* =========================
   2. HELPERS
========================= */

function parseList(text) {
  if (!text) return [];
  return text.split(',').map(s =>
    s.replace(/\[\[|\]\]|\*\*/g,'').trim()
  ).filter(Boolean);
}

function extractField(text, field) {
  const idx = text.indexOf(field + ":");
  if (idx === -1) return "";
  let start = idx + field.length + 1;
  let slice = text.substring(start);

  const stopFields = [
    "Ability Scores","Saving Throws",
    "General Skill Ranks","Expert Skill Ranks",
    "Talents","Equipment","Initial Wealth"
  ];

  let end = slice.length;
  for (const f of stopFields) {
    const p = slice.indexOf(f + ":");
    if (p !== -1 && p < end) end = p;
  }

  return slice.substring(0,end).trim();
}

/* =========================
   3. BUILD STATIC UI
========================= */

const statTable = document.getElementById("stat-table");

stats.forEach(stat => {
  const row = document.createElement("tr");

  row.innerHTML = `
    <td><strong>${stat}</strong></td>
    <td style="text-align:right;">
      <input type="number" value="10" style="width:70px;">
    </td>
  `;

  statTable.appendChild(row);
});

/* =========================
   4. LOAD QUARTZ INDEX
========================= */

let backgrounds = {};

fetch("static/contentIndex.json")
  .then(r => r.json())
  .then(data => {

    /* build ancestry lists */
    const core = [];
    const add = [];
    const bgList = [];

    for (const [slug, page] of Object.entries(data)) {

      const tags = page.tags || [];
      const content = page.content || "";
      const title = page.title || slug;

      // ancestry
      if (tags.includes("ancestry") && tags.includes("common")) {
        core.push(title);
      }

      if (tags.includes("ancestry")) {
        add.push(title);
      }

      // background
      if (tags.includes("background")) {
        bgList.push(title);

        backgrounds[title] = {
          abilityScores: extractField(content,"Ability Scores"),
          savingThrows: extractField(content,"Saving Throws"),
          generalSkills: extractField(content,"General Skill Ranks"),
          expertSkills: extractField(content,"Expert Skill Ranks"),
          talents: extractField(content,"Talents"),
          equipment: extractField(content,"Equipment"),
          wealth: extractField(content,"Initial Wealth")
        };
      }
    }

    populateSelect("core-ancestry", core);
    populateSelect("add-ancestry", add);
    populateSelect("background-select", bgList);

  });

function populateSelect(id, list) {
  const el = document.getElementById(id);
  el.innerHTML = "";

  list.sort().forEach(item => {
    const opt = document.createElement("option");
    opt.value = item;
    opt.textContent = item;
    el.appendChild(opt);
  });
}

/* =========================
   5. BACKGROUND INTERACTION
========================= */

document.getElementById("background-select")
  .addEventListener("change", e => {

    const name = e.target.value;
    const data = backgrounds[name];
    if (!data) return;

    const box = document.getElementById("dynamic-bg-content");
    box.style.display = "block";

    box.innerHTML = `
      <h4>${name}</h4>

      <p><strong>Ability Scores:</strong> ${data.abilityScores}</p>
      <p><strong>Saving Throws:</strong> ${data.savingThrows}</p>
      <p><strong>General Skills:</strong> ${data.generalSkills}</p>
      <p><strong>Expert Skills:</strong> ${data.expertSkills}</p>
      <p><strong>Talents:</strong> ${data.talents}</p>
      <p><strong>Equipment:</strong> ${data.equipment}</p>
      <p><strong>Wealth:</strong> ${data.wealth}</p>
    `;
  });

</script>
