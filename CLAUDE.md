# Claude Build Factory — CI Runner Config

Dieses Repo wird von einem GitHub Actions Workflow betrieben.
Claude läuft headless im CI-Modus und baut Projekte vollständig autonom.

## Sprache

- Antworte immer auf **Deutsch**
- Commit-Messages und Code-Kommentare auf **Englisch**
- Variablen- und Funktionsnamen auf **Englisch**

## Autonomer Modus (PFLICHT in diesem Kontext)

Du läufst in einem GitHub Actions CI-Runner ohne menschliche Aufsicht.

- **Keine Rückfragen** — arbeite vollständig selbstständig
- **Keine Bestätigungen** — niemals auf Zustimmung warten
- **Keine /plan-Aufrufe** — /plan wartet auf Bestätigung, das ist verboten
- **Bei Unklarheiten**: beste Annahme treffen, in `ASSUMPTIONS.md` dokumentieren, weitermachen
- **Workflow**: Scaffolding → TDD → Build-Gate → Deploy → URL ausgeben
- **Test-Gate**: Deploye nur wenn `npm run build` + `npm test` erfolgreich
- **Deploy**: via Netlify CLI (`netlify deploy --dir=out --no-build --prod`)
- **Ergebnis**: URL im Format `https://[name].netlify.app` ausgeben — MUSS im Output erscheinen

## Coding-Stil

- Kleine, fokussierte Dateien (200-400 Zeilen, max 800)
- Immutability bevorzugen
- Kein `console.log` in Produktionscode
- Fehlerbehandlung mit try/catch

## Wichtig

Das Ergebnis wird aus dem CI-Output extrahiert. Die Deploy-URL MUSS ausgegeben werden.
Format: `https://[a-z0-9-]+\.netlify\.app`
