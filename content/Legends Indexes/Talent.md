A Talent is a single learned ability or power that grants a specific mechanical benefit and helps define what a character can do.

Talents are organized into Talent Groups to make them easier to find and reference.  
Some Talents also form [[Talent Tree|Talent Trees]], which are structured progressions where later Talents require earlier ones as prerequisites.

A complete list of Talent Groups can be found in the table below.

|      Talent Group       | Description                                                       |
| :---------------------: | ----------------------------------------------------------------- |
|   [[Ancestry Talent]]   | Traits inherited from your ancestral bloodline.                   |
|   [[General Talent]]    | Core improvements.                                                |
|   [[Martial Talent]]    | Mastery of weapons, armor, combat styles, and martial techniques. |
|    [[Arcane Talent]]    | Scholarly magic drawn from study.                                 |
|    [[Divine Talent]]    | Powers granted through faith.                                     |
|    [[Innate Talent]]    | Inborn or herited powers awakened.                                |
|     [[Pact Talent]]     | Powers gained by forging bargains.                                |
|  [[Spiritual Talent]]   | Communion with spirits beyond the material world.                 |
| [[Spellcasting Talent]] | Universal spellcasting techniques.                                |

```dataview
TABLE
    length(rows) AS "Talent Count"
FROM #talent
WHERE file.name != "Talent Template"
GROUP BY file.link.Group
SORT file.link.Group ASC
```


Feeling bold? Take a scroll through all the Talents…

```dataview
TABLE WITHOUT ID file.link AS "Talent Name",
file.link.Group AS "Group",
file.link.Cost AS "Cost",
string(file.link.Requirements) AS "Requirements",
string(file.link.Following) AS "Following Talents"
FROM #talent   
WHERE file.name != "Talent Template"
SORT file.name ASC
```


___
#keyword