**Requirements**:: 
**Cost**:: 3 LP

*Flavour text*.

New resource Stamina

[[Stamina Point Maximum]] = [[Constitution]]

Regain all back if you gain benefits of 1 hour rest. [[Martial Technique|Martial Techniques]]

Benefit. Learn from list two. Each technique requires X stamina and uses it.


```dataview
TABLE WITHOUT ID file.link AS "Martial Techniques"

FROM #martial_technique AND #1st   
WHERE file.name != "Talent Template" AND file.name != "Martial Technique Template"
SORT file.name ASC
```


**Group**:: Martial
**Following**:: [[Martial Techniques II]]
___
#talent #martial 
[[Talent|]] [[Talent|]][[Martial Talent|]]