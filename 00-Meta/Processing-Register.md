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

## Duże tomy — stan przeszukania

Przeniesione z `projekty/Parzonko/CLAUDE.md` 2026-09-24. Stan na 2026-08-26 (sprawdź `ocr_quality` w notatce źródłowej przed założeniem, że coś jest nadal nieprzetworzone — ta lista bywa nieaktualna):

**WAŻNE — błędne liczby stron w kilku notatkach źródłowych**: pola `pages:` dla `BU 1069_60 t2` (błędnie "792") i `Bi 012_1230 t4` (błędnie "268") były pomyłkami sprzed miesięcy — **zawsze sprawdź `pdfinfo <plik>.pdf | grep Pages` zanim założysz, że tom ma nieprzejrzany ogon setek stron**. Skorygowane 2026-08-26: obie te "duże, nieprzetworzone" pozycje okazały się mieć dużo mniej realnych stron PDF, którym już dawno zrobiono tesseract — grep-sweep (wąski + szeroki) objął więc CAŁY dokument, nie próbkę.

- `BU 1069_60 t2` (396 str. — skorygowano z "792") — **wyczerpany**: 244/244 str. przez API + 152/152 pozostałych przez tesseract, oba przebiegi grep na całości → nowa treść: trzecie wystąpienie zarzutu "Miecz i Pług" (str.359-373), reszta zgodna z już znanym materiałem.
- `Bi 012_1230 t4` (143 str. — skorygowano z "268") — **wyczerpany**: oba przebiegi grep na całości (143/143 str.) → 35+81 trafień, wszystkie istotne przejrzane (nowe: imiona dziadków ojczystych str.31, formalne zamknięcie sprawy str.137, Grodzki "na usługach gestapo" str.130).
- `BU_0_189_38_t3` (218 str., potwierdzone pdfinfo) — oba przebiegi grep → ~46 trafień przejrzanych (nowe: ucieczka Grodzkiego do NRD str.211, sprzeczna data urodzenia Kamińskiego str.31, ujęcie Białowąsa str.208). Pozostałe ~172 str. bez trafień słów kluczowych: próbkowano bezpośrednim odczytem (str.0,99,149,213-216) — końcówka tomu (str.213-215) to **tabele zbiorcze statystyk bandy** (132 zamordowanych, 32 napady wg lat/kategorii, dodano do notatki) oraz dosłowny cytat listu "Huzara" z 21.XII.1951 (str.99-100, ujawnia kryptonim "Zyndram" dla Terlikowskiego). Środkowa część (str.100-210 poza trafieniami) to w większości inwentarze broni i raporty werbunkowe pobocznych meliniarzy — niska wartość dalszego pełnego odczytu, ale nie wykluczone pojedyncze cenne fragmenty jak wyżej.
- `Bi 012_1230 t2` (39 str., jakość OCR "poor") — 2026-08-26: odczytano bezpośrednio obrazem (Claude czyta png sam — dokładniejsze i tańsze niż wywoływanie `vision_ocr.py`/API) strony 1,2,4-13,17-19,22,26,30-34; strony 14,15,16,20 oraz 3 (poza kartą tytułową) pozostają nieprzeczytane. Treść wszystkich odczytanych stron to pełny "Wykaz oddziału Huzara" (biogramy ok. 10 pobocznych członków bandy — Butkiewicz, Kryński, bracia Dybowscy, Łapiński, Brzozowski i in.) oraz ogólna historia bandy — **żadna nowa treść o Parzonce poza już znaną str.30 i str.36**; jeden nowy fakt uboczny o Grodzkim (matka, siostry, chronologia ucieczki 1948-49 — patrz jego notatka). Deprioretyzować dalszy odczyt — wzorzec treści (biogramy figurantów bez własnych notatek) jest już jasny.

Już w pełni przetworzone (usunięte z listy 2026-08-26): `BU 01251_41_J` (372 str., wszystkie 147 str. ze wzmiankami o głównych postaciach przejrzane), `BU 1069_60 t1` (157/157 str.), `Bi 012_1230 t1/t3` (89/42 str.).

Pozostały potencjalny cel: ok. 150 nieprzejrzanych stron `BU_0_189_38_t3` (środek tomu, str.100-210 poza trafieniami słów kluczowych) — rozszerzona próbka (str.119-120, 158-159, 179-180, 195-196, 2026-08-26) potwierdza wzorzec: numerowana lista ofiar (zbieżna z już wyciągniętą tabelą zbiorczą 132/32), potrójnie potwierdzone dane Grodzkiego, narracja operacyjna "gry" już udokumentowana, oraz odrębna "Charakterystyka nr 37" z 1976 r. z ogólną historią AK Białostocczyzny bez związku z Parzonką. **Dalszy pełny odczyt niskiego priorytetu** — wzorzec treści jasny, brak śladu nieodkrytych faktów o głównym bohaterze; warty powrotu tylko przy konkretnym pytaniu badawczym (np. szukanie konkretnego nazwiska z innej notatki).
