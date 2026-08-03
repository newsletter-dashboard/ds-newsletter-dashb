# UK Kings Prague — Content Playbook

Pracovní nástroj pro social media UK Kings Prague, sezóna 26/27. Statická jednosouborová webová appka (`index.html`) nasazená přes GitHub Pages — žádný backend, žádný build krok.

**Živá verze:** https://newsletter-dashboard.github.io/ds-newsletter-dashb/

## Co appka obsahuje

| Sekce | K čemu slouží |
|---|---|
| **Tento týden** | Landing view — počet naplánovaných výstupů, nejbližší zápas, hlavní úkol týdne, seznam obsahu na tento týden. |
| **Obsahový plán** | Realistické minimum obsahu (týden se zápasem / bez zápasu / „když není čas“) + kompletní backlog úkolů s filtry. |
| **Kalendář** | Přidání zápasů/náborů — appka sama doplní přípravu (7 dní/3 dny/den před, den akce, den po). |
| **Inside the Kings** | Definice hlavní obsahové série klubu. |
| **Tryout** | Náborová kampaň o 6 fázích, storyboard po sekundách, shotlist. |
| **Gameday** | Mobilní checklist na den zápasu (před/během/po). |
| **Výsledky** | Co sledovat a jak si nastavit cíl (baseline → cílová změna → období testu). |
| **Strategie** | Pozicování, tón komunikace, 5 obsahových pilířů s cíli (Reach/Community/Tickets/Recruitment/Brand). |
| **Inspirace** | Sekundární banka nápadů (NCAA inspirace, Reels, Stories, Carousel) — sbalená, ne hlavní část appky. |

## Jak je to postavené

Čisté HTML/CSS/JS, žádný framework, žádné externí JS knihovny. Appka je jeden `index.html` soubor v kořeni repozitáře — GitHub Pages ho servíruje přímo.

- **Fonty** — Oswald, Literata, IBM Plex Mono, načítané standardně z Google Fonts (`<link>` v hlavičce, ne base64).
- **Data o klubu/obsahu** (nápady na Reels/Stories/Carousel/NCAA inspirace) jsou vložená jako JS objekt přímo v `<script>` na konci souboru.
- **Uživatelská data** (zápasy, úkoly, poznámky v kalendáři, stav gameday checklistu) se ukládají do `localStorage` prohlížeče — nic se neposílá na server. To znamená, že data jsou vázaná na konkrétní prohlížeč/zařízení, ne sdílená mezi lidmi.

### Zdrojové soubory (pro úpravy)

Appka se generuje z těchto zdrojů skriptem `build.py` → `build2.py` → `build3.py` (Python), které skládají finální `index.html`:

- `sections.txt` — veškerý textový obsah stránky (HTML fragmenty pro jednotlivé sekce)
- `idea_data.json` / `ncaa_data.json` — banka nápadů (Reels/Stories/Carousel/NCAA)
- `app_core_js.txt` — navigace, banka nápadů (explorer)
- `task_manager_js.txt` — plánovač úkolů, kalendář zápasů, gameday checklist
- `build.py` — generuje CSS (`built_css.txt`)
- `build2.py` — generuje JS data blob (`data_js.txt`) z JSON souborů
- `build3.py` — poskládá finální `index.html`

Pokud upravuješ obsah, uprav zdrojový soubor a spusť `python3 build.py && python3 build2.py && python3 build3.py`, ne `index.html` přímo (přepíše se při dalším buildu).

## Nasazení přes GitHub Pages

1. Repozitář je public (GitHub Pages zdarma vyžaduje public repo, pokud nemáte placený plán).
2. V nastavení repa: **Settings → Pages → Source: Deploy from a branch → Branch: `main` / `(root)` → Save.**
3. Po uložení se appka objeví na `https://<uživatel>.github.io/<repo>/` (může trvat ~1 minutu).
4. Každý nový `git push` na `main` s upraveným `index.html` automaticky aktualizuje živou verzi.

## Poznámka k datům

Protože appka ukládá zápasy/úkoly do `localStorage` prohlížeče, **není to sdílený nástroj mezi víc lidmi** — každý, kdo appku otevře, má svoje vlastní data. Pokud bude potřeba sdílet plán mezi víc lidmi z týmu, appka by potřebovala jednoduchý backend (např. Firebase/Supabase) — momentálně to není implementované.
