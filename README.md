# KI-Agenten ohne Token-Kosten

> Bauen Sie 24/7 KI-Agenten mit **Hermes + OmniRoute** – ohne laufende API-Kosten.
> Praxis-Anleitung für KMU von Hermetikmarketing.

🔗 **Live-Seite:** [GitHub Pages Landingpage](https://hermetikmarketing.github.io/ki-agenten-leadmagnet/)

## Was ist das?

Eine komplette Anleitung, um KI-Agenten aufzubauen, die automatisch laufen – jeden Tag, ohne laufende Token-Kosten. Die Architektur nutzt:

- **[Hermes Agent](https://github.com/NousResearch/hermes-agent)** (Nous Research) – Open-Source KI-Agent-Framework
- **[OmniRoute](https://www.npmjs.com/package/omniroute)** – kostenloser LLM-Gateway (115+ Modelle, kein API-Key)
- **Manager/Worker-Pattern** – bezahlter Manager sanitisiert Daten, kostenlose Worker erledigen die Arbeit

## Architektur

```
[Manager — lokal, bezahlt]
   liest Kunden-Briefing → anonymisiert → startet Worker
[Worker — OmniRoute-Profil, kostenlos]
   Mitbewerber-Scout · Content-Creator · Reality-Checker · USP-Stratege
[Output]
   Markdown → Notion-Kanban → Telegram-Push-Benachrichtigung
```

## Quick Start

```bash
# 1. OmniRoute installieren
npm install -g omniroute
omniroute                 # Server auf http://localhost:20128

# 2. Hermes installieren
curl -fsSL https://hermes-agent.nousresearch.com/install.sh | bash
hermes setup

# 3. OmniRoute-Profil erstellen
hermes profile create omniroute-workers
hermes -p omniroute-workers config set model.provider custom
hermes -p omniroute-workers config set model.base_url http://localhost:20128/v1
hermes -p omniroute-workers config set model.default oc/deepseek-v4-flash-free
hermes -p omniroute-workers config set model.api_key dummy

# 4. Cron-Agent erstellen
hermes -p omniroute-workers cron create "0 7 * * 1-6" "Dein Prompt..." --name "Scout" --deliver local

# 5. Gateway aktivieren
hermes -p omniroute-workers gateway install
hermes -p omniroute-workers gateway start
```

## Kosten

| Komponente | Kosten |
|---|---|
| OmniRoute | 0 € / Monat |
| Hermes Agent | 0 € / Monat |
| Manager-Modell (minimal) | ~5-15 € / Monat |
| Infrastruktur | 0 € (lokal) oder ~5 € (Hetzner) |
| **Gesamt** | **ca. 5-20 € / Monat** |

## Use Cases

- 🔍 **Mitbewerber-Beobachtung** – Täglich automatisch
- ✍️ **Content-Ideen** – 2x pro Woche
- 🚦 **Reality-Checker** – Auf Anforderung
- 📈 **USP-Strategie** – Wöchentlich
- 🎯 **Lead-Recherche** – 3x pro Woche
- 📺 **YouTube-Monitoring** – Täglich

## Datenschutz

Der Manager entfernt vor der Weitergabe an Worker alle:
- Firmennamen
- Personennamen
- Konkrete Zahlen/KPIs
- Interne Systembezeichnungen

Worker erhalten nur ein **anonymisiertes Problem-Profil** (Branche, Größenklasse, Schmerzpunkt).

## Pitfalls

- ⚠️ Statt `model: "auto"` immer ein konkretes Modell setzen (z.B. `oc/deepseek-v4-flash-free`) – "auto" führt zu HTTP 503
- ⚠️ Cron-Testläufe können 5-20 Minuten dauern (Free-Gateways sind langsam) – im Hintergrund ausführen
- ⚠️ Job-IDs sind 12-Hex-Zeichen – nicht mit `{16,}` greppen
- ⚠️ Node.js ≥ 22 erforderlich

## Kontakt

**Hermetikmarketing** – KI-Agentur für Sondermaschinenbau & KMU

📧 timo@hermetikmarketing.de

---

MIT-lizenziert · 2026
