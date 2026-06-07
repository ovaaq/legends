_Humans are a versatile and ambitious people, known for their adaptability and drive to shape the world around them. Though their lives are shorter than many other ancestries, humans settle in nearly every corner of the realms, building cities, forging alliances, and leaving their mark on history._

**Moderate-Lived.** Humans mature at the same pace as their peers and are considered adults at around the age of 18. On average, they live about 80 years.

**Average Build.** Humans stand between 1.4 and 2.1 meters tall, weighing around 70 kilograms on average. Their builds are balanced, reflecting a blend of strength and agility. Your [[Creature Size]] is Medium.

**Standard Stride.** Your [[Walking Speed]] is 10 meters.

### Celestial Ancestry Talents
Having a celestial ancestry you unlock multiple [[Ancestry Talent|Ancestry Talents]] that shape how your character is. These [[Talent|Talent]] are:

```dataview
TABLE WITHOUT ID file.link AS "Talents",
file.link.Cost AS "Cost"
FROM #talent AND #celestial AND #ancestry 
WHERE file.name != "Background Template"
SORT file.name ASC
```

___
#keyword #rare #ancestry [[Ancestry|]]
