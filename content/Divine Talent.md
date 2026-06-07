
```dataview
TABLE WITHOUT ID file.link AS "Main Divine Talent Tree"
FROM #divine AND #talent_tree     
WHERE file.name != "Talent Template" AND file.name = "Divine Talent Tree"
SORT file.name ASC
```

```dataview
TABLE WITHOUT ID file.link AS "Sub Talent Trees"
FROM #divine AND #talent_tree     
WHERE file.name != "Talent Template" AND file.name != "Divine Talent Tree"
SORT file.name ASC
```

```dataview
TABLE WITHOUT ID file.link AS "Talent Name",
file.link.Group AS "Group",
file.link.Cost AS "Cost",
string(file.link.Requirements) AS "Requirements",
string(file.link.Following) AS "Following Talents"
FROM #talent AND #divine 
WHERE file.name != "Talent Template"
SORT file.name ASC
```

