[[Cantrip]]
[[1st Level Spell]]
[[2nd Level Spell]]
[[3rd Level Spell]]
[[4th Level Spell]]
[[5th Level Spell]]
[[6th Level Spell]]

```dataview
TABLE WITHOUT ID file.link AS "Spell",
Level,
Casting,
Components,
Mana,
Range,
Duration
FROM #spell AND (#cantrip OR #1st OR #2nd OR #3rd OR #4th OR #5th OR #6th)
SORT file.name ASC
```
___
#keyword