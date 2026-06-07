# Requirements

## Projekt

Name:

```text
MyLibrary.Email
```

---

# Kurzbeschreibung

Wiederverwendbare Bibliothek zum Versand von E-Mails aus .NET-Anwendungen.

Die Bibliothek soll von Blazor-Anwendungen, Worker Services, Web APIs und Konsolenanwendungen verwendet werden können.

---

# Ziel

Zentralisierung des E-Mail-Versands innerhalb der MyLibrary-Familie.

Vermeidung mehrfach implementierter SMTP- und Graph-Logik.

---

# Anwender

* Entwickler
* Blazor Anwendungen
* Worker Services
* Web APIs
* Konsolenanwendungen

---

# Anwendungsfälle

* Versand einfacher E-Mails
* Versand von HTML-E-Mails
* Versand mit Anhängen
* Versand an mehrere Empfänger
* Versand über SMTP
* Versand über Microsoft Graph

---

# Nicht-Ziele

Nicht Bestandteil der Bibliothek:

* Newsletter-System
* Massenversand
* Marketing-Automation
* E-Mail-Archivierung

---

# Funktionale Anforderungen

* E-Mails versenden
* HTML-Mails unterstützen
* Anhänge unterstützen
* CC unterstützen
* BCC unterstützen
* Mehrere Empfänger unterstützen
* SMTP unterstützen
* Microsoft Graph unterstützen
* Konfigurierbare Absenderadresse

---

# Nichtfunktionale Anforderungen

* Hohe Wiederverwendbarkeit
* Testbarkeit
* Erweiterbarkeit
* Logging
* Asynchrone Verarbeitung
* Dependency Injection

---

# Schnittstellen

* SMTP Server
* Microsoft Graph API

---

# Datenhaltung

Keine dauerhafte Speicherung.

Optional:

* Temporäre Templates
* Temporäre Anhänge

---

# Konfiguration

Konfigurierbar:

* SMTP Host
* SMTP Port
* Benutzername
* Passwort
* Absenderadresse
* Graph Tenant
* Graph Client Id

---

# Sicherheit

* Zugangsdaten niemals im Repository
* appsettings.Secrets.json verwenden
* Vorbereitung auf Entra ID

---

# Logging

Zu protokollieren:

* Versand gestartet
* Versand erfolgreich
* Versand fehlgeschlagen

Keine Protokollierung von:

* Passwörtern
* Mailinhalten

---

# Deployment

* Klassenbibliothek
* NuGet-fähig

---

# Akzeptanzkriterien

* SMTP Versand funktioniert
* Graph Versand funktioniert
* Unit Tests vorhanden
* DI Integration vorhanden
* Dokumentation vorhanden

---

# Offene Fragen

* Mail Templates?
* Queue-Verarbeitung?
* Retry Mechanismus?
