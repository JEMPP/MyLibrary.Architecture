# Requirements

## Projekt

Name:

```text
MyLibrary.Workflow
```

---

# Kurzbeschreibung

Bibliothek zur Definition und Ausführung konfigurierbarer Geschäftsprozesse.

Workflows sollen ohne Neukompilierung erweitert und angepasst werden können.

---

# Ziel

Bereitstellung einer zentralen Workflow-Engine für interne Anwendungen.

Geschäftsprozesse sollen konfigurierbar und wiederverwendbar sein.

---

# Anwender

* Fachabteilungen
* Entwickler
* Blazor Anwendungen
* Worker Services
* Web APIs

---

# Anwendungsfälle

* Freigabeprozesse
* Ticketprozesse
* Genehmigungsworkflows
* Importprozesse
* Benachrichtigungsprozesse

---

# Nicht-Ziele

Nicht Bestandteil:

* BPMN Designer
* Low-Code Plattform
* Vollständige Process Mining Lösung

---

# Funktionale Anforderungen

* Workflow Definitionen laden
* Workflows starten
* Workflows pausieren
* Workflows fortsetzen
* Workflow Status abfragen
* Workflow Historie speichern
* Benutzeraufgaben unterstützen
* Automatische Schritte unterstützen

---

# Nichtfunktionale Anforderungen

* Erweiterbarkeit
* Wiederverwendbarkeit
* Hohe Testbarkeit
* Konfigurierbarkeit
* Logging
* Skalierbarkeit

---

# Schnittstellen

* SQL Server
* REST APIs
* E-Mail Benachrichtigungen
* Active Directory / Entra ID

---

# Datenhaltung

Speicherung von:

* Workflow Definitionen
* Workflow Instanzen
* Workflow Historie

Datenbank:

```text
SQL Server
```

---

# Konfiguration

Konfigurierbar:

* Workflow Definitionen
* Timeouts
* Retry Regeln
* Benachrichtigungen

---

# Sicherheit

* Windows Authentication bevorzugt
* Vorbereitung auf Entra ID
* Benutzerkontext berücksichtigen
* Rollenbasierte Freigaben unterstützen

---

# Logging

Zu protokollieren:

* Workflow gestartet
* Workflow beendet
* Fehler
* Statuswechsel

---

# Deployment

* Klassenbibliothek
* Verwendung in Blazor Server
* Verwendung in Worker Services
* Verwendung in Web APIs

---

# Akzeptanzkriterien

* Workflow Definitionen können geladen werden
* Workflow Instanzen können gestartet werden
* Workflow Historie wird gespeichert
* Unit Tests vorhanden
* Dokumentation vorhanden

---

# Offene Fragen

* JSON oder Datenbank für Definitionen?
* Versionierung von Workflows?
* Visual Designer?
* Mehrmandantenfähigkeit?
