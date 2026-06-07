# Create New Library Process

Version: 1.0

Dieses Dokument beschreibt den Standardprozess zur Erstellung neuer Bibliotheken gemäß den Standards aus MyLibrary.Architecture.

---

# Ziel

Ziel dieses Prozesses ist die Erstellung einer neuen Bibliothek, die von Anfang an:

* den Architekturstandards entspricht
* testbar ist
* dokumentiert ist
* GitHub-ready ist
* NuGet-ready ist
* langfristig wartbar ist

Die Bibliothek soll nicht nachträglich standardisiert werden müssen.

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
Prompts/*
```

---

# Bibliothekstyp bestimmen

Vor der Erstellung muss der Typ der Bibliothek festgelegt werden.

Verfügbare Typen:

```text
Class Library
Blazor Library
Console App
Worker Service
Web API
```

Passendes Template auswählen:

```text
Templates/ClassLibraryTemplate.md
Templates/BlazorLibraryTemplate.md
Templates/ConsoleAppTemplate.md
Templates/WorkerServiceTemplate.md
Templates/WebApiTemplate.md
```

---

# Namensgebung festlegen

Namensschema:

```text
MyLibrary.<Name>
```

Beispiele:

```text
MyLibrary.Email
MyLibrary.LinkListe
MyLibrary.Workflow
MyLibrary.Reporting
```

---

# GitHub Repository anlegen

Neues Repository anlegen:

```text
MyLibrary.<Name>
```

Einstellungen:

```text
Visibility: Private
Default Branch: main
```

Optional:

```text
Visibility: Public
```

wenn die Bibliothek öffentlich bereitgestellt werden soll.

---

# Lokale Struktur erstellen

Standardstruktur:

```text
MyLibrary.<Name>.sln

├─ MyLibrary.<Name>
└─ MyLibrary.<Name>.Test
```

---

# Visual Studio Projekt erstellen

Empfohlene Reihenfolge:

1. Solution erstellen
2. Hauptprojekt erstellen
3. xUnit Testprojekt erstellen
4. Projektverweis setzen

---

# Standarddateien anlegen

Im Repository Root:

```text
README.md
.gitignore
LICENSE
```

Optional:

```text
CHANGELOG.md
```

---

# .gitignore übernehmen

Verwenden:

```text
Templates/GitIgnoreTemplate.md
```

Insbesondere:

```text
bin/
obj/
.vs/
appsettings.Secrets.json
```

müssen ausgeschlossen werden.

---

# Dependency Injection vorbereiten

Ordner:

```text
Extensions
```

Datei:

```text
ServiceCollectionExtensions.cs
```

Beispiel:

```csharp
builder.Services.AddMyLibraryEmail();
```

---

# Projektstruktur erstellen

Mindestens:

```text
Models
Interfaces
Services
Extensions
Configuration
Exceptions
```

Optional:

```text
Repositories
Validators
Infrastructure
Components
```

abhängig vom Projekttyp.

---

# Logging vorbereiten

Standard:

```text
Serilog
```

Bibliotheken verwenden:

```csharp
ILogger<T>
```

Die Bibliothek konfiguriert Serilog nicht selbst.

---

# Konfiguration vorbereiten

Konfigurationsklassen:

```text
<Name>Options
```

Beispiele:

```text
EmailOptions
DatabaseOptions
WorkflowOptions
```

---

# Datenbankzugriffe

Falls Datenbankzugriffe benötigt werden:

Standard:

```text
Dapper
```

Zusätzlich:

```text
Repository Pattern
IDbConnectionFactory
```

Verwenden.

Die Regeln aus:

```text
Standards/Database-Standards.md
```

gelten vollständig.

---

# Authentifizierung

Falls erforderlich:

Standard:

```text
Windows Authentication
```

Zusätzlich:

```text
ICurrentUserService
```

vorsehen.

Die Architektur muss auf:

```text
Microsoft Entra ID
```

vorbereitbar sein.

---

# Tests vorbereiten

Standard:

```text
xUnit
```

Projekt:

```text
MyLibrary.<Name>.Test
```

Mindestens vorbereiten:

```text
Services
Validators
Repositories
```

---

# README erstellen

README muss enthalten:

* Beschreibung
* Ziel
* Installation
* Dependency Injection
* Konfiguration
* Beispiele
* Tests

---

# Architekturprüfung

Vor dem ersten Commit prüfen:

* Projektstruktur korrekt?
* Naming Conventions eingehalten?
* Interfaces vorhanden?
* DI vorbereitet?
* Logging vorbereitet?
* Tests vorhanden?
* README vorhanden?

---

# Erster Commit

Empfohlen:

```bash
git add .
git commit -m "Initial project structure"
```

---

# Erster Push

```bash
git push -u origin main
```

---

# Architektur-Review

Vor der eigentlichen Implementierung prüfen:

* Entspricht die Struktur den Standards?
* Passt das gewählte Template?
* Sind alle benötigten Komponenten vorhanden?

Optional:

Review gegen:

```text
Prompts/Review-Library-Prompt.md
```

durchführen.

---

# Erste Version

Empfohlener Tag:

```text
v0.1.0
```

Begründung:

Die Bibliothek ist angelegt, aber funktional noch nicht vollständig.

---

# Release-Kandidaten

Typische Entwicklung:

```text
v0.1.0
Projektstruktur

v0.2.0
Erste Funktionalität

v0.5.0
Feature vollständig

v1.0.0
Produktiv nutzbar
```

---

# Qualitätsziel

Die neue Bibliothek soll:

* den Standards aus MyLibrary.Architecture entsprechen
* von Anfang an testbar sein
* dokumentiert sein
* wiederverwendbar sein
* GitHub-ready sein
* NuGet-ready sein

ohne später ein größeres Architektur-Refactoring zu benötigen.

---

# Ergebnis

Nach Abschluss dieses Prozesses existieren:

```text
Repository
Solution
Projektstruktur
Testprojekt
README
.gitignore
DI-Struktur
Logging-Struktur
Konfigurationsstruktur
```

als vollständige Grundlage für die weitere Entwicklung.
