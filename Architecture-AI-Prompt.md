# Architecture AI Prompt

Version: 1.0

Dieses Dokument dient als kompakte Zusammenfassung der Architekturstandards für alle Projekte der MyLibrary-Familie.

Wenn ein Projekt analysiert, refaktoriert oder neu erstellt wird, gelten die folgenden Regeln.

---

# Projektstruktur

Standard:

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

Der Methodenname wird aus dem Bibliotheksnamen ohne das Präfix `MyLibrary.` gebildet:

```csharp
builder.Services.Add{LibraryName}();
```

Beispiele:

```csharp
builder.Services.AddLinkListe();
builder.Services.AddEmail();
builder.Services.AddExcelExport();
```

Zuordnung:

| Bibliothek            | DI-Methode       |
| --------------------- | ---------------- |
| MyLibrary.LinkListe   | AddLinkListe()   |
| MyLibrary.Email       | AddEmail()       |
| MyLibrary.ExcelExport | AddExcelExport() |

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

Jede Bibliothek besitzt ein eigenes Testprojekt.

Namensschema:

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

Bevorzugt:

```text
Razor Class Library
```

Komponenten sollen generisch sein.

Nicht zulässig:

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
