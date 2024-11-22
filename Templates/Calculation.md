<%*
const uuid = crypto.randomUUID();
const baseFolder = '.data/';
const calcFolder = `${baseFolder}${uuid}`;
const jupyterToken = 'CustomizedConstantJupyterToken';
-%>
---
uuid: <% uuid %>
alias: <% uuid %>
creation_date: <% tp.date.now() %>
completion_date: 
complete: false
computer:
jobid:
---

# Metadata

`VIEW[**UID: {uuid}**][text(renderMarkdown)]`  `BUTTON[copyuuid]`
`VIEW[**Creation Date: {creation_date}**][text(renderMarkdown)]`
**Completion Date:** `INPUT[date:completion_date]` `INPUT[toggle:complete]`
**On Hold:** `INPUT[toggle:on_hold]`

**Computer:** `INPUT[inlineSelect( option(custom1), option(custom2) ):computer]` | **Job ID:** `INPUT[inlineList:jobid]`

`BUTTON[openfolder]` `BUTTON[copypath]` `BUTTON[jupyterlink]` `BUTTON[createfolder]`

## Tags

_Tags here._

## Description 

_Description and notes here._

---

# Data

_Extracted data here._

---

```meta-bind-button
label: "Open Folder"
icon: ""
hidden: true
class: ""
tooltip: ""
id: "openfolder"
style: primary
actions:
  - type: inlineJS
    code: "window.open('file://' + app.vault.adapter.getBasePath() + '/<% calcFolder %>');"
```

```meta-bind-button
label: "Open Notebook"
icon: ""
hidden: true
class: ""
tooltip: ""
id: "jupyterlink"
style: primary
actions:
  - type: open
    link: http://localhost:8888/lab/tree/<% uuid %>?token=<% jupyterToken %>
```

```meta-bind-button
label: "Copy"
icon: ""
hidden: true
class: ""
tooltip: ""
id: "copyuuid"
style: default
actions:
  - type: inlineJS
    code: "navigator.clipboard.writeText('<% uuid %>')"
```

```meta-bind-button
label: "Copy Path"
icon: ""
hidden: true
class: ""
tooltip: ""
id: "copypath"
style: default
actions:
  - type: inlineJS
    code: "navigator.clipboard.writeText(app.vault.adapter.getBasePath() + '/<% calcFolder %>')"
```

```meta-bind-button
label: "Create Folder"
icon: ""
hidden: true
class: ""
tooltip: ""
id: "createfolder"
style: default
actions:
  - type: inlineJS
    code: "app.vault.createFolder('<% calcFolder %>');"
```

[template_rev::5]
