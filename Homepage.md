---
id_search: ""
---

### New Calculation

`BUTTON[create]`

### Find Calculations

Job ID or UUID: `INPUT[text:id_search]`

```dataview
TABLE choice(complete , "✅", "✘") as Complete
FROM "Calculations"
WHERE this.id_search != ""
AND (
contains(file.frontmatter.jobid, this.id_search)
OR contains(file.frontmatter.uuid, this.id_search)
)
```

### Unfinished Calculations

```dataview
TABLE creation_date as Created, computer as Computer
FROM "Calculations"
SORT creation_date asc
WHERE complete = false AND on_hold != true
```

### Recent Calculations

```dataview
TABLE creation_date as Created, choice(complete , "✅", "✘") as Complete
FROM "Calculations"
WHERE creation_date >= date(today) - dur("1 w")
SORT creation_date descending
```

```meta-bind-button
label: Create New Calculation
icon: ""
hidden: true
class: ""
tooltip: ""
id: "create"
style: primary
actions:
  - type: templaterCreateNote
    templateFile: Templates/Calculation.md
    folderPath: Calculations
    fileName: New Calculation
    openNote: true

```

### On-Hold Calculations

```dataview
TABLE creation_date as Created, computer as Computer
FROM "Calculations"
SORT creation_date asc
WHERE on_hold = true
```