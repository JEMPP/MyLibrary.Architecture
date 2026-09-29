# Architecture AI Prompt

Version: 1.0

Dieses Dokument dient als kompakte Zusammenfassung der Architekturstandards für alle Projekte der MyLibrary-Familie.

Wenn ein Projekt analysiert, refaktoriert oder neu erstellt wird, gelten die folgenden Regeln.

---

# Projektstruktur

Für neue .NET-Repositories gelten `.slnx` im Repository-Root und eigene
gleichnamige Unterordner für jedes Produktiv- und Testprojekt. Projektdateien
liegen nicht im Repository-Root. Keine parallele `.sln` für dieselbe neue Solution.
Historische `.sln` und ältere Repositorystrukturen müssen nicht allein wegen
dieser Regel migriert werden. README, CHANGELOG, .gitignore und LICENSE liegen im Root.

Anwendungen (Repository/Application: `<AppName>`):

```text
<AppName>/
├── <AppName>.slnx
├── <AppName>/
│   └── <AppName>.csproj
├── <AppName>.Tests/
│   └── <AppName>.Tests.csproj
├── .gitignore
├── README.md
├── CHANGELOG.md
└── LICENSE
```

Beispiel: `GaebApp`, `GaebApp/GaebApp.csproj`,
`GaebApp.Tests/GaebApp.Tests.csproj`, `GaebApp.slnx`.
Details: [DotNet Repository Standard](Standards/DotNet-Repository-Standard.md).

Bibliotheken:

```text
MyLibrary.<Name>
MyLibrary.<Name>.Razor
MyLibrary.<Name>.Tests
```
Bei Bibliotheken ohne Blazor UI kann auf das Projekt `MyLibrary.<Name>.Razor`
verzichtet werden.

UI-Komponenten sind bevorzugt in Razor Class Libraries auszulagern.

Jede Bibliothek besitzt eine eigene Solution.

Beispiele:

```text
MyLibrary.Core
MyLibrary.Core.Tests

MyLibrary.Email
MyLibrary.Email.Razor
MyLibrary.Email.Tests

MyLibrary.LinkListe
MyLibrary.LinkListe.Razor
MyLibrary.LinkListe.Tests
```

---

# Architektur

Businesslogik gehört in Services.

Erlaubt:

```text
UI
↓
Services
↓
Repositories
↓
Datenbank
```

Nicht erlaubt:

```text
UI
↓
SQL
```

oder

```text
UI
↓
Businesslogik
```

---

# Dependency Injection

Alle Services werden über Dependency Injection registriert.

Jede Bibliothek stellt genau eine öffentliche `IServiceCollection`-Erweiterungsmethode als primären Einstiegspunkt bereit.

## Namenskonvention

Der Methodenname wird grundsätzlich aus dem Bibliotheksnamen ohne das Präfix
`MyLibrary.` gebildet:

```csharp
builder.Services.Add{LibraryName}();
```

Für interne oder sehr generisch benannte Infrastrukturkomponenten darf zur
Eindeutigkeit das Präfix `MyLibrary` verwendet werden:

```csharp
builder.Services.AddMyLibrary{LibraryName}();
```

Dies ist insbesondere sinnvoll, wenn der Name ohne Präfix zu allgemein oder
kollisionsanfällig wäre.

Beispiele:

```csharp
builder.Services.AddLinkListe();
builder.Services.AddEmail();
builder.Services.AddPdf();
builder.Services.AddGaeb();
builder.Services.AddExcelExport();

builder.Services.AddMyLibraryDataAccess();
builder.Services.AddMyLibraryCore();
```

Zuordnung:

| Bibliothek                | Einordnung                         | DI-Methode                  |
| ------------------------- | ---------------------------------- | --------------------------- |
| MyLibrary.LinkListe       | fachlich etablierter Name          | `AddLinkListe()`            |
| MyLibrary.Email           | fachlich etablierter Name          | `AddEmail()`                |
| MyLibrary.Pdf             | fachlich etablierter Name          | `AddPdf()`                  |
| MyLibrary.Gaeb            | fachlich etablierter Name          | `AddGaeb()`                 |
| MyLibrary.ExcelExport     | fachlich etablierter Name          | `AddExcelExport()`          |
| MyLibrary.DataAccess      | generische Infrastruktur           | `AddMyLibraryDataAccess()`  |
| MyLibrary.Core            | interne/generische Infrastruktur   | `AddMyLibraryCore()`        |

## Eindeutigkeit

Der Methodenname soll möglichst kurz und verständlich sein.

Falls der Name einer Bibliothek zu Konflikten mit anderen Bibliotheken führen könnte, MUSS ein eindeutigerer Bibliotheksname gewählt werden.

Beispiele:

```csharp
AddSmtpEmail();
AddSendGridEmail();
AddExcelExport();
```

statt:

```csharp
AddEmail();
```

wenn mehrere E-Mail-Bibliotheken existieren.

## Namenskonflikte

Sollte in einem Projekt dennoch ein Konflikt zwischen gleichnamigen Erweiterungsmethoden entstehen, kann der Aufruf jederzeit über den vollständigen Typnamen oder einen Namespace-Alias erfolgen.

Dies stellt keinen Architekturverstoß dar und erfordert keine Änderung der Bibliothek.

## Aggregator-Bibliotheken

Methoden mit dem Namen

```csharp
builder.Services.AddMyLibrary();
```

sind ausschließlich für Aggregator-, Meta- oder Bundle-Pakete vorgesehen, die mehrere MyLibrary-Bibliotheken gemeinsam registrieren.

Beispiel:

```csharp
builder.Services.AddMyLibrary();
```

registriert intern beispielsweise:

```csharp
builder.Services.AddLinkListe();
builder.Services.AddEmail();
builder.Services.AddExcelExport();
```

Einzelbibliotheken dürfen `AddMyLibrary()` nicht als primären Registrierungspunkt verwenden.

## Rückwärtskompatibilität

Bei Refactorings dürfen bestehende DI-Methoden vorübergehend als Alias erhalten bleiben, um Breaking Changes zu vermeiden.

Neue Dokumentation und Beispiele müssen jedoch immer die bibliotheksspezifische Methode verwenden.

---

# Datenbankzugriffe

Standard:

```text
Dapper
```

Nicht verwenden:

```text
Entity Framework Core
```

außer wenn ausdrücklich gefordert.

Verwendete Datenbanken:

* Microsoft SQL Server
* Firebird SQL
* Microsoft Access

SQL wird sichtbar geschrieben.

SQL-Parameter sind verpflichtend.

---

# Logging

Standard:

```text
Serilog
```

Bibliotheken verwenden:

```csharp
ILogger<T>
```

Bibliotheken konfigurieren Serilog nicht selbst.

---

# Authentifizierung

Bevorzugter Standard:

```text
Windows Authentication
```

Ziele:

* Single Sign-On
* Arbeiten im Benutzerkontext
* Integration mit Active Directory

Benutzerinformationen sollen über einen Service abstrahiert werden:

```csharp
ICurrentUserService
```

---

# Zukunft

Die Architektur soll auf Microsoft Entra ID vorbereitbar sein.

Anwendungen dürfen nicht fest an Windows Authentication gekoppelt werden.

---

# Tests

Standard:

```text
xUnit
```

Jede Bibliothek sowie jede neue Anwendung, API, jeder Service oder Worker mit
testbarer Logik erhält ein separates Testprojekt `<Produktivprojekt>.Tests`.
Dieses referenziert das Produktivprojekt und wird in die Solution aufgenommen.
Geschäfts-, Zustands-, Mapping-, Berechnungs-, Validierungs- und Anwendungslogik
muss außerhalb der UI testbar sein und im Testprojekt geprüft werden.
Nicht jede Razor-Darstellung benötigt einen isolierten Test.

Namensschema für Testklassen:

```text
<ClassName>Tests
```

---

# Namenskonventionen

Interfaces:

```text
IEmailService
ICustomerRepository
```

Services:

```text
EmailService
WorkflowService
```

Repositories:

```text
CustomerRepository
```

Exceptions:

```text
EmailConfigurationException
```

Options:

```text
EmailOptions
DatabaseOptions
```

---

# Blazor

Neue nutzerseitige Anwendungen folgen verbindlich dem
[Blazor-App-Template](Templates/BlazorAppTemplate.md) und dem
[Erstellungsprozess](Processes/Create-New-Application-Process.md).
Pflicht sind `wwwroot/about.md`, `wwwroot/help.md` und
`wwwroot/release-notes/v<Version>.md` innerhalb des Produktivprojekts sowie eine
über die Navigation erreichbare Informationsseite mit Beschreibung, Hilfe und
Versionshistorie nach dem Urlaub-Muster. App-spezifische Namen sind im Host erlaubt.

Für wiederverwendbare UI-Komponenten bevorzugt:

```text
Razor Class Library
```

Wiederverwendbare Bibliothekskomponenten sollen generisch sein.

In diesen Bibliothekskomponenten nicht zulässig:

* Kundennamen im Code
* Projektnamen im Code
* Hardcodierte URLs

Konfiguration erfolgt über Parameter oder JSON.

---

# Sicherheit

Geheimnisse gehören niemals ins Repository.

Verwenden:

```text
appsettings.Secrets.json
```

Diese Datei muss in `.gitignore` enthalten sein.

---

# GitHub

Standardbranch:

```text
main
```

Nicht verwenden:

```text
master
```

Versionierung:

```text
MAJOR.MINOR.PATCH
```

Beispiel:

```text
v1.0.0
```

---

# Ziel bei Refactorings

Bestehende Projekte sollen schrittweise an diesen Standard angepasst werden.

Vorgehen:

1. Analyse
2. Abweichungen identifizieren
3. Refactoring-Plan erstellen
4. Umbau in kleinen Schritten
5. Tests ergänzen
6. Dokumentation aktualisieren

Nicht sofort alles neu schreiben.

Bestehende Funktionalität muss erhalten bleiben.

---

# Referenz

Weitere Details befinden sich in:

```text
Standards/*
Templates/*
```

dieses Repositories.
