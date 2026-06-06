# Development Standard

Version: 1.0

Dieses Dokument definiert die verbindlichen Entwicklungsrichtlinien für alle Projekte der MyLibrary-Familie.

---

# Ziele

Die MyLibrary-Projekte sollen:

* konsistent aufgebaut sein
* wartbar sein
* testbar sein
* wiederverwendbar sein
* dokumentiert sein
* GitHub-Ready sein
* NuGet-Ready sein
* Security-by-Default unterstützen

---

# Architekturprinzipien

## SOLID

Alle Projekte orientieren sich an den SOLID-Prinzipien.

* Single Responsibility Principle
* Open Closed Principle
* Liskov Substitution Principle
* Interface Segregation Principle
* Dependency Inversion Principle

---

## Separation of Concerns

Businesslogik darf nicht in UI-Komponenten implementiert werden.

### Erlaubte Schichten

```text
UI
↓
Services
↓
Repositories
↓
Datenquelle
```

### Nicht erlaubt

```text
UI
↓
SQL
```

```text
UI
↓
Businesslogik
```

---

# Projektstruktur

Standardstruktur einer Bibliothek:

```text
MyLibrary.<Name>

├─ Models
├─ Interfaces
├─ Services
├─ Extensions
├─ Configuration
├─ Exceptions
└─ Components (optional)
```

Optionale Ordner:

```text
Infrastructure
Repositories
Validators
Helpers
```

---

# Solution-Struktur

Jede Bibliothek besitzt eine eigene Solution.

Beispiel:

```text
MyLibrary.Email.sln

├─ MyLibrary.Email
└─ MyLibrary.Email.Test
```

---

# Dependency Injection

Alle Services werden über Dependency Injection bereitgestellt.

Direkte Instanziierungen mittels `new` außerhalb der Composition Root sollen vermieden werden.

Jede Bibliothek liefert eine eigene Registrierungs-Erweiterung:

```csharp
builder.Services.AddMyLibraryEmail();
```

Datei:

```text
Extensions/ServiceCollectionExtensions.cs
```

---

# Interfaces

Öffentliche Services erhalten Interfaces.

Beispiele:

```csharp
IEmailService
EmailService
```

```csharp
ILinkListService
LinkListService
```

---

# Services

Services enthalten die Geschäftslogik.

Services dürfen:

* Models verwenden
* Repositories verwenden
* andere Services verwenden
* Logger verwenden

Services sollen nicht:

* Razor-Code enthalten
* UI-Code enthalten
* HTML erzeugen
* SQL direkt in Komponenten ausführen

---

# Models

Models enthalten Datenstrukturen.

Erlaubt:

```csharp
public string EffectiveIcon =>
    string.IsNullOrWhiteSpace(Icon)
        ? "bi-link-45deg"
        : Icon;
```

Nicht erlaubt:

* Datenbankzugriffe
* HTTP-Aufrufe
* UI-Logik

---

# Logging

## Standard

Für Logging wird Serilog verwendet.

Bibliotheken selbst konfigurieren Serilog nicht.

Bibliotheken loggen ausschließlich über:

```csharp
ILogger<T>
```

Beispiel:

```csharp
private readonly ILogger<EmailService> _logger;
```

### Erlaubt

```csharp
_logger.LogInformation("E-Mail wurde versendet.");
_logger.LogWarning("SMTP Server antwortet langsam.");
_logger.LogError(ex, "Fehler beim Versand.");
```

### Nicht erlaubt

```csharp
Console.WriteLine(...)
```

```csharp
Serilog.Log.Information(...)
```

Direkte Serilog-Aufrufe innerhalb von Bibliotheken sind zu vermeiden.

Die konkrete Serilog-Konfiguration erfolgt in der Anwendung:

* Blazor
* ASP.NET Core
* Worker Service
* Console Application

---

# Asynchrone Programmierung

I/O-Operationen werden asynchron implementiert.

Beispiele:

```csharp
await httpClient.GetAsync(...)
```

```csharp
await repository.SaveAsync(...)
```

Vermeiden:

```csharp
.Result
```

```csharp
.Wait()
```

---

# Fehlerbehandlung

Eigene Exceptions werden im Ordner

```text
Exceptions
```

abgelegt.

Beispiele:

```csharp
EmailConfigurationException
```

```csharp
DatabaseConnectionException
```

---

# Konfiguration

Konfiguration erfolgt bevorzugt über JSON-Dateien.

Beispiele:

```text
appsettings.json
workflow-definitions.json
helpdesk-links.json
email-settings.json
```

Konfigurationsdaten werden nicht hardcodiert.

---

# Geheimnisse

Geheimnisse dürfen niemals im Repository gespeichert werden.

Beispiele:

* SMTP-Passwörter
* API-Keys
* Datenbank-Passwörter
* OAuth-Secrets

Datei:

```text
appsettings.Secrets.json
```

Diese Datei muss in `.gitignore` enthalten sein.

Beispiel:

```gitignore
appsettings.Secrets.json
```

---

# Datenbankzugriffe

Datenbankrichtlinien werden im Dokument

```text
Standards/Database-Standards.md
```

definiert.

Dort werden geregelt:

* Dapper
* SQL Server
* FirebirdSQL
* MS Access
* Repositories
* Connection Management
* Transaktionen
* Parameterisierung
* Performance-Richtlinien

---

# Blazor-Komponenten

Blazor-Komponenten sollen generisch entwickelt werden.

Beispiel:

```razor
<LinkList JsonPath="helpdesk-links.json" />
```

Nicht zulässig:

```razor
<LinkList HelpdeskMode="true" />
```

wenn dadurch projektspezifisches Verhalten entsteht.

---

# Wiederverwendbarkeit

Bibliotheken dürfen keine projektspezifischen Namen enthalten.

Nicht erwünscht:

```csharp
IntermetricWorkflowService
```

Bevorzugt:

```csharp
WorkflowService
```

---

# Dokumentation

Öffentliche Klassen erhalten XML-Kommentare.

Beispiel:

```csharp
/// <summary>
/// Service zum Versenden von E-Mails.
/// </summary>
public class EmailService
{
}
```

Öffentliche Methoden werden dokumentiert.

---

# Dateinamen

Dateiname entspricht Klassenname.

Beispiele:

```text
EmailService.cs
IEmailService.cs
EmailOptions.cs
```

Nicht erwünscht:

```text
Helper.cs
Utils.cs
Stuff.cs
```

---

# Testbarkeit

Geschäftslogik muss unabhängig von UI testbar sein.

Zu testen:

* Services
* Models
* Validatoren
* Repository-Logik

Nicht im Fokus von Unit Tests:

* Razor-Markup
* Layouts
* CSS

---

# GitHub

Jede Bibliothek enthält:

```text
README.md
LICENSE
.gitignore
```

sowie ein separates Testprojekt.

---

# Branch Standard

Standard-Branch:

```text
main
```

Der Branchname

```text
master
```

wird nicht verwendet.

Empfohlene Branches:

```text
main
feature/*
bugfix/*
hotfix/*
```

---

# Review-Checkliste

Vor jedem Commit prüfen:

* Ist der Code testbar?
* Ist der Code wiederverwendbar?
* Ist der Code dokumentiert?
* Ist der Code konfigurierbar?
* Ist der Code unabhängig von UI?
* Sind Geheimnisse ausgeschlossen?
* Wird Dependency Injection verwendet?
* Wird ILogger<T> verwendet?
* Werden Standards eingehalten?
