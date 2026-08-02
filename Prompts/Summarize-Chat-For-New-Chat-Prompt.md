Erstelle eine vollständige Projektübergabe als Markdown-Dokument.

Die Übergabe dient als Startdokument für einen neuen Chat innerhalb desselben Projekts.

Wichtig:

- Dokumentiere ausschließlich den aktuellen Stand.
- Keine verworfenen Ideen.
- Keine Zwischenlösungen.
- Keine historischen Diskussionen.
- Keine Chat-Zusammenfassung.
- Beschreibe nur die Architektur und den aktuell gültigen Stand.

Das Dokument soll möglichst kompakt, aber vollständig sein.

Verwende folgende Gliederung:

# Projekt

- Ziel der Anwendung
- Fachlicher Überblick
- Aktueller Entwicklungsstand

# Architektur

- Solution-Struktur
- Projekte und Verantwortlichkeiten
- Schichten
- Abhängigkeiten
- verwendete MyLibrary-Standards

# Datenmodell

Für jede wesentliche Entität:

- Aufgabe
- wichtigste Eigenschaften
- Beziehungen

Beschreibe insbesondere:

- VacationRequest
- Employee
- CostCenterApprovalRule
- ApprovalAssignment
- Kommentare
- Protokoll

# Fachlogik

Beschreibe die aktuell gültigen Geschäftsregeln:

- Antrag stellen
- Genehmigung Stufe 1
- Genehmigung Stufe 2
- Ablehnung
- Stellvertretungen
- Genehmigerermittlung
- Rollenmodell
- Administratorrechte

# Services

Für jeden wichtigen Service:

- Zweck
- wichtigste Methoden
- Verantwortlichkeit

# Repositories

Beschreibe:

- AccessRepository
- VacationRequestRepository
- RuleRepository
- sonstige Repositories

inklusive Verantwortlichkeiten.

# UI

Beschreibe:

- Seiten
- Komponenten
- Navigation
- QuickGrid-Konzept
- Filtermodell
- Statusanzeige

# Technische Entscheidungen

Dokumentiere ausschließlich die aktuell gültigen Architekturentscheidungen.

Zum Beispiel:

- Genehmiger werden beim Antrag gespeichert
- Genehmigung erfolgt gegen gespeicherte Genehmiger
- Regeländerungen wirken nur auf neue Anträge
- QuickGrid statt Tabellen
- Blazor Server
- Repository-Struktur
- Dependency Injection
- keine statischen Fachservices

# Tests

Beschreibe:

- vorhandene Testprojekte
- wichtigste Testfälle
- aktueller Teststatus

# Konfiguration

Beschreibe:

- appsettings
- Benutzerumschaltung
- Entwicklungsmodus
- geplante Windows-Authentifizierung

# Bekannte Einschränkungen

Nur aktuell bestehende Probleme.

Keine bereits gelösten Probleme aufnehmen.

# Offene Aufgaben

Sortiert nach Priorität.

Kennzeichne dabei:

## Vor Release

## Nach Release

## Später

# Roadmap

Beschreibe die nächsten sinnvollen Entwicklungsschritte.

# Hinweise für den nächsten Chat

Kurze Zusammenfassung:

- Was sollte der nächste Chat unbedingt wissen?
- Welche Architekturprinzipien dürfen nicht verletzt werden?
- Welche Dateien sind für Änderungen meist relevant?

# Nicht dokumentieren

Folgende Informationen sollen bewusst NICHT aufgenommen werden:

- Git-Kommandos
- Release-Notizen
- Commit-Historie
- verworfene Lösungsansätze
- Debugging-Verläufe
- temporäre Workarounds
- Chat-Verlauf



Das Ergebnis soll als README_NEXT_CHAT.md geeignet sein und ohne weiteren Chatverlauf als alleinige Wissensbasis dienen.


