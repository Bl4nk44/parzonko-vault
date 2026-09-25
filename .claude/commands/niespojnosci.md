---
description: Systematyczny skan vaulta w poszukiwaniu niespójności danych (daty, osoby, chronologia, cytowania)
argument-hint: opcjonalnie zakres (osoba, rok, folder) — bez argumentu skan całości
---

Przeskanuj vault pod kątem niespójności. Zakres: **$ARGUMENTS** (pusty = cały vault). Raportuj, nie poprawiaj — poprawki dopiero po decyzji użytkownika.

Najpierw uruchom `cd /home/ubuntu/projekty/Parzonko && python3 -m scripts.vault_lint` — mechaniczne części klas 4–5
(martwe linki, nieznane UID-y, `certainty: high` przy jednym źródle, brak `ocr_file`, eventy bez `timeline`) są
policzone deterministycznie; wklej jego podsumowanie i skup analizę na klasach semantycznych.

Klasy niespójności do sprawdzenia (dla każdej podaj: gdzie, co się nie zgadza, sygnatury, proponowane działanie):

1. **Daty biograficzne** — ta sama osoba z różnymi `birth_date`/`death_date` między notatką w `40-People` a treścią źródeł/wydarzeń; daty z `_accuracy` niezgodną z formatem (dzień przy `accuracy: year`).
2. **Chronologia** — wydarzenia z udziałem osoby po jej `death_date`; sekwencje niemożliwe (awans przed wstąpieniem, zeznanie po egzekucji); sprzeczne datowania tego samego zdarzenia w różnych źródłach.
3. **Osoby** — potencjalne duplikaty (podobne nazwiska/pseudonimy w `40-People` — wypisz do ręcznej oceny, NIE scalaj); ta sama osoba pod różnymi pseudonimami bez odnotowania w `aliases`; osoba wymieniona w `people_mentioned`/`people_involved` bez notatki w `40-People`.
4. **Cytowania** — twierdzenia w notatkach bez `SRC-XXX, str. N`; `key_sources` wskazujące źródła, w których treści faktu nie widać (wyrywkowo, przy podejrzeniu); pola `related_events`/`key_sources` z UID-ami, które nie istnieją w `uid-registry.json`.
5. **Integralność struktury** — martwe wikilinki (komenda w CLAUDE.md); notatki bez wymaganych pól schematu; `#status/verified` na notatce zmienionej po dacie ostatniego review (git log); eventy bez tagu `timeline`; rozjazd `certainty` między notatką osoby a źródłami, na których wisi.
6. **Hipotezy robocze** — bloki „Hipoteza robocza", które nowsze źródła już rozstrzygnęły (porównaj z `00-Meta/Otwarte-Pytania-Badawcze.md`).

Techniki: grep po frontmatter, porównania dat skryptem (Python/bash na plikach md), indeksy w `70-Indexes/`. Na końcu: podsumowanie liczbowe per klasa + lista TOP problemów wg wagi (błędny fakt > brak cytowania > kosmetyka schematu).
