# MyLibrary.Architecture

Dieses Repository definiert die Architektur-, Entwicklungs-, Test-, Sicherheits-, GitHub- und Prozessmodellierungsstandards für alle Projekte der **MyLibrary-Familie**.

Ziel ist eine einheitliche Struktur, Namensgebung und Vorgehensweise über alle Bibliotheken und Anwendungen hinweg.

Beispiele:

* MyLibrary.LinkListe
* MyLibrary.Email
* MyLibrary.Workflow
* MyLibrary.Reporting
* MyLibrary.Excel

---

# Ziele

* Konsistente Projektstruktur
* Wiederverwendbare Komponenten
* Hohe Testbarkeit
* Trennung von UI und Businesslogik
* SOLID-Prinzipien
* Security by Default
* GitHub-Ready
* NuGet-Ready
* Dokumentierte Standards

---

# Repository-Struktur

```text
MyLibrary.Architecture
│
├─ README.md
│
├─ Standards
│  ├─ DotNet-Repository-Standard.md
│  ├─ Development-Standard.md
│  ├─ Naming-Conventions.md
│  ├─ GitHub-Standards.md
│  ├─ Security-Standards.md
│  └─ Testing-Standards.md
│
├─ Templates
│  ├─ BlazorAppTemplate.md
│  ├─ ReadmeTemplate.md
│  ├─ GitIgnoreTemplate.md
│  └─ LibraryStructure.md
│
└─ Examples
```

---

# Standards

| Dokument                       | Beschreibung                                                            |
| ------------------------------ | ----------------------------------------------------------------------- |
| [DotNet-Repository-Standard.md](Standards/DotNet-Repository-Standard.md) | Verbindliche Struktur neuer .NET-Repositories |
| Development-Standard.md        | Allgemeine Entwicklungsrichtlinien                                      |
| Naming-Conventions.md          | Namenskonventionen für Projekte und Code                                |
| GitHub-Standards.md            | GitHub-, Git- und Branching-Standards                                   |
| Security-Standards.md          | Umgang mit Geheimnissen und Sicherheit                                  |
| Testing-Standards.md           | Unit-Test- und Qualitätsrichtlinien                                     |
| Process-Modeling-Standards.md  | Modellierung, Versionierung und Veröffentlichung von Geschäftsprozessen |

---

# Grundprinzipien

## Architektur

* Businesslogik gehört in Services.
* UI enthält keine Geschäftslogik.
* Dependency Injection wird verwendet.
* Öffentliche APIs werden dokumentiert.

## Testbarkeit

* Bibliotheken und neue Anwendungen, Services, Worker und APIs mit testbarer Logik
  besitzen ein separates `<Produktivprojekt>.Tests`-Projekt.
* Businesslogik muss unabhängig von UI testbar sein.
* xUnit ist das Standard-Testframework.

## Konfiguration

* Konfiguration erfolgt bevorzugt über JSON-Dateien.
* Keine Hardcodierung projektspezifischer Daten.
* Geheimnisse werden niemals im Repository gespeichert.

## Sicherheit

Folgende Dateien dürfen niemals eingecheckt werden:

```text
appsettings.Secrets.json
```

Diese Dateien müssen in `.gitignore` aufgenommen werden.

---

# Standardprojektstruktur

Für neue .NET-Repositories gilt der verbindliche
[.NET Repository Standard](Standards/DotNet-Repository-Standard.md):
eine `.slnx` im Root, Produktiv- und Testprojekte jeweils in eigenen gleichnamigen
Unterordnern und README, CHANGELOG, .gitignore sowie LICENSE im Root.
Keine Projektdateien im Root und keine parallele `.sln` für dieselbe neue Solution.
Bestehende historische `.sln`-Dateien und Strukturen müssen nicht allein deshalb
migriert werden.

Für Anwendungen siehe [Erstellungsprozess](Processes/Create-New-Application-Process.md)
und [Blazor-App-Template](Templates/BlazorAppTemplate.md). Nutzerseitige Blazor-Apps
enthalten Beschreibung, Hilfe und versionierte Release Notes im Projekt-Webroot
und eine über die Navigation erreichbare Informationsseite.

Für jede neue Bibliothek wird folgendes Schema verwendet:

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

Beispiel:

```text
MyLibrary.Email/  # Repository-Root
├── MyLibrary.Email.slnx
├── MyLibrary.Email/
│   └── MyLibrary.Email.csproj
├── MyLibrary.Email.Tests/
│   └── MyLibrary.Email.Tests.csproj
├── .gitignore
├── README.md
├── CHANGELOG.md
└── LICENSE
```

---

# Branch-Strategie

Standard-Branch:

```text
main
```

Der Branchname `master` wird nicht verwendet.

Empfohlene Branchtypen:

```text
main
feature/*
bugfix/*
hotfix/*
```

---

# Verwendung

Bei der Erstellung neuer Bibliotheken oder Anwendungen ist dieser Standard verbindlich anzuwenden.

Beispiel:

> Erstelle eine neue Bibliothek MyLibrary.Email gemäß dem Standard aus MyLibrary.Architecture.

---

# Lizenz

Dieses Repository dient ausschließlich der Definition von Standards, Vorlagen und Richtlinien für die MyLibrary-Projektfamilie.
