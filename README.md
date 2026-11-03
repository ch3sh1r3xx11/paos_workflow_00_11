# PAOS: Project Artifacts Operating System

Szablon plików 00–11 i skill `/praca`, które utrzymują ciągłość pracy i kontekst projektu przez miesiące pracy z agentami AI. Cała prawda o projekcie leży w plikach, nie w historii czatu, więc nowa sesja zaczyna od przeczytania kilku plików zamiast od tłumaczenia wszystkiego od nowa.

## Jak zacząć

1. Skopiuj pliki z tego repo do swojego projektu, np. do folderu `docs/`.
2. Uzupełnij `10_project_charter.md` i `00_now.md`.
3. Przekaż agentowi `08_zasady_pracy.md` i każ mu zaczynać każdą sesję od `00_index.md`, `00_now.md` i `01_backlog.md`.
4. Na koniec sesji niech dopisze wpis do `03_sessions.md`, a zrobione zadania do `02_worklog.md`.

Kroki 3 i 4 automatyzuje skill `/praca` dla Claude Code (niżej).

## Pliki

| Plik | Do czego służy | Typ |
|---|---|---|
| `00_index.md` | mapa projektu i zasady numeracji | żywy |
| `00_now.md` | stan tu i teraz | żywy |
| `01_backlog.md` | co jest do zrobienia | żywy |
| `02_worklog.md` | co już zrobione | księga |
| `03_sessions.md` | log sesji: sukcesy, problemy, cel | księga |
| `04_decisions.md` | decyzje i ich powody | księga |
| `05_idee.md` | bank pomysłów | pomocniczy |
| `06_backlog_archiwum.md` | stare backlogi | pomocniczy |
| `08_zasady_pracy.md` | zasady współpracy człowieka z AI | stały |
| `09_one_pager.md` | jednostronicowa wizytówka | stały |
| `10_project_charter.md` | karta projektu: cele i zakres | stały |
| `11_roadmap.md` | fazy projektu | aktualizowany |

**Żywe** pliki nadpisujesz, bo pokazują stan obecny. **Księgi** tylko dopisujesz, więc historia nigdy nie ginie. Każdy nowy plik dostaje numer według pasma z `00_index.md` i wpis w tym indeksie.

## Skill `/praca` (Claude Code)

W `.claude/skills/praca/SKILL.md` leży skill, który automatyzuje start i koniec sesji:

- `/praca start`: agent czyta `00_index.md`, `00_now.md`, `01_backlog.md` i ostatni wpis sesji, sprawdza, czy pliki zgadzają się z rzeczywistością, i daje krótki briefing.
- `/praca koniec`: agent dopisuje wpis sesji i zrobione zadania do ksiąg, aktualizuje pliki żywe i decyzje.

Instalacja: skopiuj folder `.claude/skills/praca` do swojego projektu (albo do `~/.claude/skills/`, żeby działał wszędzie). Skill ma `disable-model-invocation: true`, więc uruchamiasz go tylko Ty, wpisując komendę; agent nie zamknie sesji sam.

## Licencja

[MIT](LICENSE): możesz używać, zmieniać i rozpowszechniać ten szablon, także komercyjnie, zachowując informację o licencji.
