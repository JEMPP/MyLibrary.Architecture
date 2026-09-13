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
│  ├─ Development-Standard.md
│  ├─ Naming-Conventions.md
│  ├─ GitHub-Standards.md
│  ├─ Security-Standards.md
│  └─ Testing-Standards.md
│
├─ Templates
│  ├─ ReadmeTemplate.md
│  ├─ GitIgnoreTemplate.txt
│  └─ LibraryStructure.md
│
└─ Examples
```

---

# Standards

| Dokument                       | Beschreibung                                                            |
| ------------------------------ | ----------------------------------------------------------------------- |
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

* Jede Bibliothek besitzt ein eigenes Testprojekt.
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

Für jede Bibliothek wird folgendes Schema verwendet:

```text
MyLibrary.<Name>.sln

├─ MyLibrary.<Name>
└─ MyLibrary.<Name>.Test
```

Beispiel:

```text
MyLibrary.Email.sln

├─ MyLibrary.Email
└─ MyLibrary.Email.Test
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
