# Claude Build Factory

Automatisierte Projekt-Build-Pipeline: GitHub Issue erstellen → Label setzen → Claude baut und deployed.

## Wie es funktioniert

1. Issue mit dem "Build Request"-Template erstellen
2. Spec ausfüllen (App-Name, Features, Tech-Stack)
3. Label **`claude-build`** hinzufügen
4. GitHub Actions startet automatisch
5. Claude baut das Projekt (~10–20 min)
6. Deploy-URL erscheint als Issue-Kommentar
7. Label wechselt zu **`deployed`** (oder `build-failed`)

## Setup

### 1. Repository forken oder klonen

### 2. GitHub Secrets konfigurieren

Unter **Settings → Secrets and variables → Actions → New repository secret**:

| Secret | Wert | Woher |
|--------|------|-------|
| `ANTHROPIC_API_KEY` | `sk-ant-...` | [console.anthropic.com](https://console.anthropic.com) |
| `NETLIFY_AUTH_TOKEN` | `nfp_...` | [app.netlify.com/user/applications](https://app.netlify.com/user/applications) |

### 3. GitHub Labels erstellen

Unter **Issues → Labels → New label**:

| Label | Farbe | Beschreibung |
|-------|-------|--------------|
| `claude-build` | `#0075ca` | Trigger: Claude baut dieses Projekt |
| `deployed` | `#0e8a16` | Build erfolgreich deployed |
| `build-failed` | `#e4e669` | Build fehlgeschlagen |

### 4. Workflow-Permissions prüfen

Unter **Settings → Actions → General → Workflow permissions**:
- "Read and write permissions" aktivieren

## Ersten Build testen

1. Issue erstellen mit dem "Build Request"-Template
2. Spec anpassen (z.B. `NAME: test-app`)
3. Issue speichern
4. Label `claude-build` hinzufügen
5. Unter **Actions** den laufenden Workflow beobachten

## Spec-Felder

```
APP_TYPE: Web-App | API | CLI
NAME: kebab-case-name (wird als Netlify-Subdomain verwendet)
DESCRIPTION: Was macht die App?

ZIELGRUPPE: Wer nutzt sie?

FEATURES:
- Feature 1
- Feature 2

TECH_STACK: next.js | react | express | ...
STYLING: tailwind+shadcn | tailwind | css
AUTH: keine | supabase | nextauth
DATABASE: localStorage | supabase | sqlite | postgres

DESIGN:
  STIL: minimal | modern | playful
  FARBEN: z.B. "warmes Off-White + Dunkelgrau"
  BESONDERHEITEN: mobile-first | dark-mode | ...

DEPLOY_TARGET: netlify
SPRACHE: de | en
```

## Kosten

- **Anthropic API**: ~$0.50–2.00 pro Build (je nach Komplexität, Sonnet 4.6)
- **Netlify**: Free tier reicht für viele Projekte

## Einschränkungen

- Kein Backend / kein Datenbankzugriff aus dem CI (nur localStorage / externe APIs)
- Build-Timeout: 45 Minuten
- Netlify Free: 300 Build-Minuten/Monat (nicht für den CI-Runner relevant, nur für Rebuilds)
