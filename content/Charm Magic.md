```dataview
TABLE WITHOUT ID link.file.link AS "List of Charm Spells"
FROM ""
WHERE file.name = this.file.name
FLATTEN file.inlinks AS link
SORT link.file.name ASC
```





