# Release Checklist

Diese Checkliste definiert den Standard für Releases aller MyLibrary-Anwendungen und -Bibliotheken.

---

# Versionierung

Es wird Semantic Versioning verwendet.

Beispiele:

- v0.6.1
- v1.2.0
- v2.0.0

---

# Release Notes

## Speicherort

Anwendungen:

```text
wwwroot/release-notes/vX.Y.Z.md
```

Bibliotheken:

```text
docs/releases/vX.Y.Z.md
```

---

## Dateiname

Immer:

```text
vX.Y.Z.md
```

Beispiel:

```text
v0.6.1.md
```

---

## Überschrift

Format:

```markdown
# v<Version> - <Kurzer Titel> (<YYYY-MM-DD>)
```

Beispiele:

```markdown
# v0.5.4 - Dokumentverwaltung und UI-Vereinheitlichung (2026-07-08)

# v0.6.1 - Tagebuch-Auswertungen und Mitarbeiter-Adressen (2026-08-02)

# v2.0.0 - E-Mail-Infrastruktur und Batchversand (2026-08-03)
```

---

## Titel

Der Titel beschreibt die zwei wichtigsten Themen des Releases.

Empfehlungen:

- kurz
- prägnant
- maximal zwei Hauptthemen

Gut:

- Dokumentverwaltung und UI-Vereinheitlichung
- Tagebuch-Auswertungen und Mitarbeiter-Adressen
- E-Mail-Infrastruktur und Batchversand

Nicht empfohlen:

- Dokumentverwaltung, Bugfixes, Refactoring, Performance, UI, Sicherheit und viele weitere Änderungen

---

## Struktur

Jede Release-Note verwendet dieselbe Struktur.

```markdown
# vX.Y.Z - Titel (YYYY-MM-DD)

## Highlights

Kurze Zusammenfassung der wichtigsten Änderungen.

## Neue Funktionen

- ...
- ...

## Verbesserungen

- ...
- ...

## Architektur

- ...
- ...

## Fehlerbehebungen

- ...
- ...

## Wartung

- Paketupdates
- Refactorings
- Performance
```

Nicht benötigte Kapitel können entfallen.

---

# appsettings.json

Vor jedem Release aktualisieren:

```json
{
  "Version": "0.6.1",
  "ReleaseDate": "2026-08-02"
}
```

## Datumsformat

Immer:

```text
YYYY-MM-DD
```

---

# Build

Vor jedem Release:

```text
dotnet build
```

muss erfolgreich sein.

---

# Tests

Falls vorhanden:

```text
dotnet test
```

muss erfolgreich sein.

---

# Qualitätsprüfung

Vor dem Release prüfen:

- keine Compilerfehler
- möglichst keine Compilerwarnungen
- git status sauber
- git diff --check sauber

---

# Git

## Commit

Release-relevante Änderungen (z. B. Release Notes, Version, ReleaseDate) sollen in einem eigenen Commit zusammengefasst werden.

Empfohlenes Format:

```text
Release vX.Y.Z - <Kurzer Titel>
```

Beispiel:

```text
Release v0.6.1 - Tagebuch-Auswertungen und Mitarbeiter-Adressen
```

---

## Tag

Format:

```text
vX.Y.Z
```

Beispiel:

```text
v0.6.1
```

---

## Tag-Beschreibung

Format:

```text
<Projektname> vX.Y.Z - <Kurzer Titel>
```

Beispiel:

```text
iOrga v0.6.1 - Tagebuch-Auswertungen und Mitarbeiter-Adressen
```

---

# GitHub Release

## Titel

Format:

```text
vX.Y.Z - <Kurzer Titel>
```

Beispiel:

```text
v0.6.1 - Tagebuch-Auswertungen und Mitarbeiter-Adressen
```

## Beschreibung

Die Beschreibung des GitHub-Releases wird direkt aus der Markdown-Datei übernommen.

---

# Release-Ablauf

Die folgenden Schritte sind in dieser Reihenfolge durchzuführen:

1. Implementierung abschließen
2. Build erfolgreich
3. Tests erfolgreich
4. Release Notes aktualisieren
5. Version aktualisieren
6. ReleaseDate aktualisieren
7. Release-Änderungen committen
8. Release-Tag erstellen
9. Änderungen und Tag pushen
10. GitHub-Release erstellen

---

# Abschlussprüfung

Vor Veröffentlichung muss geprüft werden:

- Version aktualisiert
- ReleaseDate aktualisiert
- Release Notes erstellt
- Build erfolgreich
- Tests erfolgreich
- Git-Status sauber
- Tag erstellt
- Tag gepusht
- GitHub Release erstellt