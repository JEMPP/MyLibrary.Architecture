# Changelog

## Unreleased

### Changed

- Neue .NET-Repositories verwenden `.slnx` im Root und Produktiv-/Testprojekte
  in eigenen Unterordnern; keine Projektdateien im Root und keine parallele `.sln`.
- `<Produktivprojekt>.Tests` und separate xUnit-Testprojekte gelten auch für
  Anwendungen, APIs, Services, Worker und Konsolenanwendungen mit testbarer Logik.
- Aktive Standards, Vorlagen, Prozesse und Prompts konsistent angepasst.
  Historische Solutionformate und Releaseinformationen bleiben unverändert gültig.

### Added

- Verbindlicher .NET Repository Standard mit Ablage-, Naming- und Prüfregeln.
- Blazor-App-Template mit Beschreibung, Hilfe und versionierter Historie im Webroot
  sowie Informationsseite und Navigation nach dem Urlaub-Muster.
- Eigener Prozess zur Erstellung neuer .NET-Anwendungen.

---

## v1.0.0

Initial release

### Standards

- Development Standard
- Database Standard
- Security Standard
- Testing Standard
- Naming Conventions
- GitHub Standards

### Templates

- Class Library
- Blazor Library
- Console App
- Worker Service
- Web API

---

## v1.1.0

Planned

- Process Modeling Standard
- Standard fÃ¼r versionierte GeschÃ¤ftsprozessdokumentation
- Vorbereitung der VerÃ¶ffentlichung von GeschÃ¤ftsprozessen in iOrga
- NuGet Standards
- Documentation Standards
- Docker Standards

---

## v1.2.0

2026-06-07  Add requirements engineering workflow

---

## v1.2.1

2026-06-07  Added archive and package exclusion rules to GitIgnoreTemplate and GitHub Standards.

---

## v1.2.2

2026-06-07  Gitignore - comments augmented

---

## v1.2.3

2026-06-07  Added Quickstart for AI

---

## v1.2.4

2026-06-07  define library-specific DI registration methods

---

## v1.3.0

2026-08-02  Define module architecture standard and new Prompts

---

## v1.4.0

2026-08-02  MyLibrary.Architecture v1.4.0 - Release standard and checklist

---

## v1.4.1

2026-08-02  MyLibrary.Architecture v1.4.1 - Release-Checkliste verfeinert

---

## v1.5.0

2026-09-27  Standardize test project and DI naming

### Changed

- Testprojekte werden einheitlich im Plural benannt:
  - `MyLibrary.<Name>.Tests`
  - `MyLibrary.<Name>.Console.Tests`
  - `MyLibrary.<Name>.Api.Tests`
  - `MyLibrary.<Name>.Worker.Tests`

- Dependency-Injection-Konventionen vereinheitlicht:
  - fachlich etablierte Bibliotheken verwenden `Add<Name>()`
  - Beispiele: `AddEmail()`, `AddPdf()`, `AddGaeb()`, `AddLinkListe()`
  - interne oder generische Infrastruktur darf `AddMyLibrary<Name>()` verwenden
  - Beispiele: `AddMyLibraryDataAccess()`, `AddMyLibraryCore()`

- Architekturprompt, Standards, Prozesse und Templates an die neuen Konventionen angepasst.

---
