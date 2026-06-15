<div style="padding: 1.5rem; border: 1px solid var(--lightgray); border-radius: 8px; background-color: var(--light); max-width: 350px;">
  <h3 style="margin-top: 0;">Long Rest Recovery</h3>

  <div style="margin-bottom: 10px;">
    <label style="display: inline-block; width: 120px; font-weight: bold; color: var(--darkgray);">Max HP:</label>
    <input type="number" id="maxHp" value="50" style="width: 80px; padding: 4px; border: 1px solid var(--gray); border-radius: 4px; background: var(--light); color: var(--dark);">
  </div>

  <div style="margin-bottom: 20px;">
    <label style="display: inline-block; width: 120px; font-weight: bold; color: var(--darkgray);">CON Modifier:</label>
    <input type="number" id="conMod" value="2" style="width: 80px; padding: 4px; border: 1px solid var(--gray); border-radius: 4px; background: var(--light); color: var(--dark);">
  </div>

  <div style="margin-top: 10px; padding-top: 15px; border-top: 1px solid var(--lightgray);">
    <span style="font-weight: bold; color: var(--darkgray);">HP Regenerated: </span>
    <span id="hpResult" style="font-weight: bold; color: var(--tertiary); font-size: 1.2em;">--</span>
  </div>

  <script>
    function calculateRest() {
      // 1. Grab the current numbers from the inputs
      const max = parseInt(document.getElementById('maxHp').value) || 0;
      const conInput = document.getElementById('conMod').value;
      const con = conInput === "" ? 0 : parseInt(conInput);
      
      // 2. THE MATH: Regain 50% of Max HP + CON Modifier
      let regenerated = Math.floor(max * 0.5) + con;
      
      // Make sure you don't regenerate below 0 or above Max HP
      if (regenerated < 0) regenerated = 0;
      if (regenerated > max) regenerated = max;
      
      // 3. Update the text on the screen
      document.getElementById('hpResult').textContent = regenerated + " HP";
    }

    // 4. THE TRIGGERS: Automatically calculate when inputs change
    document.getElementById('maxHp').addEventListener('input', calculateRest);
    document.getElementById('conMod').addEventListener('input', calculateRest);

    // 5. Run it once immediately so the default values display correctly on page load
    calculateRest();
  </script>

</div>

---

#keyword
