A Talent Tree is a structured group of related [[Talent|Talents]] arranged in a progression, where access to later Talents requires taking specific earlier Talents. Talent Trees represent focused paths of mastery that characters can follow alongside any other Talents they choose.

```dataview
TABLE WITHOUT ID file.link AS "Talent Tree Name"
FROM #talent_tree     
WHERE file.name != "Talent Template"
SORT file.name ASC
```

___
#keyword 