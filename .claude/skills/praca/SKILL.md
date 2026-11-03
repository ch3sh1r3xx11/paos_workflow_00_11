---
name: praca
description: Uniwersalny rytuał sesji projektowej (system żywe pliki/księgi w docs/). "/praca start": wczytaj panel sterowania, zweryfikuj z rzeczywistością, daj briefing; "/praca koniec": dopisz do ksiąg, zaktualizuj pliki żywe i pamięć. Uruchamia WYŁĄCZNIE PM, wpisując /praca, nigdy Claude sam.
disable-model-invocation: true
---

# Skill: /praca: uniwersalny rytuał sesji

Prawda leży na dysku w `docs/` bieżącego projektu, nie w kontekście czatu. Ten skill utrzymuje ją aktualną i archiwizowaną. Działa w każdym projekcie, który stosuje ten sam system plików (pasma numeracji, żywe vs księgi: patrz niżej).

**Tryby:** argument `start` albo `koniec`. Jeśli PM nie poda: zapytaj który. Nie zgaduj z kontekstu i nie uruchamiaj trybu `koniec`, dopóki PM sam go nie wpisze.

## Fundament, o którym musisz pamiętać

- **Pliki żywe** (`00_now.md`, `01_backlog.md`) = STAN OBECNY, nadpisywane.
- **Pliki księgi** (`02_worklog.md`, `03_sessions/YYYY-MM.md`, `04_decisions.md`) = HISTORIA, **tylko dopisywane, NIGDY nie kasuj wpisów**.
- **Mapa wszystkiego:** `docs/00_index.md`. Każdy nowy plik w `docs/` = numer wg pasma + wpis w indeksie.
- **Czas:** zawsze Europe/Warsaw.
- Jeśli projekt ma plik zasad (np. `docs/08_zasady_pracy.md` / `docs/10_zasady_pracy.md`): trzymaj się go (styl współpracy, strażnik monetyzacji/wartości, anty-overengineering, "krok po kroku").
- **Jeśli projekt NIE ma jeszcze tej struktury** (brak `docs/00_index.md`): zapytaj PM-a, czy założyć ją od zera (skopiować szkielet 00-11) zamiast zgadywać.

---

## TRYB: `/praca start`

1. **Wczytaj panel sterowania** (przeczytaj w tej kolejności, pomiń brakujące pliki):
   - `docs/00_index.md` (mapa: co gdzie jest)
   - `docs/00_now.md` (gdzie jesteśmy)
   - `docs/01_backlog.md` (co do zrobienia)
   - ostatni wpis sesji: `tail -n 25` na najnowszym pliku w `docs/03_sessions/` (nie czytaj całego). Stary układ bez folderu → `head -n 30 docs/03_sessions.md`.
   - pamięć długoterminowa (`MEMORY.md` / auto-memory, jeśli dostępna)
2. **Zweryfikuj z rzeczywistością** (pliki bywają nieaktualne):
   - Czy daty/statusy w `00_now` się zgadzają? Czy coś oznaczone "w toku" mogło się zmienić w innym wątku/gałęzi?
   - Jeśli coś wygląda na przeterminowane lub sprzeczne: **zgłoś to PM-owi jako pytanie**, nie zakładaj.
3. **Daj briefing (max ~8 linii):** gdzie jesteśmy · 2–3 rzeczy na dziś (z celu poprzedniej sesji + backlogu) · co blokuje · ewentualne rozjazdy do wyjaśnienia.
4. Zapytaj PM-a: "od czego zaczynamy?" i czekaj.

---

## TRYB: `/praca koniec`

Wykonaj po kolei (potwierdzenie PM-a przy wątpliwościach).

**Oszczędność tokenów (twarde):** każde wywołanie narzędzia przesyła cały kontekst rozmowy, a księgi rosną bez końca.
- Treść sesji bierzesz z rozmowy, **nie czytasz ksiąg w całości**. Do ksiąg dopisujesz przez Bash (`cat >> plik <<'EOF'`), bez Read.
- Gdy Edit jest konieczny: Read z `limit` tylko na fragment, który zmieniasz.
- Nie czytasz plików ponownie „dla sprawdzenia”. Edit/Write zgłosi błąd, jeśli się nie udało.
- Wpis sesji max ~12 linii. Robisz zmiany możliwie małą liczbą wywołań (niezależne równolegle).

1. **Dopisz wpis sesji na KONIEC** pliku miesięcznego `docs/03_sessions/YYYY-MM.md` (Bash `>>`, bez czytania). Brak pliku na ten miesiąc → utwórz z nagłówkiem `# Sesje <PROJEKT>: YYYY-MM`. Brak folderu, a jest stary `docs/03_sessions.md` → **nie czytaj go**, załóż folder i plik miesięczny, dopisz w `00_index.md`; podział starego pliku to osobne zadanie, tylko na prośbę PM-a.
   ```
   ## Sesja: YYYY-MM-DD (pora dnia): tytuł
   - **Sukcesy:** ...
   - **Problemy:** ...
   - **Ważne decyzje:** ... (jeśli trwałe → też do 04_decisions.md)
   - **Cel na następną sesję:** ...
   ```
2. **Dopisz ukończone zadania** w `docs/02_worklog.md` (Read z `limit` ~30 na nagłówek z licznikiem i górę listy, Edit tam) i **zaktualizuj licznik** ("Licznik: N ukończonych"). Format: `- [YYYY-MM-DD] opis (obszar)`. Tu tylko suche "zrobione", narracja idzie do sesji.
   - Jeśli projekt taguje zadania wg modelu/agenta (patrz plik zasad, np. `[Opus]`/`[Sonnet]`/`[AGY]`): nowe zadania w backlogu też taguj.
3. **Zaktualizuj pliki żywe:**
   - `docs/00_now.md`: nowy stan bieżący. **UWAGA (higiena międzywątkowa):** jeśli plik ma osobne sekcje per nurt/wątek, aktualizuj TYLKO sekcję swojego wątku: nie kasuj i nie nadpisuj sekcji drugiego (może być świeższa, z równoległej sesji).
   - `docs/01_backlog.md`: oznacz zrobione, dodaj nowe zadania.
4. **Decyzje trwałe** → dopisz do `docs/04_decisions.md` (jeśli padły), nowe na górze: Read z `limit` ~10 (nagłówek do pierwszego `---`), Edit zaraz pod nim. Nie czytaj reszty pliku.
5. **Pamięć**: jeśli padły trwałe fakty (nie tylko-tej-sesji): zaktualizuj plik(i) pamięci długoterminowej. Nie duplikuj tego, co już jest w `docs/`.
6. **Nowe pliki w `docs/`?** → nadaj numer wg pasma (patrz `00_index.md`) i dopisz wpis do `00_index.md`.
7. **Archiwizacja (raz w tygodniu LUB przy większej przebudowie):** skopiuj `docs/01_backlog.md` do `docs/archive/backlog_YYYY-MM-DD.md`. Nie rób tego codziennie: to ma być lekkie, nie hałas.
8. **Podsumuj PM-owi w 3 liniach:** co zapisane, licznik worklog, cel na następną sesję.

---

## Zasady twarde

- Księgi (`02_worklog`, `03_sessions`, `04_decisions`): **append-only**. Jeśli musisz poprawić stary wpis, dopisz korektę z datą, nie nadpisuj.
- Nie rób "cichej" aktualizacji dużej liczby plików bez powiedzenia PM-owi co zmieniasz.
- Przy przenazwaniu/przenoszeniu plików: najpierw backup (brak gita = brak cofnięcia), potem aktualizuj linki, potem weryfikuj że nic nie wisi.
