Ancestry defines a character’s natural traits, heritage, and tendencies. It shapes their physical form, lifespan, and potential ancestral abilities, while also influencing cultural outlooks and affinities. Choosing an Ancestry provides the foundation for who your character is and how they interact with the world. Ancestry affects your [[Walking Speed]], [[Creature Size]], and other traits. Ancestries are divided into Common Ancestries and Rare Ancestries.

Common Ancestry represents the classic ancestries of the world. Your character must be at least half one of these ancestries. Characters can be a pure Core Ancestry or a hybrid, combining two ancestries. A complete list is provided in the table below.

```dataview
TABLE WITHOUT ID file.link AS "Common Ancestries"
FROM #ancestry AND #common 
SORT file.name ASC
```

Rare Ancestries are rare, and characters can be at most half derived from them. A complete list is provided in the table below.

```dataview
TABLE WITHOUT ID file.link AS "Rare Ancestries"
FROM #ancestry AND #rare 
SORT file.name ASC
```

___
#keyword