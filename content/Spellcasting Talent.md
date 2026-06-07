
```dataview
TABLE WITHOUT ID file.link AS "Talent Tree Name"
FROM #spellcasting AND #talent_tree     
WHERE file.name != "Talent Template"
SORT file.name ASC
```

```dataview
TABLE WITHOUT ID file.link AS "Talent Name",
file.link.Group AS "Group",
file.link.Cost AS "Cost",
string(file.link.Requirements) AS "Requirements",
string(file.link.Following) AS "Following Talents"
FROM #spellcasting AND #talent 
WHERE file.name != "Talent Template"
SORT file.name ASC
```
