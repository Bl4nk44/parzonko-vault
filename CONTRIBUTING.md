# Jak pracować z tym vaultem

Vault badawczy — każdy fakt musi być wywodliwy do konkretnej strony dokumentu źródłowego. Pełny schemat i konwencje: [[00-Meta/Schema-and-Conventions]] (**przeczytaj przed pierwszą edycją**).

## Skrót zasad

1. **Statusy**: nowa/zmieniona notatka dostaje `#status/unreviewed`. Tag `#status/verified` nadaje wyłącznie człowiek po weryfikacji ze źródłem — nigdy AI, nigdy autor własnej notatki.
2. **Pewność**: pole `certainty: high/medium/low` w frontmatter — to ocena faktu, nie statusu review.
3. **Cytowanie**: każde twierdzenie ze wskazaniem strony (`Źródło: strona 3.`). Bez strony = nie wpisujemy.
4. **UID-y**: nie wymyślaj ręcznie. Rejestr: `00-Meta/uid-registry.json` — alokacja przez pipeline (`uid_registry.py`) lub po uzgodnieniu z prowadzącym projekt.
5. **Sprzeczności źródeł**: nie wybieraj jednej wersji — blockquote „Hipoteza robocza" z opisem rozbieżności (szablon w Schema-and-Conventions).
6. **Nie scalaj osób** po samym nazwisku — sprawdź kontekst (data, sprawa, dowódca). W tym środowisku były dwie różne osoby „Radziszewski" i dwóch „Kazimierzów".
7. **OCR**: pełny tekst w `80-Media/ocr/`, notatka źródłowa w `20-Sources/` zostaje lekka (opis, ustalenia, cytaty, linki).

## Workflow git (plugin Obsidian Git jest skonfigurowany)

- Vault auto-pulluje co 10 min i przy starcie — pracujesz zawsze na aktualnym stanie.
- Commit **ręczny**, po skończeniu logicznej całości (jeden dokument / jedno ustalenie), przez panel „Source Control" lub `Ctrl+P` → „Git: Commit-and-push".
- Wiadomość commita: co i skąd, np. `SRC-092: notatka źródłowa + 2 osoby (BU 1069/60 t1)`.
- Większe zmiany (nowy dokument, zmiana ustaleń w zweryfikowanej notatce) → osobny branch + Pull Request na GitHubie, ktoś drugi przegląda.
- **Nie force-pushuj. Nie edytuj cudzych branchy bez uzgodnienia.**

## Konflikty

Przy konflikcie merge plugin pokaże pliki z markerami `<<<<<<<`. Nie zgaduj — skontaktuj się z autorem drugiej zmiany albo zostaw notatkę z `#status/conflict` i opisem w treści.
