---
type: meta
uid: "META-PROCESSING-REGISTER"
tags:
  - type/meta
---

# Rejestr przetwarzania korpusu

Tabela postępu przetwarzania dokumentów wejściowych na notatki źródłowe w vault. Materiał NIE jest oznaczany jako "Gotowe", dopóki nie ma utworzonej notatki źródłowej w `20-Sources/`.

Status "OCR w toku" oznacza dokumenty przetwarzane obecnie przez `scripts/pipeline.py` (pipeline OCR działa niezależnie od tempa tworzenia notatek merytorycznych — patrz `processing_status.json` w repo `projekty/Parzonko` po aktualny stan techniczny OCR).

| Plik | Typ | Źródło | OCR | Notatka źródłowa | Status | Uwagi |
|---|---|---|---|---|---|---|
| `BU 01006_501 DONOSY Z PROCESU W ŁAPACH I CIECHANOWCU.pdf` | PDF | IPN | Tak | [[IPN-BU-01006-501-Donosy-z-procesu-Lapy-Ciechanowiec]] | Gotowe | Dokument kalibracyjny #1. Jakość OCR mieszana, str. 4 nieczytelna. |
| `BU 024_95 ZDJECIE W MIODUSACH Z RADZISZEWSKIM I OLSZEWSKIM.pdf` | PDF | IPN | Tak | [[IPN-BU-024-95-Zdjecie-Miodusy-Radziszewski-Olszewski]] | Gotowe (wymaga przeglądu) | Dokument kalibracyjny #2. Jakość OCR słaba — karta fotograficzna, wymaga ręcznego obejrzenia skanu. |
| pozostałe ~138 dokumentów korpusu | PDF/DOC | IPN / archiwum rodzinne | częściowo (w toku) | — | Oczekuje | Pipeline OCR (`scripts/pipeline.py`) przetwarza korpus w tle; notatki źródłowe do utworzenia w Task 9 po zatwierdzeniu szablonu kalibracyjnego. |

## Status opracowania (stan kalibracji)

- Liczba źródeł z notatką: 2 / 140
- Liczba wydarzeń: 2 (`EVENT-1953-001`, `EVENT-1953-002`)
- Liczba osób: 4 (`PERSON-001` – `PERSON-004`)
- Liczba miejsc: 2 (`PLACE-001`, `PLACE-002`)
- Materiały wymagające OCR: cały pozostały korpus, w toku (pipeline działa w tle)
- Materiały wymagające ręcznej weryfikacji: `IPN-BU-024-95` (jakość OCR słaba, karta fotograficzna); strona 4 dokumentu `IPN-BU-01006-501` (spis treści, nieczytelny OCR)
