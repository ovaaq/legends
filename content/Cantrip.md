
```dataview
TABLE WITHOUT ID file.link AS "Cantrip",
Casting,
Components,
Mana,
Range,
Duration
FROM #spell AND #cantrip
SORT file.name ASC
```



to do


[[Dark Flame]]
[[Ignite]]



Static Charge
Sword Burst

Toll the Death

Withering Touch
Word of Radiance



Thaumaturgy
Witchcraft


Summon Insect
ideas

[[Shadow Veil]]
[[Jump]]


```dataview
TABLE WITHOUT ID link.file.link AS "List of Cantrips"
FROM ""
WHERE file.name = this.file.name
FLATTEN file.inlinks AS link
SORT link.file.name ASC
```

___
#keyword