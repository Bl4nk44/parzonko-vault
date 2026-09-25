---
description: Znajdź fakt w vaultcie z pełnym łańcuchem cytowania (twierdzenie → notatka → SRC → strona)
argument-hint: pytanie badawcze (np. "kiedy Parzonko wstąpił do oddziału Młota")
---

Odpowiedz na pytanie: **$ARGUMENTS** — wyłącznie z danych vaulta (ZASADA ZERO z CLAUDE.md).

Procedura warstwowa (przerwij na warstwie, która daje pewną odpowiedź, ale zawsze sprawdź warstwę 1):

1. **Rozstrzygnięcia** — `00-Meta/Otwarte-Pytania-Badawcze.md`: czy to pytanie już rozstrzygnięto/omówiono.
2. **Notatki syntetyczne** — `10-Biography`, `30-Events`, `40-People`, `60-Topics`, potem `20-Sources` (grep po kluczowych terminach i UID-ach).
3. **Pełny OCR** — `80-Media/ocr/` z wariantami OCR („ł"→„l", „ż"→„z", zniekształcone końcówki). Trafienie w OCR → ustal stronę (nagłówek `## Strona N` nad trafieniem) i źródło (nazwa pliku = notatka źródłowa).

Format odpowiedzi:

- **Odpowiedź** — jedno-dwa zdania.
- **Dowody** — każde źródło: `SRC-XXX, str. N` + cytat lub bliska parafraza; ocena: potwierdzone krzyżowo / pojedynczy świadek / sprzeczne wersje.
- **Zastrzeżenia** — jakość OCR, typ dokumentu (doniesienie agenturalne ≠ fakt), luki.

Reguły twarde:
- Vault milczy → „vault tego nie potwierdza" + gdzie szukałeś. Nie uzupełniaj wiedzą ogólną; kontekst historyczny spoza vaulta wolno dodać tylko wyraźnie oznaczony „poza vaultem, do weryfikacji".
- Sprzeczne źródła → pokaż wszystkie wersje, nie wybieraj po cichu.
- Fakt znaleziony tylko w OCR (niewydobyty do notatek) → zaznacz to; zaproponuj dopisanie do właściwej notatki (bez samodzielnego tworzenia notatek źródłowych — UID-y alokuje pipeline).
- Odpowiedź będąca nową syntezą (zebranie rozproszonych faktów, porównanie źródeł, rozstrzygnięcie) → zaproponuj
  zapis jako notatkę w `60-Topics/` (frontmatter wg `00-Meta/Schema-and-Conventions.md`, `#status/unreviewed`,
  każdy fakt z `SRC-XXX, str. N`). Zapis dopiero po akceptacji użytkownika.
