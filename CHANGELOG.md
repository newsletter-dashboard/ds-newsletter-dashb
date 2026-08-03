# Changelog

## Refactor — zjednodušení a přepracování na pracovní nástroj

Kompletní přestavba dashboardu z rozsáhlé banky nápadů na praktický pracovní nástroj pro social media UK Kings Prague.

### Přidáno

- **Sekce „Tento týden“** jako výchozí landing view — počet naplánovaných výstupů, nejbližší zápas/nábor, hlavní úkol týdne, seznam obsahu.
- **Task manager** — každý content úkol má název, formát, platformu, datum, deadline, odpovědnou osobu, cíl (Reach/Community/Tickets/Recruitment/Brand), stav (Nápad → Připraveno → Natočeno → Ve střihu → Schváleno → Publikováno), poznámku/shotlist. Jde editovat, mazat, filtrovat podle stavu/platformy/cíle.
- **Obsahový plán** s realistickým minimem (týden se zápasem / bez zápasu / „když není čas“).
- **Inside the Kings** — definice jedné hlavní obsahové série s pravidly konzistence (intro, titulky, číslování dílů) místo několika stejně důležitých sérií.
- **Tryout kampaň** rozdělená do 6 fází (Teaser → Přihlášky → Připomenutí → Den tryoutu → Aftermovie → Výběr týmu), se storyboardem po sekundách a praktickým shotlistem.
- **Gameday checklist** — mobilní seznam úkolů před/během/po zápase, ukládá se do localStorage.
- Cílové štítky (Reach/Community/Tickets/Recruitment/Brand) u obsahových pilířů a úkolů.

### Odstraněno / sloučeno

- Samostatná kapitola „Kolik na to máme lidí“ (produkční kapacita) — smazána, klíčová myšlenka (natáčení dělá tým, ne jeden člověk) přenesena jinam.
- Samostatná kapitola „Proč lidi sdílí“ (psychologie) — zkrácena na jeden odstavec uvnitř Strategie.
- Velká KPI tabulka s konkrétními predikcemi čísel (sledující, zhlédnutí po měsících) — nahrazena rámcem baseline → cílová změna → období testu, bez nepodložených konkrétních čísel.
- Banky nápadů (150+ Reels, 100 Stories, 50 Carousel, 32 NCAA nápadů) přesunuty ze střední pozice dashboardu do sbalené sekundární sekce „Inspirace“.
- Zredukován rozsah popisných textů napříč celým dashboardem (odhadem o 40–50 %).

### Zachováno

- Veškerá uživatelská data v `localStorage` (klíče `ukkings_planner_matches`, `ukkings_planner_notes`) — logika pro čtení starých záznamů zůstala zpětně kompatibilní.
- Banka nápadů (obsahově beze změny, jen přesunutá a sbalená).
- Klubové barvy (navy + červená) a typografie (Oswald / Literata / IBM Plex Mono).

### Technické změny

- Fonty přesunuty z vloženého base64 (~330 KB) na standardní `<link>` na Google Fonts — velikost `index.html` klesla z ~420 KB na ~106 KB.
- Odstraněn nepoužívaný CSS (`.hero` blok po zjednodušení navigace).
- Opravena chyba synchronizace — úkol přidaný v jedné části appky (Tento týden) se neobjevoval v druhé (Obsahový plán), protože obě části měly nezávislou kopii dat v paměti. Přidán jednoduchý registr, co po každé změně obnoví všechny zobrazené seznamy úkolů.
- Ověřeno: žádné duplicitní ID, žádné rozbité odkazy v menu, žádné chyby v konzoli, žádný horizontální scroll na 390px/768px/1440px.
