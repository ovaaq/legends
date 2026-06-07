
```dataview
TABLE WITHOUT ID file.link AS "Expert Skills"
FROM #expert_skill 
WHERE file.name != "Background Template"
SORT file.name ASC
```

___
#keyword