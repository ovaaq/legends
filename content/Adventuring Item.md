[[Equipment]]

```dataview
TABLE WITHOUT ID
    link AS "Item",
    link.Weight AS "Weight",
    link.Cost AS "Cost"
FROM [[Adventuring Item]]
WHERE file.name = "Equipment"
FLATTEN file.inlinks AS link
SORT link.file.name ASC
```


```dataview
TABLE WITHOUT ID
    link.file.link AS "Item",
    link.file.Weight AS "Weight",
    link.file.Cost AS "Cost"
FROM ""
WHERE file.name = "Adventuring Item"
FLATTEN file.inlinks AS link
SORT link.file.name ASC
```


```dataview
TABLE WITHOUT ID link.file.link AS "List of People"
FROM ""
WHERE file.name = "Adventuring Item"
FLATTEN file.inlinks AS link
SORT link.file.name ASC
```


| Name                  | Weight     | Price  | Description                                            |
| --------------------- | ---------- | ------ | ------------------------------------------------------ |
| [[Backpack]]          | 1 Stack    | 2 gp   | Holds and distributes up to several Stacks comfortably |
| [[Ball Bearings]]     | Negligible | 1 gp   | Small metal spheres; used to impede movement           |
| [[Bedroll]]           | 1 Stack    | 1 gp   | Simple bedding for rest while traveling                |
| [[Bell]]              | Negligible | 1 sp   | Small metal bell; audible at distance                  |
| [[Tome]]              | Negligible | 5 gp   | Bound book of notes, lore, or records                  |
| [[Bucket]]            | 1 Stack    | 5 sp   | Wooden or metal container                              |
| [[Bullseye Lantern]]  | 2 Stacks   | 10 gp  | Directional light source                               |
| [[Caltrops]]          | Negligible | 1 gp   | Sharp spikes scattered to slow enemies                 |
| [[Candle]]            | Negligible | 1 cp   | Provides light for several hours                       |
| [[Chain]] (3 m)       | 2 Stacks   | 5 gp   | Heavy iron chain                                       |
| [[Chalk]] (10 pieces) | Negligible | 1 cp   | Used for marking surfaces                              |
| [[Chest]]             | 2 Stacks   | 5 gp   | Sturdy wooden storage chest                            |
| [[Compass]]           | Negligible | 10 gp  | Navigational instrument                                |
| [[Crowbar]]           | 1 Stack    | 2 gp   | Leverage tool for forcing objects                      |
| [[Flint and Steel]]   | Negligible | 5 sp   | Used to start fires                                    |
| [[Glass Vial]]        | Negligible | 1 gp   | Small glass container                                  |
| [[Grappling Hook]]    | 1 Stack    | 2 gp   | Iron hook for climbing                                 |
| [[Hammer]]            | 1 Stack    | 1 gp   | Light hammer for tools or pitons                       |
| [[Hooded Lantern]]    | 2 Stacks   | 5 gp   | Lantern with adjustable shutter                        |
| [[Lock]]              | Negligible | 10 gp  | Average-quality mechanical lock                        |
| [[Magnifying Glass]]  | Negligible | 100 gp | Precision lens for inspection                          |
| [[Manacles]]          | 1 Stack    | 2 gp   | Iron restraints for humanoids                          |
| [[Mirror]]            | Negligible | 5 gp   | Polished reflective surface                            |
| [[Oil Flask]]         | 1 Stack    | 1 sp   | Fuel for lanterns or fires                             |
| [[Parchment Sheet]]   | Negligible | 1 sp   | Writing material                                       |
| [[Pickaxe]]           | 2 Stacks   | 2 gp   | Mining or excavation tool                              |
| [[Pitons]] (10)       | 1 Stack    | 5 sp   | Iron spikes for climbing                               |
| [[Portable Ram]]      | 3 Stacks   | 10 gp  | Reinforced beam for breaking doors                     |
| [[Pouch]]             | Negligible | 5 sp   | Small belt-mounted container                           |
| [[Quill]]             | Negligible | 1 cp   | Writing implement                                      |
| [[Rope]] (15 m)       | 2 Stacks   | 2 gp   | Hemp rope, coiled                                      |
| [[Hunting Trap]]      | 2 Stacks   | 5 gp   | Spring-loaded snare                                    |
| [[Rations]] (3 days)  | 1 Stack    | 15 sp  | Preserved food for travel                              |
| [[Mess Kit]]          | 1 Stack    | 2 gp   | Cooking and eating utensils                            |
| [[Wax Beads]]         | Negligible |        |                                                        |

| Set Name                 | Weight | Price | Description |
| ------------------------ | ------ | ----- | ----------- |
| [[Alchemist’s Supplies]] |        |       |             |
| [[Appraisal Tools]]      |        |       |             |
| [[Brewer’s Kit]]         |        |       |             |
| [[Carpenter’s Tools]]    |        |       |             |
| [[Cartographer’s Kit]]   |        |       |             |
| [[Cook’s Kit]]           |        |       |             |
| [[Disguise Kit]]         |        |       |             |
| [[Exorcism Supplies]]    |        |       |             |
| [[Fishing Tools]]        |        |       |             |
| [[Forgery Kit]]          |        |       |             |
| [[Herbalism Kit]]        |        |       |             |
| [[Jeweler’s Kit]]        |        |       |             |
| [[Leatherworking Tools]] |        |       |             |
| [[Masonry Kit]]          |        |       |             |
| [[Mining Tools]]         |        |       |             |
| [[Smithing Tools]]       |        |       |             |
| [[Thieves' Tools]]       |        |       |             |
| [[Scribe’s Supplies]]    |        |       |             |

___
#keyword