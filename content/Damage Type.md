
```dataview
TABLE WITHOUT ID file.link AS "Talent Name",
file.link.Type AS "Damage Type Group"
FROM #damage_type    
WHERE file.name != "Talent Template"
SORT file.name ASC
```

___
#keyword