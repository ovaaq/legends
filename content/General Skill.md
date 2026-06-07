General Skills represent the common activities and practical tasks that any adventurer might attempt during their journeys. Each General Skill is rated by a [[Rank]] from 0 (untrained) to 4 (mastery). When you attempt a [[Check]], add the skill’s [[General Skill Modifier]] to the roll. This modifier is calculated as follows:

> [!info] Calculating General Skill Modifier  
> General Skill Modifier = [[Ability Score]] + ([[Rank]] × 2)

Each General Skill is listed below.

```dataview
TABLE WITHOUT ID file.link AS "General Skills",
file.link.Modifier AS "Ability Score*"
FROM #general_skill  
WHERE file.name != "Background Template"
SORT file.name ASC
```
\* Some [[General Skill|General Skills]] can be used with multiple [[Ability Score|Ability Scores]]

___
#keyword