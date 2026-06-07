*Carved from the heart of stone itself, dwarves are a long lasting and enduring folk. Their bond with the earth runs deep; stone, metal, and gem feel as much a part of them as flesh and blood. Though their origins lie in the deep places of the world, dwarves have spread far across the realms, adapting to mountain strongholds, bustling cities, and distant frontiers alike.*

**Long-lived.** Dwarves mature at roughly the same pace as humans but are not considered adults until the age of 50. On average, they live about 350 years.

**Stout and Sturdy.** Dwarves stand between 1.2 and 1.5 meters tall, weighing around 70 kilograms on average. Their compact builds are dense with muscle and bone, granting them remarkable endurance. Your [[Creature Size]] is Medium.

**Slow Stride.** Your [[Walking Speed]] is 6 meters.

### Dwarven Ancestry Talents
Having a dwarven ancestry you unlock multiple [[Ancestry Talent|Ancestry Talents]] that shape how your dwarf is. These [[Talent|Talent]] are:

```dataview
TABLE WITHOUT ID file.link AS "Talent Name",
file.link.Group AS "Group",
file.link.Cost AS "Cost",
string(file.link.Requirements) AS "Requirements",
string(file.link.Following) AS "Following Talents"
FROM #talent AND #dwarven 
WHERE file.name != "Background Template"
SORT file.name ASC
```

___
#keyword #common #ancestry [[Ancestry|]]