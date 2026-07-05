# 00_index — Mapa Projektu

**Co to jest:** jedno miejsce, które mówi co jest gdzie. Otwierasz to na starcie sesji i pokazujesz komuś, kto pyta "co tu się dzieje".
**Ostatnia aktualizacja:** [Data]

## Jak czytać numerację (pasma dziesiątek = kategoria)

| Pasmo | Kategoria | Typ plików |
|---|---|---|
| **00–06** | Sterowanie bieżące | żywe (nadpisywane) + księgi (dopisywane) |
| **08–10** | Fundament / wizytówka | stałe, rzadko ruszane |
| **11–19** | Strategia / Roadmapa | aktualne |
| **20–29** | Architektura / infrastruktura | stałe |
| **30–39** | Referencje / szablony / guidelines | pomocnicze (stały warsztat) |
| **40–49** | Case studies | archiwalne |
| **50–59** | Plany wykonawcze 1 | aktualne |
| **60–69** | Plany wykonawcze 2 | historyczne |

> **Żywe vs Księgi.** Pliki **żywe** (`00_now`, `01_backlog`) pokazują STAN OBECNY — są nadpisywane, stare rzeczy z nich znikają. Pliki **księgi** (`02_worklog`, `03_sessions`, `04_decisions`) są tylko DOPISYWANE — nigdy nie tracą historii.

---

## 00–06 · Sterowanie bieżące
- [00_index.md](00_index.md) — ta mapa.
- [00_now.md](00_now.md) — status projektu tu i teraz *(żywy)*.
- [01_backlog.md](01_backlog.md) — co do zrobienia, wg faz *(żywy)*.
- [02_worklog.md](02_worklog.md) — **co już zrobione** (rosnąca lista wygranych) *(księga)*.
- [03_sessions.md](03_sessions.md) — log sesji: sukcesy/problemy/cel *(księga)*.
- [04_decisions.md](04_decisions.md) — decyzje i ADR *(księga)*.
- [05_idee.md](05_idee.md) — bank pomysłów na przyszłość.
- [06_backlog_archiwum.md](06_backlog_archiwum.md) — archiwum starych backlogów.

## 08–10 · Fundament / Wizytówka
- [08_zasady_pracy.md](08_zasady_pracy.md) — żelazne zasady współpracy PM ↔ AI.
- [09_one_pager.md](09_one_pager.md) — jednostronicowa wizytówka (dla sponsora/klienta).
- [10_project_charter.md](10_project_charter.md) — główna karta projektu (cele, zakres).

## 11–19 · Strategia / Roadmapa
- [11_roadmap.md](11_roadmap.md) — roadmapa faz projektu.

## 30–39 · Referencje / szablony (Stały warsztat techniczny)
- [30_paos_perplexity_guidelines.md](30_paos_perplexity_guidelines.md)
- [31_summarizer_template.md](31_summarizer_template.md)
- [32_prompt_seed_generator_vscode.md](32_prompt_seed_generator_vscode.md)
- [33_n8n_mcp_bridge_setup.md](33_n8n_mcp_bridge_setup.md)

> **Zasada:** każdy nowy plik w głównym katalogu dostaje numer wg pasma powyżej i wpis w tym indeksie. Numery bez indeksu gniją — indeks jest prawdziwym systemem.
