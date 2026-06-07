# Architecture AI Prompt

Version: 1.0

Dieses Dokument dient als kompakte Zusammenfassung der Architekturstandards für alle Projekte der MyLibrary-Familie.

Wenn ein Projekt analysiert, refaktoriert oder neu erstellt wird, gelten die folgenden Regeln.

---

# Projektstruktur

Standard:

```text
MyLibrary.<Name>
MyLibrary.<Name>.Test
```

Beispiele:

```text
MyLibrary.Email
MyLibrary.Email.Test

MyLibrary.LinkListe
MyLibrary.LinkListe.Test
```

Jede Bibliothek besitzt eine eigene Solution.

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

Jede Bibliothek stellt eine Erweiterungsmethode bereit:

```csharp
builder.Services.AddMyLibrary<Name>();
```

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
