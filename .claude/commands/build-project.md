# /build-project

**AUTONOMOUS MODE — KEINE BESTÄTIGUNG NÖTIG.**

Starte sofort. Kein `/plan`-Skill, kein Warten auf "ja". Der Spec unten ist der einzige Input.

## WICHTIG: Niemals pausieren

- Niemals `/plan` aufrufen (der wartet auf Bestätigung)
- Niemals fragen "Soll ich weitermachen?"
- Niemals auf Bestätigung warten
- Bei Unklarheiten: Annahme in `ASSUMPTIONS.md` schreiben, weitermachen

---

## Workflow — sofort ausführen:

### Schritt 1: Verzeichnis + Metadaten

```bash
mkdir -p /tmp/[name_aus_spec]
```

Erstelle:
- `CLAUDE.md` mit Projekt-Info aus dem Spec
- `ASSUMPTIONS.md` leer mit Titel

Statusmeldung: `[1/8] Setup fertig`

### Schritt 2: Architektur (intern, kein Output nötig)

Leite aus dem Spec ab:
- Tech-Stack
- Dateistruktur
- Features und ihre Abhängigkeiten

Schreibe Ergebnis in `CLAUDE.md`. Kein Output an User, direkt weiter.

### Schritt 3: Scaffolding

Laut Spec:
- Next.js: `npx create-next-app@latest [name] --typescript --tailwind --app --no-src-dir --yes`
- Express: `npm init -y && npm install express typescript ts-node`
- Oder anderes Framework laut Spec

Dann Abhängigkeiten installieren. Bei Peer-Dependency-Fehlern: `--legacy-peer-deps`.

`.env.local` mit Platzhaltern anlegen.

Statusmeldung: `[3/8] Scaffolding fertig`

### Schritt 4: TDD-Implementierung

Für jedes Feature aus dem Spec **sequenziell**:
1. Datei anlegen mit Tests (expect → RED)
2. Implementierung schreiben (GREEN)
3. Tests laufen lassen

Statusmeldung nach jedem Feature: `Feature X/Y: [Name] implementiert`

### Schritt 5: Build-Gate

```bash
npm run build && npm test
```

Wenn Fehler: analysieren, beheben, max. 3 Versuche. Dann weiter.

Statusmeldung: `[5/8] Build + Tests grün`

### Schritt 6: Deploy

Via Netlify MCP oder `netlify deploy --prod` je nach Verfügbarkeit.

Statusmeldung: `[6/8] Deployed`

### Schritt 7: Fertig

```
FERTIG!
URL: https://[name].netlify.app
Features implementiert: [Liste]
Annahmen: [Wichtigstes aus ASSUMPTIONS.md]
```

---

## Spec:

$ARGUMENTS
