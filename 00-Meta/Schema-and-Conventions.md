---
type: meta
title: "Schemat i konwencje vaulta Parzonko"
tags:
  - type/meta
---

# Schemat i konwencje vaulta Parzonko

Ten dokument jest jedynym źródłem prawdy dla struktury folderów, schematu YAML, zasad identyfikatorów, tagowania, nazewnictwa plików i cytowania stron w tym vault. Wszystkie notatki generowane w kolejnych etapach muszą być z nim spójne.

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
80-Media/      — kopie lub linki do plików binarnych, zdjęć, skanów i załączników, jeśli są potrzebne.
99-Archive/    — duplikaty, wersje zastąpione lub materiały wymagające ręcznej decyzji. Niczego nie usuwaj bez wyraźnego polecenia użytkownika.
```

## Zasada nadrzędna: źródło ponad narracją

Nie wolno tworzyć faktów bez podstawy w materiale źródłowym. Dla każdego istotnego twierdzenia biograficznego musi być możliwe przejście do: notatki wydarzenia → notatki źródłowej → pliku oryginalnego → strony/zakresu stron → cytatu.

Niepewne/sprzeczne/przypuszczalne informacje:
- oznacz jako niepewne,
- opisz źródło niepewności,
- podaj wszystkie konkurencyjne wersje,
- nie wybieraj jednej wersji bez wyjaśnienia.

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
### Strona 1
[Tekst wyodrębniony lub OCR.]
### Strona 2
[Tekst wyodrębniony lub OCR.]

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
  - status/verified
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
  - status/verified
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

---

## Zasady stabilnych identyfikatorów dla MCP i AI

Formaty: `SRC-...`, `PERSON-...`, `PLACE-...`, `EVENT-...`, `TOPIC-...`, `BIO-...`.

Przykłady: `SRC-IPN-GK-123-45`, `PERSON-001`, `PLACE-WARSZAWA`, `EVENT-1944-ARREST-001`, `BIO-PERSON-001`.

Zasady:
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
| Biografia | umieszczona w `10-Biography/`, tytuł opisowy | `Biografia-Jana-Kowalskiego.md` |

## Zasady cytowania stron

- Każde odniesienie do źródła w polu `sources` wydarzenia powinno wskazywać konkretną stronę lub zakres stron, np. `"SRC-IPN-GK-123-45#p3"` lub `"SRC-IPN-GK-123-45#p3-4"`.
- W treści notatki źródłowej cytaty istotne muszą podawać numer strony (`Źródło: strona 3.`).
- Nie cytuj ani nie twierdź bez wskazania konkretnej strony/zakresu stron w dokumencie źródłowym.
