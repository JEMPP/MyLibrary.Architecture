# Create New Library Prompt

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

Erstelle eine neue Bibliothek gemäß den Standards aus MyLibrary.Architecture.

---

## Eingaben

Name der Bibliothek:

```text
MyLibrary.<Name>
```

Typ der Bibliothek:

```text
Class Library
Blazor Library
Console App
Worker Service
Web API
```

Falls kein Typ angegeben ist, verwende:

```text
Class Library
```

---

## Zielstruktur

Die Lösung soll grundsätzlich folgende Struktur erhalten:

```text
MyLibrary.<Name>.sln

├─ MyLibrary.<Name>
└─ MyLibrary.<Name>.Test
```

Bei speziellen Projekttypen gelten die passenden Templates aus:

```text
Templates/*
```

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

## Erwartete Ausgabe

Erzeuge eine vollständige Zielarchitektur mit:

* Solution-Struktur
* Projektstruktur
* Ordnerstruktur
* Namespaces
* Interfaces
* Services
* Models
* Configuration
* Exceptions
* Extensions
* Testprojekt

Erzeuge außerdem:

* README.md
* ServiceCollectionExtensions.cs
* Beispiel für Dependency Injection
* Beispiel für Konfiguration
* Beispiel für Unit Tests

---

## Technische Standards

Verwende als Standard:

* Dapper für Datenbankzugriffe
* Serilog als Logging-Standard
* ILogger<T> innerhalb von Bibliotheken
* xUnit für Tests
* main als Standardbranch
* appsettings.Secrets.json für Geheimnisse

---

## Datenbankzugriffe

Falls die Bibliothek Datenbankzugriffe benötigt:

* Repository Pattern verwenden
* IDbConnectionFactory verwenden
* Dapper verwenden
* SQL parameterisieren
* Connection Strings nicht hardcodieren
* Database-Standards berücksichtigen

---

## Blazor-Komponenten

Falls die Bibliothek Blazor-Komponenten enthält:

* Razor Class Library verwenden
* Components-Ordner verwenden
* generische Komponenten entwickeln
* keine projektspezifischen URLs verwenden
* keine Kundennamen verwenden
* Konfiguration über Parameter oder JSON

---

## Authentifizierung

Falls Authentifizierung erforderlich ist:

* Windows Authentication bevorzugen
* Single Sign-On berücksichtigen
* ICurrentUserService vorsehen
* Benutzerkontext abstrahieren
* zukünftige Migration zu Microsoft Entra ID berücksichtigen

---

## Vorgehen

Arbeite in dieser Reihenfolge:

1. Architektur kurz zusammenfassen
2. Passendes Template auswählen
3. Zielstruktur darstellen
4. Benötigte Klassen und Dateien auflisten
5. Code für die wichtigsten Dateien erzeugen
6. Testprojekt vorschlagen
7. README-Inhalt erzeugen
8. Nächste Umsetzungsschritte nennen

---

## Qualitätsanforderungen

Die erzeugte Bibliothek soll:

* sofort als Ausgangspunkt verwendbar sein
* testbar sein
* wiederverwendbar sein
* erweiterbar sein
* GitHub-ready sein
* NuGet-ready sein
* keine projektspezifischen Namen enthalten
* keine Geheimnisse enthalten
* den Standards aus MyLibrary.Architecture entsprechen

---

## Wichtige Regel

Erzeuge konkrete Codevorschläge.

Wenn Annahmen notwendig sind, triff sinnvolle Annahmen und benenne sie kurz.

Frage nur nach, wenn ohne Klärung kein sinnvoller Vorschlag möglich ist.
