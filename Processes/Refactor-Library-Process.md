# Refactor Library Process

Version: 1.0

Dieses Dokument beschreibt den Standardprozess zur Modernisierung und Anpassung bestehender Bibliotheken an die Standards aus MyLibrary.Architecture.

---

# Ziel

Ziel eines Refactorings ist:

* bestehende Funktionalität beizubehalten
* technische Schulden zu reduzieren
* Standards umzusetzen
* Testbarkeit zu verbessern
* Wartbarkeit zu erhöhen
* Dokumentation zu verbessern

Ein Refactoring ist keine vollständige Neuentwicklung.

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

Vor dem Refactoring:

```bash
git status
```

Erwartetes Ergebnis:

```text
nothing to commit, working tree clean
```

---

# Branch erstellen

Refactorings erfolgen niemals direkt auf:

```text
main
```

Neuen Branch anlegen:

```bash
git checkout -b feature/refactor-architecture-standard
```

Alternativ:

```bash
git checkout -b feature/refactor-<bibliotheksname>
```

Beispiel:

```bash
git checkout -b feature/refactor-linkliste
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

# Refactoring-Analyse

Neuen Chat erstellen.

Prompt verwenden:

```text
Prompts/Refactor-Library-Prompt.md
```

Projekt-ZIP hochladen.

---

# Analyse prüfen

Folgende Punkte überprüfen:

* aktuelle Struktur korrekt erkannt?
* Bibliothek vollständig erkannt?
* Testprojekt erkannt?
* Hauptservices erkannt?
* Datenbankzugriffe erkannt?
* Logging erkannt?

Falls erforderlich:

* Kontext ergänzen
* Fachlichkeit erläutern
* Sonderfälle beschreiben

---

# Refactoring-Plan erstellen

Vor der Umsetzung prüfen:

* Welche Änderungen sind notwendig?
* Welche Änderungen sind optional?
* Welche Änderungen bringen den größten Nutzen?

Priorisierung:

```text
Priorität 1
kritische Abweichungen

Priorität 2
wichtige Verbesserungen

Priorität 3
optionale Optimierungen
```

---

# Umsetzung

Refactoring erfolgt schrittweise.

Empfohlene Reihenfolge:

1. Projektstruktur
2. Ordnerstruktur
3. Namespaces
4. Interfaces
5. Services
6. Dependency Injection
7. Logging
8. Konfiguration
9. Datenbankzugriffe
10. Tests
11. Dokumentation

---

# Kleine Commits bevorzugen

Nicht:

```text
Refactor everything
```

Bevorzugt:

```text
Refactor project structure
Add service interfaces
Add dependency injection
Replace direct logging with ILogger
Add unit tests
Update README
```

---

# Dependency Injection

Prüfen:

* Services registriert?
* Interfaces vorhanden?
* ServiceCollectionExtensions vorhanden?

Beispiel:

```csharp
builder.Services.AddMyLibrary<Name>();
```

---

# Logging

Prüfen:

* ILogger<T> vorhanden?
* Console.WriteLine entfernen
* direkte Serilog-Aufrufe vermeiden

Serilog wird ausschließlich im Host konfiguriert.

---

# Konfiguration

Prüfen:

* Options-Klassen vorhanden?
* Secrets ausgelagert?
* Hardcodierte Werte vermeiden

Verwenden:

```text
appsettings.json
appsettings.Secrets.json
```

---

# Datenbankzugriffe

Prüfen:

* Dapper verwendet?
* Repository Pattern vorhanden?
* SQL parameterisiert?
* Connection Strings ausgelagert?

Die Regeln aus:

```text
Standards/Database-Standards.md
```

gelten vollständig.

---

# Blazor-Komponenten

Prüfen:

* Komponenten generisch?
* keine projektspezifischen URLs?
* keine Kundennamen?
* Logik in Services?

---

# Tests

Prüfen:

* Testprojekt vorhanden?
* xUnit verwendet?
* Services getestet?
* Validatoren getestet?

Fehlende Tests ergänzen.

---

# README

Prüfen:

* Beschreibung vorhanden?
* Installation beschrieben?
* DI dokumentiert?
* Beispielcode vorhanden?

README bei Bedarf aktualisieren.

---

# Build-Prüfung

Nach jeder größeren Änderung:

```bash
dotnet build
```

---

# Test-Prüfung

Nach jeder größeren Änderung:

```bash
dotnet test
```

Alle bestehenden Tests müssen weiterhin erfolgreich sein.

---

# Review des Ergebnisses

Prüfen:

* Funktionalität unverändert?
* Standards erfüllt?
* Architektur verbessert?
* Dokumentation aktuell?

---

# Merge

Nach erfolgreichem Refactoring:

```bash
git checkout main
git merge feature/refactor-<name>
```

---

# Versionierung

Nach erfolgreichem Refactoring:

Patch:

```text
v1.0.1
```

Kleinere Verbesserungen.

Minor:

```text
v1.1.0
```

Neue Funktionen oder größere Architekturverbesserungen.

Major:

```text
v2.0.0
```

Inkompatible Änderungen.

---

# Qualitätsziel

Nach Abschluss soll die Bibliothek:

* den Standards aus MyLibrary.Architecture entsprechen
* testbar sein
* dokumentiert sein
* GitHub-ready sein
* NuGet-ready sein
* wartbar sein

ohne bestehende Funktionalität zu verlieren.
