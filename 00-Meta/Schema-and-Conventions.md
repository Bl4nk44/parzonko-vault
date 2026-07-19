---
type: meta
title: "Schemat i konwencje vaulta Parzonko"
tags:
  - type/meta
---

# Schemat i konwencje vaulta Parzonko

Ten dokument jest jedynym źródłem prawdy dla struktury folderów, schematu YAML, zasad identyfikatorów, tagowania, nazewnictwa plików i cytowania stron w tym vault. Wszystkie notatki generowane w kolejnych etapach muszą być z nim spójne.

**Spis treści:**
- [Struktura folderów](#struktura-folderów)
- [Zasada nadrzędna: źródło ponad narracją](#zasada-nadrzędna-źródło-ponad-narracją)
- [Notatka źródłowa (20-Sources/)](#notatka-źródłowa-20-sources)
- [Notatka osoby (40-People/)](#notatka-osoby-40-people)
- [Notatka miejsca (50-Places/)](#notatka-miejsca-50-places)
- [Notatka wydarzenia (30-Events/)](#notatka-wydarzenia-30-events)
- [Biografia (10-Biography/)](#biografia-10-biography)
- [Zasady stabilnych identyfikatorów dla MCP i AI](#zasady-stabilnych-identyfikatorów-dla-mcp-i-ai)
- [Zasady tagowania](#zasady-tagowania)
- [Obsługa konfliktów źródłowych](#obsługa-konfliktów-źródłowych)
- [Cytaty w innych językach](#cytaty-w-innych-językach)
- [Dopuszczalne wartości pól wspólnych](#dopuszczalne-wartości-pól-wspólnych)
- [Zasady nazewnictwa plików (podsumowanie)](#zasady-nazewnictwa-plików-podsumowanie)
- [Zasady cytowania stron](#zasady-cytowania-stron)

## Struktura folderów

```text
00-Meta/       — opis vaulta, schemat danych, zasady, rejestry kontrolne.
10-Biography/  — syntetyczna biografia głównej osoby.
20-Sources/    — pojedyncze notatki źródłowe, po jednej na dokument lub jednostkę archiwalną.
30-Events/     — atomowe wydarzenia z życia przodka.
40-People/     — osoby: przodek, rodzina, świadkowie, urzędnicy, współwięźniowie itd.
50-Places/     — miejscowości, adresy, więzienia, obozy, urzędy i inne lokalizacje.
60-Topics/     — notatki tematyczne, np. działalność konspiracyjna, pobyt w więzieniu, służba wojskowa.
70-Indexes/    — indeksy, chronologie, mapy treści i punkty wejścia.
80-Media/      — pełny tekst OCR, skany, załączniki (patrz podfoldery niżej).
99-Archive/    — duplikaty, wersje zastąpione lub materiały wymagające ręcznej decyzji. Niczego nie usuwaj bez wyraźnego polecenia użytkownika.
```

### Podfoldery `80-Media/` (od Task 9, poprawka po przetworzeniu pierwszych 8 dokumentów)

```text
80-Media/
  ocr/           — pełny tekst OCR strona po stronie, jeden plik .md na dokument źródłowy,
                   ta sama nazwa pliku co odpowiadająca notatka w 20-Sources/ (bez folderu).
                   NIE wklejaj pełnego OCR do notatki źródłowej — patrz sekcja "Tekst źródłowy" niżej.
  originals/     — (opcjonalnie, jeśli kiedyś potrzebne) kopie plików oryginalnych; domyślnie
                   oryginały PDF/DOC zostają tylko na dysku poza vaultem (gitignored, patrz repo
                   pipeline), ten podfolder istnieje jako miejsce docelowe gdyby trzeba było
                   skopiować pojedynczy plik do wglądu.
  derivatives/   — renderowane obrazy stron (np. do wglądu przy niepewnym OCR), jeśli potrzebne.
```

**Powód tej zmiany:** projekt docelowo ma wielu współpracowników. Pełny OCR wklejony do każdej notatki źródłowej (jak robiono w pierwszych 8 dokumentach) nadmiernie powiększa notatki, utrudnia review w Git i miesza "materiał roboczy" (surowy OCR) z "syntezą" (streszczenie, cytaty, linki) w jednym pliku. Notatka źródłowa ma być czytelna dla człowieka w 1-2 ekrany; pełny tekst źródłowy zawsze dostępny pod linkiem.

## Zasada nadrzędna: źródło ponad narracją

Nie wolno tworzyć faktów bez podstawy w materiale źródłowym. Dla każdego istotnego twierdzenia biograficznego musi być możliwe przejście do: notatki wydarzenia → notatki źródłowej → pliku oryginalnego → strony/zakresu stron → cytatu.

Niepewne/sprzeczne/przypuszczalne informacje:
- oznacz jako niepewne,
- opisz źródło niepewności,
- podaj wszystkie konkurencyjne wersje,
- nie wybieraj jednej wersji bez wyjaśnienia.

### Vision OCR (`scripts/vision_ocr.py`) — obowiązkowa weryfikacja krzyżowa

Dla stron nieczytelnych przez tesseract (pismo odręczne, zniszczony maszynopis) dostępne jest narzędzie awaryjne wywołujące model wizyjny (Mistral Large przez OpenRouter). **Potwierdzone ryzyko halucynacji** (2026-07-16): na realnej stronie z korpusu model podstawił płynny, wewnętrznie spójnie brzmiący tekst prawdziwego, ale kompletnie niepowiązanego, dobrze udokumentowanego protokołu egzekucji (inna, znana z historii sprawa) zamiast faktycznie odczytać zniszczoną treść. Wykryto tylko dzięki wewnętrznej sprzeczności dat w zwróconym tekście i porównaniu numeru sprawy z sąsiednimi stronami.

**Zasada:** wynik `vision_ocr.py` nigdy nie jest samodzielną podstawą faktu w polach YAML notatki. Przed wpisaniem do vaulta wymagana weryfikacja: (1) spójność wewnętrzna zwróconego tekstu, (2) zgodność numerów spraw/dat/sygnatur z sąsiednimi stronami tego samego dokumentu, (3) czy wymienione osoby/wydarzenia pasują do kontekstu sprawy, czy przypominają inną, znaną sprawę (czerwona flaga halucynacji: model "rozpoznał typ dokumentu" i podstawił zapamiętany tekst). Wynik niepotwierdzony → sekcja "Niepewności" z blockquote "Hipoteza robocza", nigdy pole YAML wprost.

---

## Notatka źródłowa (20-Sources/)

**Nazwa pliku:** `[Źródło]-[sygnatura-lub-ID]-[krótki-opis].md`

Przykłady:
- `IPN-GK-123-45-Protokol-przesluchania-1946.md`
- `Archiwum-Rodzinne-List-do-zony-1944.md`
- `Prasa-Kurier-Warszawski-1947-05-12.md`

### YAML

```yaml
---
type: source
uid: "SRC-UNIQUE-STABLE-ID"
source_id: "IPN-GK-123-45"
title: "Pełny tytuł dokumentu lub jednoznaczny opis"
source_type: "akta IPN"
archive: "IPN"
call_number: "GK 123/45"
date_document: "1946-03-12"
date_accuracy: "day"
place_document: "Warszawa, Polska"
language:
  - pl
pages: 12
original_filename: "oryginalna-nazwa-pliku.pdf"
original_path: "/pełna/ścieżka/do/pliku.pdf"
ocr_file: "[[80-Media/ocr/IPN-GK-123-45-Protokol-przesluchania-1946]]"
reliability: "primary"
ocr_quality: "good"
main_person: "PERSON-001"
people_mentioned: []
places_mentioned: []
organizations_mentioned: []
related_events: []
tags:
  - type/source
  - source/ipn
  - status/unreviewed
---
```

Dopuszczalne wartości `reliability`:
- `primary` — źródło pierwotne (protokół, list, dokument urzędowy, akt sprawy)
- `secondary` — opracowanie, wspomnienie, artykuł, relacja późniejsza
- `uncertain` — pochodzenie lub wiarygodność niepewne

### Treść notatki źródłowej (struktura markdown po YAML)

```markdown
# [Tytuł dokumentu]

## Opis dokumentu
Krótki opis po polsku: czym jest dokument, kiedy powstał, kto go stworzył, czego dotyczy, dlaczego jest ważny dla biografii przodka.

## Najważniejsze ustalenia
- [Fakt lub obserwacja] → [[Event-...]]
- [Fakt lub obserwacja] → [[Person-...]]
- [Fakt lub obserwacja] → [[Place-...]]

## Osoby
- [[Person-Imie-Nazwisko]]

## Miejsca
- [[Place-...]]

## Powiązane wydarzenia
- [[Event-1944-Aresztowanie]]

## Tekst źródłowy
Pełny tekst OCR strona po stronie przeniesiony do osobnego pliku: [[80-Media/ocr/NAZWA-TEJ-NOTATKI]].
Najważniejsze cytaty pozostają poniżej, w sekcji "Cytaty istotne".

(Plik `80-Media/ocr/NAZWA-TEJ-NOTATKI.md` ma tę samą nazwę co ta notatka źródłowa, zawiera
pełny tekst strona po stronie w formacie `### Strona N` / treść, dokładnie jak dawny wzorzec
tej sekcji poniżej — po prostu w osobnym pliku, nie w notatce syntetycznej.)

## Cytaty istotne
> Cytat z dokumentu.
Źródło: strona 3.

## Uwagi o jakości i niepewności
- Jakość OCR: dobra / średnia / słaba.
- Nieczytelne fragmenty: ...
- Warianty nazwiska: ...
- Możliwe błędy w dokumencie: ...
```

---

## Notatka osoby (40-People/)

**Nazwa pliku:** `Person-[Nazwisko]-[Imię]-[rok-urodzenia].md`

### YAML

```yaml
---
type: person
uid: "PERSON-001"
person_id: "PERSON-001"
full_name: "Jan Kowalski"
given_names:
  - Jan
surname: "Kowalski"
aliases:
  - "Jan K."
  - "Pseudonim X"
gender: "M"
birth_date: "1912-04-18"
birth_date_accuracy: "day"
birth_place: "PLACE-001"
death_date: null
death_date_accuracy: "unknown"
death_place: null
nationality: "polska"
occupation: []
roles: []
related_to_main_person: "self"
related_persons: []
key_sources: []
certainty: "high"
tags:
  - type/person
  - status/unreviewed
---
```

Dopuszczalne wartości `related_to_main_person`: `self`, `family`, `witness`, `official`, `associate`, `unknown`.

### Treść notatki osoby

Sekcje:
- `## Podsumowanie`
- `## Dane podstawowe` (Data urodzenia, Miejsce urodzenia, Data śmierci, Role, Pseudonimy)
- `## Relacje` (Ojciec/Matka/Małżonek/Dzieci jako wikilinks)
- `## Chronologia życia` (lista rok → wikilink eventu)
- `## Najważniejsze źródła` (wikilink → str. X-Y)
- `## Niepewności i sprzeczności`

---

## Notatka miejsca (50-Places/)

**Nazwa pliku:** `Place-[Nazwa-Miejsca].md`

### YAML

```yaml
---
type: place
uid: "PLACE-001"
place_id: "PLACE-001"
name: "Warszawa"
alternative_names: []
country: "Polska"
historical_administrative_unit: null
coordinates: null
certainty: "high"
tags:
  - type/place
---
```

### Treść notatki miejsca

Sekcje:
- `## Znaczenie dla biografii`
- `## Powiązane wydarzenia`
- `## Powiązane osoby`
- `## Źródła`

---

## Notatka wydarzenia (30-Events/)

**Nazwa pliku:** `Event-[data]-[krótki-opis].md`

Jedna notatka = jedno konkretne zdarzenie (narodziny, aresztowanie, przesłuchanie, transport, osadzenie, zwolnienie, wyrok, śmierć, itd. — NIE tematy zbiorcze typu "II wojna światowa").

### YAML

```yaml
---
type: event
uid: "EVENT-1944-001"
event_id: "EVENT-1944-001"
title: "Aresztowanie Jana Kowalskiego w Warszawie"
date: "1944-08-01"
date_accuracy: "day"
place: "PLACE-001"
main_person: "PERSON-001"
people_involved:
  - "PERSON-001"
  - "PERSON-014"
category: "arrest"
sources:
  - "SRC-IPN-GK-123-45#p3"
  - "SRC-IPN-GK-123-45#p4"
certainty: "high"
tags:
  - type/event
  - event/arrest
  - topic/WWII
  - status/unreviewed
---
```

### Treść notatki wydarzenia

Sekcje:
- `## Opis`
- `## Przebieg`
- `## Osoby`
- `## Miejsce`
- `## Źródła`
- `## Sprzeczne relacje` (jeśli źródła się różnią — punktowo, z uzasadnieniem najbardziej prawdopodobnej wersji)
- `## Stopień pewności`

---

## Biografia (10-Biography/)

**Nazwa pliku:** `Biografia-[Imię-Nazwisko].md`

### YAML

```yaml
---
type: biography
uid: "BIO-PERSON-001"
person_id: "PERSON-001"
title: "Biografia Jana Kowalskiego"
language: "pl"
tags:
  - type/biography
  - status/in-progress
---
```

### Treść notatki biograficznej

Sekcje:
- `## Kim był`
- `## Najważniejsze fakty`
- `## Chronologia życia`
- `## Dzieciństwo i rodzina`
- `## Edukacja i praca`
- `## Okres wojny i okupacji`
- `## Aresztowanie, śledztwo lub represje`
- `## Życie po wojnie`
- `## Śmierć i pamięć`
- `## Niewyjaśnione kwestie`
- `## Kluczowe źródła`

---

## Zasady stabilnych identyfikatorów dla MCP i AI

Formaty: `SRC-...`, `PERSON-...`, `PLACE-...`, `EVENT-...`, `TOPIC-...`, `BIO-...`.

Przykłady z oryginalnej specyfikacji (poglądowe): `SRC-IPN-GK-123-45`, `PERSON-001`, `PLACE-WARSZAWA`, `EVENT-1944-ARREST-001`, `BIO-PERSON-001`.

> **WAŻNE — jedna, jednoznaczna zasada generowania `uid`:**
> Powyższe przykłady semantyczne (`PLACE-WARSZAWA`, `EVENT-1944-ARREST-001`, `SRC-IPN-GK-123-45`) pochodzą z oryginalnej specyfikacji i są **wyłącznie poglądowe** — pokazują format prefiksu, NIE sposób generowania. **Nigdy nie twórz ręcznie identyfikatora o wyglądzie semantycznym.** Jedyny poprawny sposób nadawania `uid` to zawsze wywołanie `uid_registry.py`'s `allocate()` (lub — po utworzeniu — rejestru JSON w `00-Meta/uid-registry.json`), które zwraca kolejny sekwencyjny identyfikator w formacie rejestru: `PERSON-001`, `PLACE-002`, `EVENT-1944-003`, `SRC-004`, itd. Subagent, który napotka przykład typu `PLACE-WARSZAWA`, ma go traktować jako historyczną ilustrację formatu, a nie wzorzec do naśladowania — zawsze pyta rejestr o kolejny wolny numer.
>
> **Kolejność w planie:** `uid_registry.py` i `00-Meta/uid-registry.json` powstają w Tasku 3 tego planu, przed jakimkolwiek generowaniem realnych notatek merytorycznych (Task 8/9). Ta zasada zaczyna obowiązywać w praktyce dopiero gdy rejestr istnieje — nie ma potrzeby ręcznego trybu tymczasowego, bo żaden dokument nie jest przetwarzany zanim Task 3 się zakończy.

Zasady:
- zawsze alokuj `uid` przez `uid_registry.py` / `00-Meta/uid-registry.json` — nigdy ręcznie;
- nigdy nie zmieniaj istniejącego `uid`;
- nie generuj nowych identyfikatorów dla tej samej encji;
- używaj `uid` i dodatkowych pól YAML jako warstwy dla zapytań MCP/AI;
- używaj nazw plików oraz `[[wikilinks]]` dla wygody pracy użytkownika w Obsidianie;
- nie polegaj wyłącznie na nazwach plików jako identyfikatorach.

## Zasady tagowania

Tagi typów:
`#type/source #type/event #type/person #type/place #type/biography #type/topic #type/index #type/meta`

Tagi statusu:
`#status/verified #status/uncertain #status/conflict #status/unreviewed #status/requires-review #status/in-progress`

Tagi tematów (przykładowo):
`#topic/WWII #topic/occupation #topic/resistance #topic/arrest #topic/interrogation #topic/prison #topic/camp #topic/military #topic/family #topic/postwar`

Zasada: nie twórz wielu niemal identycznych tagów (np. `#aresztowanie #aresztowania #arrest #aresztowany` — wybierz jeden standard, np. `#topic/arrest`, i stosuj wszędzie).

**WAŻNE — `#status/verified` jest zarezerwowany dla człowieka.** Agent AI (w tym Claude Code) NIGDY nie nadaje samodzielnie tagu `#status/verified` — to oznacza "człowiek zweryfikował to ustalenie i potwierdza je". AI-owa ocena pewności wyraża się przez pole YAML `certainty: high/medium/low`, ale notatka mimo wysokiego `certainty` startuje z tagiem `#status/unreviewed`. Zmiana na `#status/verified` następuje wyłącznie przez świadomą akcję człowieka (np. w ramach code review / PR), nigdy automatycznie przy tworzeniu notatki. (Wprowadzone po Task 8/9 — pierwsze 3 notatki wydarzeń błędnie dostały `status/verified` nadany przez AI, poprawione na `status/unreviewed`.)

## Obsługa konfliktów źródłowych

Gdy źródła podają sprzeczne wersje tego samego faktu, postępuj wg tej procedury:

1. Opisz wszystkie wersje.
2. Wskaż źródła i strony dla każdej wersji.
3. Ustaw `certainty` odpowiednio niżej (`medium`/`low`).
4. Dodaj tag `#status/conflict`.
5. Wpisz konflikt do `Index-Conflicts.md` (w `70-Indexes/`), jeśli jest on istotny dla biografii.

Do opisu hipotezy roboczej w treści notatki (np. w sekcji `## Sprzeczne relacje` lub `## Niepewności i sprzeczności`) używaj dokładnie tego szablonu:

```markdown
> Hipoteza robocza:
> [opis]
>
> Podstawa:
> [[Źródło-1]] — str. X
> [[Źródło-2]] — str. Y
```

## Cytaty w innych językach

Cytaty w innym języku niż polski zachowuj w oryginale; pod cytatem dodaj krótkie tłumaczenie oznaczone jako `Tłumaczenie robocze AI:`; nigdy nie przedstawiaj tłumaczenia jako oryginalnego tekstu źródłowego.

## Dopuszczalne wartości pól wspólnych

- `date_accuracy` / `birth_date_accuracy` / `death_date_accuracy`: `day`, `month`, `year`, `unknown` (dokładność, z jaką znana jest data).
- `certainty`: `high`, `medium`, `low` (stopień pewności ustalenia/faktu).
- `reliability` (tylko źródła): `primary`, `secondary`, `uncertain`.
- `related_to_main_person` (tylko osoby): `self`, `family`, `witness`, `official`, `associate`, `unknown`.

## Zasady nazewnictwa plików (podsumowanie)

| Typ | Wzorzec | Przykład |
|-----|---------|----------|
| Źródło | `[Źródło]-[sygnatura-lub-ID]-[krótki-opis].md` | `IPN-GK-123-45-Protokol-przesluchania-1946.md` |
| Osoba | `Person-[Nazwisko]-[Imię]-[rok-urodzenia].md` | `Person-Kowalski-Jan-1912.md` |
| Miejsce | `Place-[Nazwa-Miejsca].md` | `Place-Warszawa.md` |
| Wydarzenie | `Event-[data]-[krótki-opis].md` | `Event-1944-08-01-Aresztowanie.md` |
| Biografia | `Biografia-[Imię-Nazwisko].md` | `Biografia-Jana-Kowalskiego.md` |

## Zasady cytowania stron

- Każde odniesienie do źródła w polu `sources` wydarzenia powinno wskazywać konkretną stronę lub zakres stron, np. `"SRC-IPN-GK-123-45#p3"` lub `"SRC-IPN-GK-123-45#p3-4"`.
- W treści notatki źródłowej cytaty istotne muszą podawać numer strony (`Źródło: strona 3.`).
- Nie cytuj ani nie twierdź bez wskazania konkretnej strony/zakresu stron w dokumencie źródłowym.

## Pluginy Obsidian i pola przez nie używane (dodane 2026-07-19)

Zainstalowane pluginy: Dataview, Timelines (Revamped), Map View, Metadata Menu, Linter, Omnisearch, Strange New Worlds, Various Complements. Indeksy Dataview żyją w `70-Indexes/`.

### Wydarzenia — oś czasu
- Każda notatka wydarzenia (`30-Events/`) ma w `tags` dodatkowy tag `timeline` (wymóg pluginu Timelines Revamped). Pole `date` służy jako data startowa eventu (klucz zmapowany w ustawieniach pluginu). Oś czasu: `70-Indexes/Os-Czasu.md`.

### Miejsca — mapa
- Pole `coordinates: [lat, lon]` (WGS84, z geokodowania Nominatim/OSM) używane przez Map View (`frontMatterKey` ustawiony na `coordinates`). Miejsca niejednoznaczne zostają z `coordinates: null` — nie zgaduj współrzędnych.

### Metadata Menu
- Definicje fileClass w `00-Meta/fileClasses/` (source/person/event/place), przypisane do folderów przez fileClassQueries w ustawieniach pluginu. Przy zmianie schematu w tym pliku zaktualizuj też odpowiedni fileClass.
