
```dataview
TABLE WITHOUT ID file.link AS "Main Arcane Talent Tree"
FROM #arcane AND #talent_tree     
WHERE file.name != "Talent Template" AND file.name = "Arcane Talent Tree"
SORT file.name ASC
```

```dataview
TABLE WITHOUT ID file.link AS "Sub Talent Trees"
FROM #arcane AND #talent_tree     
WHERE file.name != "Talent Template" AND file.name != "Arcane Talent Tree"
SORT file.name ASC
```

```dataview
TABLE WITHOUT ID file.link AS "Talent Name",
file.link.Group AS "Group",
file.link.Cost AS "Cost",
string(file.link.Requirements) AS "Requirements",
string(file.link.Following) AS "Following Talents"
FROM #talent AND #arcane 
WHERE file.name != "Talent Template"
SORT file.name ASC
```

