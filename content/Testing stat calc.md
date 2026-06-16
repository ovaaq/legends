<div>

<div>
<h3>Distribute Ability Scores

<table>

<tr>
<th>Ability</th>
<th>Ability Score</th>
</tr>

<tr>
<td>Strength</td>
<td><input type="number" value="0"></td>
</tr>

<tr>
<td>Agility</td>
<td><input type="number" value="0"></td>
</tr>

<tr>
<td>Precision</td>
<td><input type="number" value="0"></td>
</tr>

<tr>
<td>Constitution</td>
<td><input type="number" value="0"></td>
</tr>

<tr>
<td>Awareness</td>
<td><input type="number" value="0"></td>
</tr>

<tr>
<td>Charisma</td>
<td><input type="number" value="0"></td>
</tr>

<tr>
<td>Intelligence</td>
<td><input type="number" value="0"></td>
</tr>

<tr>
<td>Sorcery</td>
<td><input type="number" value="0"></td>
</tr>
</table>

</div>

<div>

<h3>Select Core Ancestry</h3>

<select name="pets" id="pet-select">
  <option value="">--Please choose an option--</option>
  <option value="dog">Dwarven Ancestry</option>

</select>

</div>
<div>

<h3>Select Additional Ancestry</h3>

<select name="pets" id="pet-select">
  <option value="">No Additional Ancestry</option>
  <option value="dog">Dwarven Ancestry</option>

</select>

</div>

<div>

<h3>Select Background</h3>

<select name="pets" id="pet-select">
  <option value="">--Please choose an option--</option>
  <option value="dog">Artisan</option>

</select>
<br>

<div><h4>Background's Ability Score Improvements</h4>  
<button class="choice" onclick="toggle(this)">Strength</button>  
<button class="choice" onclick="toggle(this)">Agility</button>  
<button class="choice" onclick="toggle(this)">Precision</button>  
<button class="choice" onclick="toggle(this)">Constitution</button>  
</div>
<br>
<div><h4>Background's Saving Throw Improvements</h4>  
<button class="choice" onclick="toggle(this)">Strength</button>  
<button class="choice" onclick="toggle(this)">Agility</button>  
<button class="choice" onclick="toggle(this)">Constitution</button>  
</div>

</div>

<script>  function toggle(btn) {    const active = document.querySelectorAll(".choice.active");    if (btn.classList.contains("active")) {      btn.classList.remove("active");      return;    }    if (active.length >= 3) return;    btn.classList.add("active");  }</script>
