---
type: index
title: "Indeks wydarzeń — chronologia"
tags:
  - type/index
---

# Chronologia wydarzeń (30-Events)

```dataview
TABLE WITHOUT ID date AS "Data", file.link AS "Wydarzenie", event_type AS "Typ", date_accuracy AS "Dokładność", certainty AS "Pewność"
FROM "30-Events"
SORT date ASC
```

## Wydarzenia bez miejsca

```dataview
TABLE WITHOUT ID date AS "Data", file.link AS "Wydarzenie"
FROM "30-Events"
WHERE place = null
SORT date ASC
```
