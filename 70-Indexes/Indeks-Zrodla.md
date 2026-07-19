---
type: index
title: "Indeks źródeł"
tags:
  - type/index
---

# Indeks źródeł (20-Sources)

## Wszystkie źródła

```dataview
TABLE WITHOUT ID file.link AS "Notatka", uid AS "UID", archive AS "Archiwum", call_number AS "Sygnatura", date_document AS "Data dok.", pages AS "Str.", reliability AS "Ranga"
FROM "20-Sources"
SORT uid ASC
```

## Wg jakości OCR (słabe = kandydaci do vision-OCR / ręcznej weryfikacji)

```dataview
TABLE WITHOUT ID file.link AS "Notatka", uid AS "UID", ocr_quality AS "Jakość OCR"
FROM "20-Sources"
WHERE ocr_quality != null AND (contains(ocr_quality, "słaba") OR contains(ocr_quality, "nieczyteln"))
SORT uid ASC
```
