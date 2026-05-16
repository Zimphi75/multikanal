# Swiss Digital Banking Digest

Automatisch generierter Wochendigest zu Digitalisierung, Regulierung und Innovation im Schweizer Bankensektor.

**Live:** [banking.multikanal.ch](https://banking.multikanal.ch)

## Wie es funktioniert

1. **n8n Workflow** läuft wöchentlich auf einem NAS/Docker
2. RSS-Feeds werden aggregiert (FINMA, SNB, Fintechnews.ch, BankingHub, Netzwoche, HSLU IFZ)
3. Claude Sonnet (Anthropic) fasst und strukturiert die Inhalte
4. Das Ergebnis wird als `data/kw{KW}-{YEAR}.json` in dieses Repository gepusht
5. Die Website liest das JSON automatisch und rendert den Digest

## Struktur

```
/
├── index.html          # Komplette Website (HTML/CSS/JS, kein Build-Step)
├── CNAME               # Custom Domain: banking.multikanal.ch
└── data/
    └── kw20-2026.json  # Wöchentliche Digest-Dateien (automatisch generiert)
```

## Website-Features

- **Automatische KW-Erkennung** – lädt immer den neusten verfügbaren Digest
- **Automatische KW-Erkennung** – lädt immer den neusten verfügbaren Digest
- **Live-Marktdaten** – BTC/CHF (CoinGecko), SMI & SPI (Yahoo Finance), alle 5 Min. aktualisiert; BTC mit Zeitraum-Toggle (1T/1W/1M) und Sparkline-Chart, SMI/SPI fix auf 1T
- **Metrics Row** – 4 Kennzahlen aus verschiedenen Artikeln, verlinkt auf den jeweiligen Artikel
- **Newspaper-Layout** – Lead Story, Minor Stories, 2×2-Spalten-Layout (CSS Subgrid, pixelgenaue Zeilenausrichtung)
- **Leseempfehlungen** – nummeriert mit grossen goldenen Ziffern, verlinkt auf Originalquellen
- **Strategische Implikationen** – Zielgruppe, Fliesstext und priorisierte Massnahmen
- **Dark Mode** – Toggle + automatische System-Erkennung (`prefers-color-scheme`), gespeichert in localStorage
- **DE/EN** – alle Inhalte zweisprachig, automatische Browser-Spracherkennung beim ersten Besuch
- **Tag-Filter** – klickbare Tags filtern Artikel seitenübergreifend
- **Deeplinks** – alle Headlines verlinken auf die Originalquelle
- **Impressum & Datenschutz** – nDSG-konforme Seiten mit Dark Mode & DE/EN-Toggle unter `/impressum.html` und `/datenschutz.html`

## JSON-Format

```json
{
  "meta": { "kw", "year", "date_from", "date_to", "slug", "generator" },
  "top_stories": [{ "headline_de", "headline_en", "body_de", "body_en", "source_url", "tags", "key_figures" }],
  "sections": [{ "id", "title_de", "title_en", "items": [...] }],
  "reading_recommendations": [{ "title_de", "title_en", "url", "source" }],
  "strategic_implications": { "target_de", "body_de", "key_actions": [...] }
}
```

Section IDs: `regulatory`, `market`, `ai_tech`, `international`

## Deployment

GitHub Pages auf `main` Branch, Root-Verzeichnis. Jeder Push deployt automatisch.
