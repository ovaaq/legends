_Elves are a graceful and long-lived people, closely attuned to the rhythms of nature and the flow of magic. Their lives are intertwined with forests, glades, and hidden groves, and though their origins are ancient and mysterious, elves now dwell wherever the natural world thrives, blending seamlessly with its beauty and secrets._

**Long-Lived.** Elves mature more slowly than humans and are not considered adults until around the age of 100. On average, they live about 700 years.

**Tall and Slender.** Elves stand between 1.5 and 1.9 meters tall, weighing around 50 kilograms on average. Your [[Creature Size]] is Medium.

**Standard Stride.** Your [[Walking Speed]] is 7 meters.

### Elven Ancestry Talents
Having a elven ancestry you unlock multiple [[Ancestry Talent|Ancestry Talents]] that shape how your elf is. These [[Talent|Talent]] are:

```dataview
TABLE WITHOUT ID file.link AS "Talent Name",
file.link.Group AS "Group",
file.link.Cost AS "Cost",
string(file.link.Requirements) AS "Requirements",
string(file.link.Following) AS "Following Talents"
FROM #talent AND #elven 
WHERE file.name != "Background Template"
SORT file.name ASC
```
___
#keyword #common #ancestry [[Ancestry|]]