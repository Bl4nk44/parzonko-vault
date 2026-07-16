# Vault Parzonko (Obsidian)

To jest **vault**, wynikowa baza wiedzy. Pipeline OCR/skrypty i pełny opis workflow są w osobnym repo: `/home/ubuntu/projekty/Parzonko/CLAUDE.md` — przeczytaj to najpierw, ten plik jest tylko uzupełnieniem specyficznym dla tego repo.

## Jedyne źródło prawdy dla schematu

`00-Meta/Schema-and-Conventions.md` — struktura folderów, pola YAML, konwencje UID, tagowanie, cytowanie stron, zasady konfliktów. Nie zgaduj schematu z przykładów w innych notatkach — sprawdź tam.

## Rejestr stabilnych ID

`00-Meta/uid-registry.json` — czytany/pisany przez `scripts/uid_registry.py` z drugiego repo. Nigdy nie edytuj ręcznie, nigdy nie przydzielaj UID bez `allocate()`.

## Local REST API / MCP

Plugin `obsidian-local-rest-api` skonfigurowany, `.obsidian/plugins/obsidian-local-rest-api/data.json` **gitignored** (zawiera żywy klucz API + klucz prywatny TLS) — patrz `README-SECRETS.md` w tym samym folderze. Po świeżym klonie/regeneracji klucza trzeba zaktualizować konfigurację MCP (`claude mcp add obsidian ...` w sesji Claude Code, referencja `${OBSIDIAN_API_KEY}` z `~/.zshrc`, nie hardcoded).

## Kluczowe zasady (skrót — pełne uzasadnienie w drugim CLAUDE.md)

- `#status/verified` — **tylko człowiek nadaje**, nigdy AI.
- Pełny tekst OCR → `80-Media/ocr/`, notatka źródłowa zostaje lekka.
- Wynik `vision_ocr.py` (fallback dla pisma odręcznego) → zawsze krzyżowa weryfikacja przed wpisaniem faktu, potwierdzona halucynacja w historii tego projektu (podstawiony protokół egzekucji Fieldorfa zamiast realnej treści strony).
- Nie scalaj osób po samej zgodności imienia/nazwiska.
- Przed każdym commitem sprawdź martwe wikilinki (komenda w drugim CLAUDE.md).

## Otwieranie aplikacji Obsidian (WSLg)

```bash
nohup obsidian --no-sandbox > /tmp/obsidian.log 2>&1 & disown
```
