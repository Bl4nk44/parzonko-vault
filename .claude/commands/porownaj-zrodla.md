---
description: Weryfikacja krzyżowa faktu lub porównanie treści źródeł na zadany temat
argument-hint: fakt/pytanie albo lista źródeł (np. "data urodzenia Parzonki" lub "SRC-004 vs SRC-015")
---

Porównaj źródła w sprawie: **$ARGUMENTS** — wyłącznie dane vaulta (ZASADA ZERO z CLAUDE.md).

Procedura:

1. **Zbierz świadków.** Znajdź wszystkie źródła wypowiadające się w tej sprawie: notatki `20-Sources` (frontmatter + treść), wydarzenia `30-Events` (`key_sources`), pełny OCR `80-Media/ocr/` (z wariantami OCR nazw). Jeśli podano konkretne SRC — zacznij od nich, ale sprawdź też, czy nie ma innych świadków.
2. **Tabela porównawcza.** Wiersz = źródło: `SRC-XXX | strona | co dokładnie mówi (cytat lub parafraza blisko tekstu) | data dokumentu | typ dokumentu | jakość OCR`.
3. **Waga źródeł.** Oceń każde: dokument administracyjny vs doniesienie agenturalne vs protokół przesłuchania (zeznania pod przymusem!); pierwotny vs wtórny (odpis, karta katalogowa przepisująca inne akta); jakość odczytu (`ocr_quality`, `certainty`). Bliskość czasowa do zdarzenia ≠ automatycznie większa wiarygodność — doniesienia agentury bywają fałszywe z natury.
4. **Werdykt.** Jedna z opcji: (a) zgodne — fakt potwierdzony krzyżowo, wskaż najmocniejsze źródło; (b) sprzeczne — pokaż wszystkie wersje z sygnaturami, wskaż którą wspiera przewaga dowodów i dlaczego, sformułuj „Hipotezę roboczą"; (c) pojedynczy świadek — fakt nieweryfikowalny krzyżowo, `certainty` najwyżej `medium`.
5. **Aktualizacja.** Jeśli werdykt rozstrzyga lub otwiera pytanie badawcze — zaproponuj wpis do `00-Meta/Otwarte-Pytania-Badawcze.md` i ewentualne poprawki `certainty`/„Hipoteza robocza" w dotkniętych notatkach. Zmiany wprowadzaj dopiero po akceptacji użytkownika.
