# Worker Service Template

Version: 1.0

Dieses Dokument beschreibt die Standardvorlage für Worker Services der MyLibrary-Familie.

---

# Ziel

Worker Services werden verwendet für:

* Hintergrundverarbeitung
* Synchronisationen
* geplante Aufgaben
* Import-/Export-Prozesse
* Schnittstellenjobs
* Datenbankabgleiche
* Monitoring
* Wartungsprozesse

---

# Projekttyp

Visual Studio:

```text
Worker Service
```

Projektname:

```text
MyLibrary.<Name>.Worker
```

Beispiele:

```text
MyLibrary.Email.Worker
MyLibrary.Sync.Worker
MyLibrary.Reporting.Worker
MyLibrary.Workflow.Worker
```

---

# Solution Struktur

```text
MyLibrary.<Name>.Worker.sln

├─ MyLibrary.<Name>.Worker
└─ MyLibrary.<Name>.Worker.Test
```

Optional bei gemeinsamer Businessbibliothek:

```text
MyLibrary.<Name>.Worker.sln

├─ MyLibrary.<Name>
├─ MyLibrary.<Name>.Worker
└─ MyLibrary.<Name>.Worker.Test
```

---

# Projektstruktur

```text
MyLibrary.<Name>.Worker

├─ Services
├─ Workers
├─ Configuration
├─ Extensions
├─ Models
├─ Exceptions
└─ Program.cs
```

Optional:

```text
Repositories
Infrastructure
Validators
```

---

# Program.cs

Program.cs enthält nur:

* Host-Aufbau
* Dependency Injection
* Logging-Konfiguration
* Konfiguration
* Registrierung der Worker

Keine Businesslogik.

---

# Worker-Klassen

Worker liegen im Ordner:

```text
Workers
```

Beispiele:

```text
EmailWorker
SyncWorker
ImportWorker
CleanupWorker
```

---

# BackgroundService

Worker erben von:

```csharp
BackgroundService
```

Beispiel:

```csharp
public class SyncWorker : BackgroundService
{
    protected override async Task ExecuteAsync(
        CancellationToken stoppingToken)
    {
    }
}
```

---

# Geschäftslogik

Businesslogik gehört nicht direkt in den Worker.

Der Worker orchestriert nur.

Erlaubt:

```text
Worker
↓
Service
↓
Repository
```

Nicht erlaubt:

```text
Worker
↓
SQL
```

---

# Dependency Injection

Services werden über DI registriert.

Beispiel:

```csharp
builder.Services.AddHostedService<SyncWorker>();
builder.Services.AddMyLibrarySync();
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

# Secrets

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

Worker verwenden im Code:

```csharp
ILogger<T>
```

Beispiel:

```csharp
private readonly ILogger<SyncWorker> _logger;
```

Keine direkten Aufrufe von:

```csharp
Console.WriteLine(...)
```

oder:

```csharp
Serilog.Log.Information(...)
```

innerhalb der Worker-Klassen.

---

# Fehlerbehandlung

Worker dürfen bei einzelnen Fehlern nicht unkontrolliert abstürzen.

Fehler werden geloggt.

Beispiel:

```csharp
try
{
    await _syncService.ExecuteAsync(stoppingToken);
}
catch (Exception ex)
{
    _logger.LogError(ex, "Fehler im SyncWorker.");
}
```

---

# Schleifen

Lang laufende Worker verwenden kontrollierte Schleifen.

Beispiel:

```csharp
while (!stoppingToken.IsCancellationRequested)
{
    await _syncService.ExecuteAsync(stoppingToken);

    await Task.Delay(
        TimeSpan.FromMinutes(5),
        stoppingToken);
}
```

---

# CancellationToken

Jede lang laufende Operation unterstützt:

```csharp
CancellationToken
```

Beispiel:

```csharp
Task ExecuteAsync(CancellationToken cancellationToken);
```

---

# Intervalle

Intervalle werden nicht hardcodiert.

Nicht erlaubt:

```csharp
await Task.Delay(300000);
```

Erlaubt:

```json
{
  "Worker": {
    "IntervalMinutes": 5
  }
}
```

---

# Options

Konfigurationsklassen enden mit:

```text
Options
```

Beispiel:

```csharp
public class WorkerOptions
{
    public int IntervalMinutes { get; set; } = 5;
}
```

---

# Datenbankzugriffe

Datenbankzugriffe erfolgen nicht direkt im Worker.

Verwendet wird:

```text
Service
↓
Repository
↓
Dapper
```

Die Regeln aus:

```text
Standards/Database-Standards.md
```

gelten vollständig.

---

# Windows Service

Worker Services können als Windows Service betrieben werden.

Optionales Paket:

```text
Microsoft.Extensions.Hosting.WindowsServices
```

Beispiel:

```csharp
builder.Host.UseWindowsService();
```

---

# Systemd / Linux

Worker Services können unter Linux als systemd Service betrieben werden.

Deployment-Regeln werden projektspezifisch dokumentiert.

---

# Health Checks

Für kritische Worker sollen Health Checks oder Monitoring vorgesehen werden.

Zu überwachen:

* letzter erfolgreicher Lauf
* letzter Fehler
* Laufzeit
* Datenmenge
* Zielsystem erreichbar

---

# Idempotenz

Worker-Jobs sollen möglichst idempotent sein.

Das bedeutet:

* ein wiederholter Lauf darf keine falschen Doppelverarbeitungen erzeugen
* unterbrochene Jobs können erneut gestartet werden

---

# Parallelität

Parallelverarbeitung muss bewusst geplant werden.

Zu prüfen:

* Datenbank-Locks
* doppelte Verarbeitung
* Reihenfolgeabhängigkeiten
* Transaktionen

---

# Transaktionen

Mehrere zusammengehörige Datenänderungen werden transaktional verarbeitet.

Die Regeln aus `Database-Standards.md` gelten.

---

# Tests

Testprojekt:

```text
MyLibrary.<Name>.Worker.Test
```

Framework:

```text
xUnit
```

Zu testen:

* Services
* Options
* Validatoren
* Job-Logik

Nicht primär zu testen:

* Endlosschleife des Workers
* Program.cs

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
Microsoft.Extensions.Hosting.WindowsServices
Dapper
```

---

# README

README enthält:

* Zweck des Workers
* Installation
* Konfiguration
* Secrets
* Logging
* Start als Konsole
* Betrieb als Windows Service
* Tests

---

# Beispiel Program.cs

```csharp
using Serilog;

var builder = Host.CreateApplicationBuilder(args);

builder.Services.AddHostedService<SyncWorker>();

builder.Services.AddMyLibrarySync();

builder.Logging.ClearProviders();

builder.Host.UseSerilog();

var host = builder.Build();

await host.RunAsync();
```

---

# Review Checkliste

Vor dem ersten Release prüfen:

* Enthält Program.cs keine Businesslogik?
* Ist die Worker-Logik schlank?
* Liegt Businesslogik in Services?
* Sind Datenbankzugriffe in Repositories?
* Werden CancellationToken verwendet?
* Sind Intervalle konfigurierbar?
* Werden Secrets nicht eingecheckt?
* Wird Serilog verwendet?
* Wird ILogger<T> im Code verwendet?
* Sind Fehler sauber geloggt?
* Ist der Worker idempotent?
* Existieren Tests?
* Ist der Betrieb als Windows Service dokumentiert?
