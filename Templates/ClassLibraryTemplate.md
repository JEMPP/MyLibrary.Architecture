# Class Library Template

Für neue .NET-Repositories gilt verbindlich der
[.NET Repository Standard](../Standards/DotNet-Repository-Standard.md):
eine `.slnx` im Repository-Root, jedes Produktiv- und Testprojekt in einem eigenen
gleichnamigen Unterordner mit seiner `.csproj`, Repository-Dokumentation im Root.
Historische `.sln`-Dateien müssen nicht allein deshalb migriert
werden; für neue Solutions keine parallele `.sln` anlegen.

Version: 1.0

Dieses Dokument beschreibt die Standardvorlage für neue Klassenbibliotheken der MyLibrary-Familie.

---

# Ziel

Eine neue Bibliothek soll:

* wiederverwendbar sein
* testbar sein
* GitHub-Ready sein
* NuGet-Ready sein
* den MyLibrary-Standards entsprechen

---

# Projektname

Schema:

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

# Solution Struktur

```text
MyLibrary.<Name>/  # Repository-Root
├── MyLibrary.<Name>.slnx
├── MyLibrary.<Name>/
│   └── MyLibrary.<Name>.csproj
├── MyLibrary.<Name>.Tests/
│   └── MyLibrary.<Name>.Tests.csproj
├── .gitignore
├── README.md
├── CHANGELOG.md
└── LICENSE
```

---

# Bibliotheksstruktur

```text
MyLibrary.<Name>

├─ Models
├─ Interfaces
├─ Services
├─ Extensions
├─ Configuration
├─ Exceptions
│
├─ Repositories
├─ Validators
├─ Infrastructure
```

---

# Testprojekt

```text
MyLibrary.<Name>.Tests

├─ Services
├─ Models
├─ Repositories
├─ Validators
└─ TestData
```

---

# Pflichtdateien

```text
README.md
CHANGELOG.md
LICENSE
.gitignore
```

---

# Dependency Injection

Jede Bibliothek stellt eine DI-Erweiterung bereit.

Datei:

```text
Extensions/ServiceCollectionExtensions.cs
```

Beispiel:

```csharp
builder.Services.AddEmail();
```

---

# Interfaces

Öffentliche Services besitzen Interfaces.

Beispiel:

```csharp
IEmailService
EmailService
```

---

# Logging

Standard:

```text
ILogger<T>
```

Die Bibliothek konfiguriert Serilog nicht selbst.

---

# Konfiguration

Konfigurationsklassen:

```csharp
EmailOptions
DatabaseOptions
WorkflowOptions
```

---

# Tests

Framework:

```text
xUnit
```

Projekt:

```text
MyLibrary.<Name>.Tests
```

---

# Standardpakete

```text
Microsoft.Extensions.DependencyInjection.Abstractions
Microsoft.Extensions.Logging.Abstractions
```

Optional:

```text
Dapper
Serilog
```

abhängig vom Einsatzzweck.

---

# Erstellung einer neuen Bibliothek

1. Neue Solution erstellen
2. Klassenbibliothek erstellen
3. xUnit-Testprojekt erstellen
4. Projektverweis setzen
5. README anlegen
6. LICENSE anlegen
7. .gitignore übernehmen
8. DI-Erweiterung anlegen
9. Erstes Interface definieren
10. Erste Tests erstellen
