Ancestry Talents are [[Talent|Talents]] tied to your character’s [[Ancestry]]. Each Ancestry grants a unique set of Talents that reflect innate abilities, cultural teachings, and ancestral powers. You can view them for each Ancestry in the list below.

```dataview
TABLE WITHOUT ID file.link AS "Common Ancestries"
FROM #ancestry AND #common 
SORT file.name ASC
```

```dataview
TABLE WITHOUT ID file.link AS "Rare Ancestries"
FROM #ancestry AND #rare 
SORT file.name ASC
```


You can view all Ancestry [[Talent|Talents]] in the list. Note that each Talent has its required [[Ancestry]].

```dataview
TABLE WITHOUT ID file.link AS "Talent Name",
file.link.Cost AS "Cost",
string(file.link.Requirements) AS "Requirements",
string(file.link.Following) AS "Following Talents"
FROM #talent AND #ancestry 
WHERE file.name != "Talent Template"
SORT file.name ASC
```