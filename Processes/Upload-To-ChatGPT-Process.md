# Upload To ChatGPT Process

Version: 1.0

Dieses Dokument beschreibt den Standardprozess, um bestehende MyLibrary-Projekte sicher und effizient für Analysen, Reviews und Refactorings in ChatGPT bereitzustellen.

---

# Ziel

Der Upload-Prozess soll sicherstellen, dass:

* keine Geheimnisse übertragen werden
* keine Build-Artefakte übertragen werden
* keine unnötigen Dateien übertragen werden
* der aktuelle Repository-Stand analysiert wird
* die Analyse reproduzierbar bleibt

---

# Voraussetzungen

Vor dem Export muss das Projekt in Git versioniert sein.

Das Repository sollte einen sauberen Zustand haben.

Prüfen:

```bash
git status
```

Erwartetes Ergebnis:

```text
nothing to commit, working tree clean
```

---

# Geheimnisse

Folgende Dateien dürfen nicht hochgeladen werden:

```text
appsettings.Secrets.json
```

sowie:

```text
*.pfx
*.snk
```

und alle Dateien mit:

* Passwörtern
* API Keys
* Zertifikaten
* produktiven Connection Strings

Die Regeln aus:

```text
Standards/Security-Standards.md
```

gelten vollständig.

---

# Bevorzugter Export

Verwende Git Archive.

Dadurch werden ausschließlich versionierte Dateien exportiert.

Nicht enthalten sind:

* bin
* obj
* .vs
* TestResults
* Dateien aus .gitignore

---

# ZIP erzeugen

Im Root des Repositories:

```bash
git archive --format zip --output MyLibrary.<Name>.zip HEAD
```

Beispiel:

```bash
git archive --format zip --output MyLibrary.LinkListe.zip HEAD
```

---

# Kontrolle des Exports

Optional kann geprüft werden, welche Dateien exportiert werden.

```bash
git ls-files
```

Die Ausgabe entspricht im Wesentlichen dem Inhalt des ZIP-Archivs.

---

# Alternative

Falls das Projekt bereits auf GitHub liegt:

```text
Code
→ Download ZIP
```

Dies ist ebenfalls zulässig.

---

# Nicht empfohlene Vorgehensweise

Nicht den kompletten Projektordner zippen.

Beispiel:

```text
Rechtsklick
→ Senden an ZIP
```

Dadurch können unbeabsichtigt enthalten sein:

```text
bin
obj
.vs
TestResults
temporäre Dateien
```

---

# Auswahl des passenden Prompts

Vor dem Upload festlegen, welches Ziel verfolgt wird.

---

## Architektur-Review

Verwenden:

```text
Prompts/Review-Library-Prompt.md
```

Ziel:

* Architektur bewerten
* Schwachstellen identifizieren
* Maßnahmen priorisieren

Keine Refactorings.

---

## Refactoring

Verwenden:

```text
Prompts/Refactor-Library-Prompt.md
```

Ziel:

* bestehende Bibliothek verbessern
* Standards umsetzen
* Codevorschläge erzeugen

---

## Neue Bibliothek

Verwenden:

```text
Prompts/Create-New-Library-Prompt.md
```

Ziel:

* neue Bibliothek erzeugen
* Standardstruktur erstellen
* Beispielcode erzeugen

---

# Empfohlener Ablauf

Für bestehende Bibliotheken:

```text
Review
↓
Entscheidung
↓
Refactor
↓
Commit
↓
Test
↓
Release
```

---

# Start eines neuen Chats

Für jede Bibliothek wird ein eigener Chat empfohlen.

Beispiel:

```text
Refactor MyLibrary.LinkListe according to MyLibrary.Architecture
```

oder

```text
Review MyLibrary.Email according to MyLibrary.Architecture
```

---

# Hochzuladende Dateien

Bevorzugt:

```text
MyLibrary.<Name>.zip
```

Beispiel:

```text
MyLibrary.LinkListe.zip
```

Inhalt:

```text
MyLibrary.<Name>.sln
MyLibrary.<Name>
MyLibrary.<Name>.Test
```

falls vorhanden.

---

# Referenz auf die Architektur

Bei jeder Analyse soll auf die Architekturstandards verwiesen werden.

Primäre Referenz:

```text
Architecture-AI-Prompt.md
```

Weitere Referenzen:

```text
Standards/*
Templates/*
Prompts/*
```

---

# Erwartetes Ergebnis

Nach dem Upload soll ChatGPT:

1. die Bibliothek analysieren
2. die aktuelle Struktur beschreiben
3. Abweichungen vom Standard identifizieren
4. Verbesserungen vorschlagen
5. bei Bedarf Refactoring-Code erzeugen
6. Tests und Dokumentation berücksichtigen

---

# Qualitätsziel

Die Analyse soll:

* reproduzierbar
* nachvollziehbar
* sicher
* standardkonform

sein.

Alle Vorschläge sollen sich an den Standards aus MyLibrary.Architecture orientieren.
