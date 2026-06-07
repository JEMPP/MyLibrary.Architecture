# Review Library Process

Version: 1.0

Dieses Dokument beschreibt den Standardprozess zur Bewertung bestehender Bibliotheken anhand der Standards aus MyLibrary.Architecture.

---

# Ziel

Ziel eines Reviews ist:

* die aktuelle Architektur zu verstehen
* Stärken und Schwächen zu identifizieren
* Abweichungen von Standards festzustellen
* Risiken sichtbar zu machen
* technische Schulden zu erkennen
* einen Maßnahmenkatalog für spätere Refactorings zu erstellen

Ein Review verändert keinen Code.

Ein Review bewertet.

---

# Referenzen

Primäre Referenz:

```text
Architecture-AI-Prompt.md
```

Weitere Referenzen:

```text
Standards/*
Templates/*
```

---

# Voraussetzungen

Vor dem Review:

```bash
git status
```

Erwartetes Ergebnis:

```text
nothing to commit, working tree clean
```

---

# Projekt exportieren

Projekt gemäß:

```text
Processes/Upload-To-ChatGPT-Process.md
```

exportieren.

Empfohlen:

```bash
git archive --format zip --output MyLibrary.<Name>.zip HEAD
```

---

# Review starten

Neuen Chat erstellen.

Empfohlener Titel:

```text
Review MyLibrary.<Name> according to MyLibrary.Architecture
```

Prompt verwenden:

```text
Prompts/Review-Library-Prompt.md
```

Projekt-ZIP hochladen.

---

# Analyse

Zunächst soll die Bibliothek beschrieben werden.

Zu erfassen sind:

* Solution-Struktur
* Projektstruktur
* Namespaces
* Services
* Models
* Interfaces
* Repositories
* Konfiguration
* Logging
* Datenbankzugriffe
* Testprojekte
* externe Abhängigkeiten

---

# Architekturprüfung

Prüfen:

* Ist die Struktur nachvollziehbar?
* Sind Verantwortlichkeiten sauber getrennt?
* Ist die Bibliothek wiederverwendbar?
* Ist die Bibliothek testbar?
* Ist die Bibliothek erweiterbar?

---

# Standards-Check

Prüfen gegen:

```text
Development Standards
Database Standards
Security Standards
Testing Standards
Naming Conventions
GitHub Standards
```

---

# Dependency Injection

Prüfen:

* Interfaces vorhanden?
* Services registrierbar?
* ServiceCollectionExtensions vorhanden?
* Abhängigkeiten sauber injizierbar?

---

# Logging

Prüfen:

* ILogger<T> verwendet?
* Console.WriteLine vorhanden?
* direkte Serilog-Aufrufe vorhanden?

---

# Konfiguration

Prüfen:

* Options-Klassen vorhanden?
* Konfiguration ausgelagert?
* Hardcodierte Werte vorhanden?
* Geheimnisse korrekt behandelt?

---

# Datenbankzugriffe

Prüfen:

* Dapper verwendet?
* Repository Pattern vorhanden?
* SQL parameterisiert?
* Connection Strings ausgelagert?

---

# Sicherheit

Prüfen:

* Secrets im Repository?
* Zugangsdaten hardcodiert?
* unsichere Konfigurationen?
* personenbezogene Daten ungeschützt?

---

# Blazor-Komponenten

Falls vorhanden prüfen:

* Wiederverwendbarkeit
* Komponentenstruktur
* Trennung von Logik und Darstellung
* generische Verwendbarkeit
* projektspezifische Abhängigkeiten

---

# Tests

Prüfen:

* Testprojekt vorhanden?
* xUnit verwendet?
* Testabdeckung ausreichend?
* wichtige Services getestet?

---

# Dokumentation

Prüfen:

* README vorhanden?
* Installation dokumentiert?
* Beispiele vorhanden?
* DI beschrieben?
* Konfiguration beschrieben?

---

# Bewertung

Die Ergebnisse werden eingeordnet.

---

## Stärken

Was ist bereits gut umgesetzt?

Beispiele:

* klare Struktur
* gute Testbarkeit
* sauberer DI-Einsatz
* gute Dokumentation

---

## Schwächen

Welche Probleme wurden identifiziert?

Beispiele:

* fehlende Interfaces
* fehlende Tests
* Hardcodierungen
* Logging-Probleme

---

## Risiken

Welche Risiken bestehen?

Beispiele:

* Sicherheitsrisiken
* Wartbarkeitsprobleme
* technische Schulden
* fehlende Erweiterbarkeit

---

# Priorisierung

Alle Maßnahmen werden priorisiert.

---

## Priorität 1

Kritische Probleme

Beispiele:

* Sicherheitsprobleme
* Secrets im Repository
* fehlerhafte Architekturentscheidungen

---

## Priorität 2

Wichtige Verbesserungen

Beispiele:

* fehlende Tests
* fehlende DI-Struktur
* fehlende Dokumentation

---

## Priorität 3

Optionale Verbesserungen

Beispiele:

* kosmetische Verbesserungen
* zusätzliche Tests
* Strukturvereinheitlichungen

---

# Ergebnis

Das Ergebnis eines Reviews besteht aus:

1. Kurzbewertung
2. Architekturübersicht
3. Stärken
4. Schwächen
5. Risiken
6. Abweichungen von Standards
7. Priorisierter Maßnahmenkatalog

---

# Wichtige Regel

Im Rahmen eines Reviews werden:

* keine Refactorings durchgeführt
* keine Klassen neu geschrieben
* keine umfangreichen Codeänderungen erzeugt

Kleine Codebeispiele zur Veranschaulichung sind zulässig.

---

# Übergang zum Refactoring

Nach Abschluss des Reviews wird entschieden:

```text
Keine Maßnahmen erforderlich
```

oder

```text
Refactoring durchführen
```

Falls ein Refactoring durchgeführt werden soll:

```text
Processes/Refactor-Library-Process.md
```

verwenden.

---

# Qualitätsziel

Das Review soll:

* objektiv
* nachvollziehbar
* reproduzierbar
* standardbasiert

sein.

Alle Bewertungen orientieren sich an den Standards aus MyLibrary.Architecture.
