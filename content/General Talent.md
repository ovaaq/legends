General [[Talent|Talents]] are common and miscellaneous improvements for your character, such as increased [[Hit Point|Hit Points]], [[Mana]], and other basic enhancements. They also include a few Talent Trees that don’t fit into any specific category.

Mental, Poison & Alchemy trees are not priority atm.


adventuring tree
Forager
Trailblazer
Pathfinder
Deep Delver
Relic Sniffer
Endurance March

these will be added
[[Inspiring Leader]] <- inspiration tree
[[Read Emotions]]
[[Smooth Talker]]
[[Actor]]
[[Diplomat]]
[[Analyse Person]]
[[Empathic]]

```dataview
TABLE WITHOUT ID file.link AS "Talent Tree Name"
FROM #general AND #talent_tree     
WHERE file.name != "Talent Template"
SORT file.name ASC
```

```dataview
TABLE WITHOUT ID file.link AS "Talent Name",
file.link.Group AS "Group",
file.link.Cost AS "Cost",
string(file.link.Requirements) AS "Requirements",
string(file.link.Following) AS "Following Talents"
FROM #talent AND #general 
WHERE file.name != "Talent Template"
SORT file.name ASC
```
