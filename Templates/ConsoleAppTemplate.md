# Console Application Template

Version: 1.0

Dieses Dokument beschreibt die Standardvorlage für Konsolenanwendungen der MyLibrary-Familie.

---

# Ziel

Konsolenanwendungen werden verwendet für:

* Datenmigrationen
* Import-/Export-Prozesse
* Batch-Verarbeitung
* Administrationswerkzeuge
* Wartungsskripte
* Datenkonvertierungen
* Analysewerkzeuge

---

# Projekttyp

Visual Studio:

```text
Console App
```

Projektname:

```text
MyLibrary.<Name>.Console
```

Beispiele:

```text
MyLibrary.DataMigration.Console
MyLibrary.Email.Console
MyLibrary.Reporting.Console
MyLibrary.Workflow.Console
```

---

# Solution Struktur

```text
MyLibrary.<Name>.Console.sln

├─ MyLibrary.<Name>.Console
└─ MyLibrary.<Name>.Console.Test
```

---

# Projektstruktur

```text
MyLibrary.<Name>.Console

├─ Commands
├─ Configuration
├─ Services
├─ Models
├─ Extensions
├─ Exceptions
└─ Program.cs
```

Optional:

```text
Repositories
Validators
Infrastructure
```

---

# Program.cs

Program.cs enthält ausschließlich:

* Host-Aufbau
* Dependency Injection
* Logging-Konfiguration
* Start des Hauptprozesses

Keine Businesslogik.

Nicht erlaubt:

```csharp
Program.cs
↓
SQL
```

Nicht erlaubt:

```csharp
Program.cs
↓
Geschäftslogik
```

---

# Generic Host

Es wird bevorzugt:

```csharp
Host.CreateDefaultBuilder()
```

verwendet.

Beispiel:

```csharp
var host = Host
    .CreateDefaultBuilder(args)
    .ConfigureServices(services =>
    {
        services.AddMyLibraryMigration();
    })
    .Build();
```

---

# Commands

Der eigentliche Ablauf wird in Commands gekapselt.

Beispiele:

```text
ImportCommand
ExportCommand
MigrationCommand
ReportCommand
```

Interface:

```csharp
ICommand
```

---

# Konfiguration

Standarddateien:

```text
appsettings.json
appsettings.Development.json
appsettings.Secrets.json
```

---

# Geheimnisse

Geheimnisse gehören ausschließlich in:

```text
appsettings.Secrets.json
```

Diese Datei wird nicht versioniert.

---

# Logging

Standard:

```text
Serilog
```

Beispiel:

```csharp
builder.Host.UseSerilog();
```

---

# Logging Ziele

Typische Ziele:

```text
Console
File
Seq
```

---

# Dependency Injection

Alle Services werden über DI bereitgestellt.

Beispiel:

```csharp
builder.Services.AddMyLibraryMigration();
```

---

# Datenbankzugriffe

Standard:

```text
Dapper
```

Die Regeln aus:

```text
Database-Standards.md
```

gelten vollständig.

---

# Fehlerbehandlung

Die Anwendung darf niemals unkontrolliert abbrechen.

Hauptfehlerbehandlung:

```csharp
try
{
}
catch(Exception ex)
{
}
```

im Einstiegspunkt.

Fehler werden geloggt.

---

# Exit Codes

Erfolgreich:

```text
0
```

Fehler:

```text
1
```

Weitere Codes dürfen projektspezifisch definiert werden.

---

# Parameter

Parameter werden über CommandLine-Argumente verarbeitet.

Beispiel:

```bash
MyLibrary.DataMigration.Console.exe migrate
```

```bash
MyLibrary.DataMigration.Console.exe import customers.json
```

---

# Lange Prozesse

Laufende Prozesse sollen Fortschritt ausgeben.

Beispiel:

```text
Importing customer 120 of 5000
```

oder

```text
23 % completed
```

---

# Cancellation

Lange Prozesse sollen CancellationToken unterstützen.

Beispiel:

```csharp
Task ExecuteAsync(
    CancellationToken cancellationToken);
```

---

# Dateien

Dateipfade dürfen nicht hardcodiert werden.

Nicht erlaubt:

```csharp
C:\Temp\data.json
```

Erlaubt:

```json
{
  "ImportFolder": ""
}
```

---

# Tests

Projekt:

```text
MyLibrary.<Name>.Console.Test
```

Framework:

```text
xUnit
```

---

# Testbare Komponenten

Zu testen:

* Commands
* Services
* Validatoren
* Konfiguration

Nicht zu testen:

* Program.cs

---

# README

README enthält:

* Beschreibung
* Installation
* Parameter
* Konfiguration
* Beispiele

---

# Beispiel

Projekt:

```text
MyLibrary.DataMigration.Console
```

Aufruf:

```bash
MyLibrary.DataMigration.Console migrate
```

---

# Standardpakete

```text
Microsoft.Extensions.Hosting
Microsoft.Extensions.DependencyInjection
Microsoft.Extensions.Configuration
Microsoft.Extensions.Logging
Serilog
Serilog.Extensions.Hosting
```

Optional:

```text
Dapper
```

---

# Review Checkliste

Vor dem ersten Release prüfen:

* Verwendet die Anwendung den Generic Host?
* Wird Serilog verwendet?
* Sind Secrets ausgelagert?
* Wird Dependency Injection verwendet?
* Ist die Businesslogik außerhalb von Program.cs?
* Werden Fehler geloggt?
* Existiert ein README?
* Existieren Unit Tests?
* Werden Exit Codes verwendet?
* Werden lange Prozesse abbrechbar ausgeführt?
