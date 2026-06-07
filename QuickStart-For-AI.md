# Quick Start For AI

Version: 1.0

Dieses Dokument enthält bewährte Startprompts für die Zusammenarbeit mit ChatGPT bei der Entwicklung von MyLibrary-Projekten.

Alle Prompts beziehen sich auf die Standards aus diesem Repository.

---

# Architekturreferenz

Verwende immer dieses Repository als Referenz:

```text
https://github.com/JEMPP/MyLibrary.Architecture
```

Primäre Referenz:

```text
Architecture-AI-Prompt.md
```

Weitere Referenzen:

```text
Standards/*
Templates/*
Prompts/*
Processes/*
```

---

# Review einer bestehenden Bibliothek

Verwenden wenn:

* eine bestehende Bibliothek bewertet werden soll
* Architekturprobleme identifiziert werden sollen
* Maßnahmen priorisiert werden sollen

Zusätzlich hochladen:

```text
MyLibrary.<Name>.zip
```

Prompt:

```text
Bitte führe ein Architektur-Review der hochgeladenen Bibliothek durch.

Verwende als Referenz:

https://github.com/JEMPP/MyLibrary.Architecture

Lies insbesondere:

- Architecture-AI-Prompt.md
- Prompts/Review-Library-Prompt.md

und führe das Review gemäß den dort definierten Standards und Prozessen durch.

Die hochgeladene ZIP-Datei enthält die aktuelle Version von:

MyLibrary.<Name>

Erstelle:

1. Architekturübersicht
2. Stärken
3. Schwächen
4. Abweichungen von den Standards
5. Risiken
6. Priorisierten Maßnahmenkatalog

Noch kein Refactoring durchführen.

Keine Codeänderungen erzeugen.

Ziel ist zunächst eine objektive Bewertung der Bibliothek.
```

---

# Refactoring einer bestehenden Bibliothek

Verwenden wenn:

* die Bibliothek verbessert werden soll
* Architekturstandards umgesetzt werden sollen
* konkrete Codeänderungen gewünscht sind

Zusätzlich hochladen:

```text
MyLibrary.<Name>.zip
```

Prompt:

```text
Bitte refaktoriere die hochgeladene Bibliothek gemäß den Standards aus:

https://github.com/JEMPP/MyLibrary.Architecture

Lies insbesondere:

- Architecture-AI-Prompt.md
- Prompts/Refactor-Library-Prompt.md

Analysiere zunächst die Bibliothek.

Erstelle:

1. Architekturübersicht
2. Abweichungen vom Standard
3. Refactoring-Plan

Erzeuge anschließend konkrete Codeänderungen Schritt für Schritt.

Bestehende Funktionalität muss erhalten bleiben.

Bevorzuge minimale Änderungen mit maximalem Nutzen.
```

---

# Neue Bibliothek erstellen

Verwenden wenn:

* eine neue Bibliothek entwickelt werden soll
* bereits Anforderungen vorliegen

Zusätzlich bereitstellen:

```text
Requirements/MyLibrary.<Name>.Requirements.md
```

Prompt:

```text
Bitte erstelle eine neue Bibliothek gemäß:

https://github.com/JEMPP/MyLibrary.Architecture

Lies insbesondere:

- Architecture-AI-Prompt.md
- Prompts/Create-New-Library-Prompt.md

Verwende zusätzlich folgende Anforderungen:

MyLibrary.<Name>.Requirements.md

Erzeuge:

- Zielarchitektur
- Projektstruktur
- Ordnerstruktur
- Klassen
- Interfaces
- Dependency Injection
- Tests
- README

Die Bibliothek soll den Standards aus MyLibrary.Architecture entsprechen.
```

---

# Anforderungen ermitteln

Verwenden wenn:

* eine neue Idee vorliegt
* Anforderungen noch nicht dokumentiert sind

Prompt:

```text
Bitte führe ein Requirements-Interview für eine neue Bibliothek durch.

Verwende als Referenz:

https://github.com/JEMPP/MyLibrary.Architecture

Lies insbesondere:

- Architecture-AI-Prompt.md
- Prompts/Gather-Requirements-Prompt.md

Ziel ist die Erstellung eines vollständigen Requirements-Dokuments gemäß:

Templates/RequirementsTemplate.md

Stelle die Fragen schrittweise.

Nicht direkt mit Architektur oder Code beginnen.
```

---

# Typischer Workflow

Für neue Projekte:

```text
Idee
↓
Requirements Interview
↓
Requirements.md
↓
Create
↓
Implementierung
↓
Review
↓
Refactor
↓
Release
```

---

# Typischer Workflow für bestehende Projekte

```text
Bestehende Bibliothek
↓
Review
↓
Maßnahmenkatalog
↓
Refactor
↓
Tests
↓
Release
```

---

# Empfehlungen

* Für jede Bibliothek einen eigenen Chat verwenden.
* ZIP-Dateien ausschließlich mit `git archive` erzeugen.
* Keine Secrets hochladen.
* Immer auf die Architekturstandards verweisen.
* Architekturänderungen zuerst im Repository dokumentieren.

---

# Ziel

Dieses Repository dient als Single Source of Truth für:

* Architektur
* Standards
* Templates
* Prozesse
* Prompts

aller Projekte der MyLibrary-Familie.
