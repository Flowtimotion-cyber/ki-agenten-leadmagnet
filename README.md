# Hermetikmarketing · Dein KI-Betriebssystem

> 🔥 **Aus der Asche der alten Systeme erhebt sich dein Weg.**
>
> Hermes Agent + Obsidian + N8n auf deinem eigenen Server.
> Eine KI-Infrastruktur, die dir gehört – ohne SaaS-Abos, ohne Daten an fremde Clouds, ohne laufende Token-Kosten.

## Was ist das?

Ein komplettes KI-Betriebssystem für KMU – aufgebaut auf drei Komponenten:

| Komponente | Rolle | Kosten |
|---|---|---|
| **[Hermes Agent](https://github.com/NousResearch/hermes-agent)** | KI-Agent-Framework: Tools, Memory, Cron-Jobs, Messaging | 0 € |
| **[Obsidian](https://obsidian.md)** | Zweites Gehirn: Markdown-Vault, verlinkt, durchsuchbar | 0 € |
| **[N8n](https://n8n.io)** | Automatisierungs-Engine: verbindet Postfach, CRM, Kalender | 0 € |
| **[OmniRoute](https://www.npmjs.com/package/omniroute)** | Kostenloser KI-Gateway: 115+ Modelle, kein API-Key | 0 € |
| **Hetzner-Server** | CX22, 2 GB RAM, Docker – voll unter deiner Kontrolle | ~5 €/Monat |
| **Manager-Modell** | Optional: bezahltes Modell für Sanitization (minimal) | ~5-15 €/Monat |

**Gesamt: ca. 10-20 €/Monat** für eine 24/7 KI-Agenten-Pipeline.

## Architektur

```
[Dein Hetzner-Server]
  ├── Hermes Agent (Port 9119)   ← KI-Agent-Framework
  ├── N8n (Port 5678)             ← Automatisierung
  ├── Obsidian Vault (Git-Sync)   ← Wissensspeicher
  └── OmniRoute (:20128)         ← 115+ kostenlose KI-Modelle
        ↓
  [Manager sanitisiert Briefings]  ← Datenschutz: keine echten Namen/Zahlen
        ↓
  [Worker-Agenten]                 ← Mitbewerber · Content · Leads · USP
        ↓
  [Telegram-Push]                 ← Du bekommst Ergebnisse aufs Handy
```

## Setup (4 Schritte)

```bash
# 1. Server-Setup
ssh root@dein-server
apt update && apt install docker.io docker-compose
docker run -d --name n8n -p 5678:5678 n8nio/n8n

# 2. Hermes + OmniRoute
npm install -g omniroute
omniroute  # :20128
hermes -p workers config set model.base_url http://localhost:20128/v1
hermes -p workers config set model.default oc/deepseek-v4-flash-free

# 3. Obsidian Vault + N8n Workflows
git init ~/vault && git remote add origin ssh://...

# 4. Agenten aktivieren
hermes -p workers cron create "0 7 * * 1-6" "Mitbewerber-Scout..." --deliver telegram
hermes -p workers gateway install
hermes -p workers gateway start
```

## Use Cases

- 🔍 **Mitbewerber-Beobachtung** – Täglich automatisch
- ✍️ **Content-Ideen** – 2x pro Woche
- 🚦 **Reality-Checker** – Auf Anforderung
- 📈 **USP-Strategie** – Wöchentlich
- 🎯 **Lead-Recherche** – 3x pro Woche
- 📺 **YouTube-Monitoring** – Täglich

## Datenschutz

Der Manager entfernt vor der Weitergabe an Worker alle:
- Firmennamen, Personennamen, konkrete Zahlen/KPIs, interne Systembezeichnungen

Worker erhalten nur ein **anonymisiertes Problem-Profil** (Branche, Größenklasse, Schmerzpunkt).

## Kontakt

**Hermetikmarketing** – KI-Agentur für Sondermaschinenbau & KMU

📧 timo@hermetikmarketing.de

---

🔥 *Aus der Asche der alten Systeme erhebt sich dein Weg.*

MIT-lizenziert · 2026
