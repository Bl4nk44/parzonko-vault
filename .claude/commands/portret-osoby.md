---
description: Kompletny portret osoby — wszystko co vault o niej wie, z cytowaniami i oceną spójności
argument-hint: nazwisko, pseudonim lub PERSON-XXX
---

Zbuduj kompletny portret osoby: **$ARGUMENTS** — wyłącznie z danych vaulta (ZASADA ZERO z CLAUDE.md obowiązuje bezwzględnie).

Procedura:

1. **Identyfikacja.** Znajdź notatkę w `40-People/` (grep po nazwisku, pseudonimie i UID — pamiętaj o wariantach OCR: „ł"→„l", „ż"→„z", zniekształcenia końcówek). Jeśli pasuje więcej niż jedna osoba — STOP, pokaż kandydatów z kontekstem (daty, sprawa, dowódca) i spytaj, o którego chodzi. Nie zakładaj, że zbieżność nazwiska = ta sama osoba.
2. **Zbierz wystąpienia.** Grep UID-u i wariantów nazwiska przez `20-Sources`, `30-Events`, `10-Biography`, `60-Topics`, potem pełny OCR w `80-Media/ocr/`. Odnotuj wystąpienia w OCR, których nie ma w żadnej notatce syntetycznej — to potencjalnie niewydobyte fakty.
3. **Portret.** Sekcje: dane biograficzne (z `_accuracy` i rozbieżnościami między źródłami), chronologia udziału w wydarzeniach, relacje z innymi osobami, miejsca, status w śledztwach/sprawach. **Każdy fakt: `SRC-XXX, str. N`.**
4. **Ocena spójności.** Osobna sekcja: sprzeczności między źródłami (daty, pseudonimy, role), fakty wiszące na jednym słabym OCR (`certainty: low`), luki (okresy bez żadnego źródła).
5. **Niewydobyte tropy.** Lista trafień z kroku 2, które warto przenieść do notatek (nie twórz notatek sam — wypisz propozycje).

Niczego nie uzupełniaj wiedzą ogólną. Jeżeli vault milczy — napisz „vault tego nie potwierdza".
