# Refactor Library Prompt

## Architekturreferenz

Verwende die Architekturstandards aus diesem Repository.

Lies zunächst:

```text
Architecture-AI-Prompt.md
```

Diese Datei stellt die primäre Zusammenfassung der Architektur dar.

Verwende anschließend bei Bedarf die Detaildokumente:

```text
Standards/*
Templates/*
```

Falls Widersprüche auftreten, gilt folgende Priorität:

1. Architecture-AI-Prompt.md
2. Standards/*
3. Templates/*

---

## Aufgabe

Analysiere und refaktoriere die hochgeladene Bibliothek gemäß den Standards aus MyLibrary.Architecture.

---

## Eingaben

Bestehende Bibliothek:

```text
MyLibrary.<Name>
```

Optional vorhandenes Razorprojekt:

```text
MyLibrary.<Name>.Razor
```

Optional vorhandenes Testprojekt:

```text
MyLibrary.<Name>.Tests
```

Falls mehrere Projekte vorhanden sind, identifiziere zuerst die relevante Bibliothek und das passende Testprojekt.

---

## Ziel

Die bestehende Bibliothek soll schrittweise an die Standards aus MyLibrary.Architecture angepasst werden.

Bestehende Funktionalität muss erhalten bleiben.

---

## Zu berücksichtigende Standards

Berücksichtige insbesondere:

* Development Standards
* Database Standards
* Security Standards
* Testing Standards
* Naming Conventions
* GitHub Standards

---

## Analyse

Erstelle zunächst eine Übersicht über:

* aktuelle Solution-Struktur
* aktuelle Projektstruktur
* vorhandene Namespaces
* vorhandene Models
* vorhandene Services
* vorhandene Interfaces
* vorhandene Repositories
* vorhandene Konfiguration
* vorhandene Tests
* externe NuGet-Abhängigkeiten
* Datenbankzugriffe
* Logging
* Blazor-Komponenten, falls vorhanden

---

## Abweichungen vom Standard

Identifiziere Abweichungen in folgenden Bereichen:

* Projektstruktur
* Ordnerstruktur
* Naming Conventions
* Dependency Injection
* Interfaces
* Services
* Logging
* Konfiguration
* Security
* Tests
* Datenbankzugriffe
* README / Dokumentation
* GitHub-Readiness
* NuGet-Readiness

---

## Refactoring-Plan

Erstelle danach einen konkreten Refactoring-Plan.

Gliedere den Plan in sinnvolle Schritte:

1. Struktur bereinigen
2. Namespaces korrigieren
3. Interfaces einführen oder bereinigen
4. Services extrahieren oder vereinheitlichen
5. Dependency Injection ergänzen
6. Logging auf `ILogger<T>` umstellen
7. Configuration / Options ergänzen
8. Datenbankzugriffe prüfen
9. Tests ergänzen
10. README aktualisieren
11. Razor-Komponenten in `MyLibrary.<Name>.Razor` auslagern, falls vorhanden
12. Host-Anwendungen auf AdditionalAssemblies prüfen

---

## Codeänderungen

Erzeuge anschließend konkrete Codevorschläge.

Bevorzuge:

* kleine nachvollziehbare Änderungen
* minimale Eingriffe mit maximalem Nutzen
* schrittweise Migration
* klare Dateinamen
* vollständige Klassen
* kopierbare Codeblöcke

Vermeide:

* unnötige Komplettneuschreibung
* Änderung der öffentlichen API ohne Grund
* Verlust bestehender Funktionalität
* projektspezifische Hardcodierung

---

## Datenbankzugriffe

Falls Datenbankzugriffe vorhanden sind:

* Dapper verwenden
* Repository Pattern prüfen
* IDbConnectionFactory vorsehen
* SQL parameterisieren
* Connection Strings auslagern
* keine Secrets einchecken
* Database-Standards berücksichtigen

---

## Logging

Falls Logging vorhanden ist:

* Bibliotheken verwenden ILogger<T>
* Serilog wird nur in der Host-Anwendung konfiguriert
* keine direkten Serilog-Aufrufe in Bibliotheken
* kein Console.WriteLine in Bibliotheken

---

## Konfiguration

Falls Konfiguration vorhanden ist:

* Options-Klassen verwenden
* appsettings.json berücksichtigen
* appsettings.Secrets.json für Geheimnisse verwenden
* keine Zugangsdaten hardcodieren

---

## Blazor-Komponenten

Falls Blazor-Komponenten vorhanden sind:

* Razor Class Library Struktur prüfen
* Komponenten generisch halten
* keine projektspezifischen URLs
* keine Kundennamen
* Logik in Services auslagern
* Parameter oder JSON für Konfiguration verwenden

Falls Komponenten `@page` verwenden, muss geprüft werden:

* `Routes.razor` enthält `AdditionalAssemblies`
* `Program.cs` enthält `AddAdditionalAssemblies(...)`

---

## Tests

Prüfe vorhandene Tests.

Falls Tests fehlen oder unvollständig sind:

* xUnit-Testprojekt vorschlagen oder ergänzen
* Tests für Services ergänzen
* Tests für Models mit Logik ergänzen
* Tests für Validatoren ergänzen
* Testdaten in TestData ablegen

---

## Erwartete Ausgabe

Liefere die Ergebnisse in dieser Reihenfolge:

1. Kurzbewertung der aktuellen Bibliothek
2. Gefundene Abweichungen vom Standard
3. Priorisierter Refactoring-Plan
4. Konkrete Codeänderungen
5. Tests oder Testvorschläge
6. README- oder Dokumentationsvorschlag
7. Empfohlene Commit-Reihenfolge

---

## Commit-Empfehlung

Schlage sinnvolle kleine Commits vor.

Beispiele:

```text
Refactor project structure
Add dependency injection extensions
Add service interfaces
Replace direct logging with ILogger
Add unit tests
Update README
```

---

## Wichtige Regeln

Erzeuge konkrete Codeänderungs-Vorschläge.

Bestehende Funktionalität muss erhalten bleiben.

Wenn Annahmen notwendig sind, triff sinnvolle Annahmen und benenne sie kurz.

Frage nur nach, wenn ohne Klärung kein sinnvoller Refactoring-Vorschlag möglich ist.
