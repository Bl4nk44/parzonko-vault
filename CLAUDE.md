# Vault Parzonko (Obsidian) — baza wiedzy historycznej

Vault badawczy: ~140 dokumentów archiwalnych (głównie akta IPN z lat 1945-1956) o Kazimierzu Parzonko ps. „Zygmunt"/„Wichura" i jego środowisku. Każdy fakt musi być wywodliwy do konkretnej strony konkretnego dokumentu.

Pipeline OCR (skrypty Python, korpus PDF) żyje w osobnym repo `/home/ubuntu/projekty/Parzonko` — istnieje tylko na maszynie WSL prowadzącego projekt. Ten plik jest samowystarczalny dla pracy z samym vaultem.

## ZASADA ZERO — dyscyplina faktów (obowiązkowa, nadrzędna)

1. **Fakty pochodzą wyłącznie z tego vaulta.** Każde twierdzenie o osobie, dacie, wydarzeniu, miejscu musi wskazywać źródło: `SRC-XXX, str. N` (albo notatkę, która takie wskazanie zawiera). Brak źródła w vaultcie = odpowiedz „vault tego nie potwierdza", nie uzupełniaj z pamięci.
2. **Wiedza ogólnohistoryczna** (tło epoki, struktury UB/AK, postaci znane z literatury) może służyć wyłącznie jako **oznaczona hipoteza lub kontekst** — zawsze z zastrzeżeniem „poza vaultem, do weryfikacji", nigdy jako ustalony fakt w notatce.
3. **OCR bywa błędny, vision-OCR potrafi halucynować** (potwierdzony przypadek: podstawiony protokół egzekucji Fieldorfa zamiast realnej treści strony). Fakt z pojedynczego, słabego odczytu OCR traktuj jako `certainty: low`, dopóki nie potwierdzi go druga strona/dokument.
4. **Sprzeczności źródeł to dane, nie problem do ukrycia.** Nie wybieraj jednej wersji — pokaż obie z sygnaturami (wzorzec „Hipoteza robocza", szablon w Schema-and-Conventions).
5. **`#status/verified` nadaje wyłącznie człowiek.** AI wyraża pewność przez pole `certainty: high/medium/low`, notatka startuje z `#status/unreviewed`.

## Mapa danych

| Folder | Zawartość | Kluczowe pola frontmatter |
|---|---|---|
| `20-Sources/` | Notatki źródłowe (1 dokument = 1 notatka, lekka: opis, ustalenia, cytaty) | `uid` (SRC-XXX), `call_number`, `date_document`, `ocr_quality`, `people_mentioned`, `ocr_file` |
| `80-Media/ocr/` | **Pełny tekst OCR** strona po stronie (`## Strona N`) | — |
| `40-People/` | Osoby (PERSON-XXX) | `full_name`, `aliases`, `birth_date`+`_accuracy`, `certainty` |
| `30-Events/` | Wydarzenia (EVENT-...) | `date`+`date_accuracy`, `people_involved`, `key_sources`, `certainty` |
| `50-Places/` | Miejsca (PLACE-XXX) | `name`, `region`, `coordinates` |
| `10-Biography/` | Synteza biograficzna | — |
| `60-Topics/` | Notatki tematyczne | — |
| `70-Indexes/` | Indeksy Dataview: źródła, osoby, chronologia, miejsca, kolejka review, oś czasu | — |
| `00-Meta/` | `Schema-and-Conventions.md` (**jedyne źródło prawdy schematu**), `uid-registry.json`, `Otwarte-Pytania-Badawcze.md`, fileClasses | — |

## Jak szukać faktów (kolejność warstw)

1. **Frontmatter/indeksy** — pytania strukturalne („które źródła wymieniają PERSON-016", „wydarzenia 1951") → grep po polach YAML albo indeksy w `70-Indexes/`.
2. **Notatki syntetyczne** (`20-Sources`, `30-Events`, `40-People`) — ustalenia już wydobyte, z cytatami i numerami stron.
3. **Pełny OCR** (`80-Media/ocr/`) — gdy szukasz czegoś, czego nikt jeszcze nie wydobył. Uwzględniaj warianty OCR nazwisk (np. „Parzonko"/„Parzonlco"/„Parzonke", „ł"→„l", „ż"→„z").

```bash
# które notatki wymieniają osobę (po UID i po nazwisku, z wariantami)
grep -rl "PERSON-016" 20-Sources 30-Events 40-People
grep -rniE "parzon[kl]" 80-Media/ocr | head -50
# fakt w pełnym OCR z kontekstem strony: znajdź trafienie, potem doczytaj nagłówek "## Strona N" nad nim
grep -rn -B2 -A4 "Mężenin" 80-Media/ocr
```

**Odpowiadając na pytanie o fakt, zawsze podawaj łańcuch: twierdzenie → notatka → SRC-XXX → strona.** Jeśli łańcuch się urywa (notatka twierdzi bez strony) — zgłoś to jako defekt danych.

## Typowe przypadki pracy

- **Pytanie o fakt** („kiedy X", „kto Y") → warstwy jak wyżej; odpowiedź z cytowaniem; przy wielu źródłach podaj wszystkie i oceń zgodność. Rozstrzygnięte wcześniej pytania sprawdź najpierw w `00-Meta/Otwarte-Pytania-Badawcze.md`.
- **Porównanie źródeł / weryfikacja krzyżowa** → `/porownaj-zrodla` (komenda w `.claude/commands/`).
- **Polowanie na niespójności** (daty, osoby, miejsca, chronologia awansów) → `/niespojnosci`.
- **Portret osoby** (wszystko, co vault wie o kimś) → `/portret-osoby`.
- **Nowy dokument → notatki** — proces Task 9, wymaga repo pipeline (OCR draft, alokacja UID). Bez dostępu do pipeline: nie twórz notatek źródłowych, zgłoś prowadzącemu.
- **Osoby o zbieżnych nazwiskach** — NIE scalaj po samym imieniu/nazwisku; sprawdź kontekst (data, sprawa, dowódca, miejsce). Precedens: dwie różne osoby „Radziszewski", dwóch różnych „Kazimierzów [pseudonim]" w tym samym środowisku.
- **Pytania przestrzenne** — `coordinates` w `50-Places` (WGS84, z geokodowania Nominatim). Miejsca z `coordinates: null` = niejednoznaczne, nie zgaduj współrzędnych.

## Edycja notatek — zasady twarde

- Schemat YAML, nazewnictwo plików, szablony: **tylko** wg `00-Meta/Schema-and-Conventions.md`. Nie zgaduj schematu z przykładów.
- `00-Meta/uid-registry.json` — nigdy nie edytuj ręcznie i nie wymyślaj UID; alokacja przez `uid_registry.py` z repo pipeline. Bez dostępu do pipeline — poproś prowadzącego o UID.
- Nowa/zmieniona notatka: `#status/unreviewed` + `certainty`. Cytaty z numerem strony.
- Po edycji, przed commitem — sprawdź martwe wikilinki:
  ```bash
  grep -rhoE '\[\[[^]]+\]\]' 20-Sources 30-Events 40-People 50-Places 80-Media 2>/dev/null \
    | sed 's/\[\[//;s/\]\]//' | sed 's|^80-Media/ocr/||' | sort -u > /tmp/links.txt
  find 20-Sources 30-Events 40-People 50-Places 80-Media -name "*.md" \
    | sed 's|.*/||;s/\.md$//' | sort -u > /tmp/files.txt
  comm -23 /tmp/links.txt /tmp/files.txt   # puste = OK
  ```
- Commit: jeden logiczny fragment (jeden dokument / jedno ustalenie), opis co i skąd. Praca zespołowa: `CONTRIBUTING.md`.
- Nowe ustalenie badawcze lub rozstrzygnięcie sporu → zaktualizuj `00-Meta/Otwarte-Pytania-Badawcze.md` (z sygnaturami).

## Pluginy / infrastruktura

- Indeksy Dataview i oś czasu: `70-Indexes/`. Eventy mają tag `timeline` (wymóg pluginu), miejsca pole `coordinates` (Map View).
- Metadata Menu fileClasses: `00-Meta/fileClasses/` — aktualizuj razem ze zmianą schematu.
- `obsidian-local-rest-api/data.json` **gitignored** (żywy klucz API + TLS) — patrz `README-SECRETS.md` obok. Po świeżym klonie plugin generuje nowy klucz; konfig MCP przez `${OBSIDIAN_API_KEY}`, nie hardcoded.
- Otwieranie Obsidiana w WSLg: `nohup obsidian --no-sandbox > /tmp/obsidian.log 2>&1 & disown`
