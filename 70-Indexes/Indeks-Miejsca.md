---
type: index
title: "Indeks miejsc"
tags:
  - type/index
---

# Indeks miejsc (50-Places)

Mapa: otwórz widok **Map View** (ikona mapy w lewym pasku lub komenda „Map View: Open"). Współrzędne w polu `coordinates`.

```dataview
TABLE WITHOUT ID file.link AS "Notatka", name AS "Nazwa", region AS "Region", coordinates AS "Współrzędne", certainty AS "Pewność"
FROM "50-Places"
SORT file.name ASC
```

## Miejsca bez współrzędnych (do uzupełnienia / niejednoznaczne)

```dataview
LIST
FROM "50-Places"
WHERE coordinates = null
```
