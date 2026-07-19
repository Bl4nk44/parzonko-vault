---
type: index
title: "Indeks osób"
tags:
  - type/index
---

# Indeks osób (40-People)

## Wszystkie osoby

```dataview
TABLE WITHOUT ID file.link AS "Notatka", uid AS "UID", full_name AS "Imię i nazwisko", aliases AS "Pseudonimy", birth_date AS "Ur.", death_date AS "Zm.", certainty AS "Pewność"
FROM "40-People"
SORT surname ASC
```

## Osoby o niskiej/średniej pewności identyfikacji

```dataview
TABLE WITHOUT ID file.link AS "Notatka", uid AS "UID", full_name AS "Imię i nazwisko", certainty AS "Pewność"
FROM "40-People"
WHERE certainty = "low" OR certainty = "medium"
SORT certainty DESC, surname ASC
```

## Liczba źródeł wymieniających osobę (wg backlinków)

```dataview
TABLE WITHOUT ID file.link AS "Osoba", length(file.inlinks) AS "Backlinki"
FROM "40-People"
SORT length(file.inlinks) DESC
```
