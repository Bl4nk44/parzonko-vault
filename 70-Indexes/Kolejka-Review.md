---
type: index
title: "Kolejka review"
tags:
  - type/index
---

# Kolejka review dla człowieka

Notatki z `#status/unreviewed` — po weryfikacji człowiek zmienia tag na `#status/verified` (AI nigdy tego nie robi).

## Priorytet: niska pewność (certainty: low)

```dataview
TABLE WITHOUT ID file.link AS "Notatka", type AS "Typ", certainty AS "Pewność"
FROM "20-Sources" OR "30-Events" OR "40-People" OR "50-Places"
WHERE contains(file.tags, "#status/unreviewed") AND certainty = "low"
SORT type ASC, file.name ASC
```

## Cała kolejka

```dataview
TABLE WITHOUT ID file.link AS "Notatka", type AS "Typ", certainty AS "Pewność"
FROM "20-Sources" OR "30-Events" OR "40-People" OR "50-Places"
WHERE contains(file.tags, "#status/unreviewed")
SORT type ASC, file.name ASC
```

## Zweryfikowane

```dataview
TABLE WITHOUT ID file.link AS "Notatka", type AS "Typ"
FROM "20-Sources" OR "30-Events" OR "40-People" OR "50-Places"
WHERE contains(file.tags, "#status/verified")
SORT type ASC, file.name ASC
```
