# Security Standards

Version: 1.0

Dieses Dokument definiert die Sicherheitsstandards für alle Projekte der MyLibrary-Familie.

---

# Ziele

Sicherheit hat Vorrang vor Bequemlichkeit.

Alle Projekte sollen:

* keine Geheimnisse veröffentlichen
* sensible Daten schützen
* sichere Standardkonfigurationen verwenden
* Least-Privilege-Prinzipien beachten
* DSGVO-konforme Lösungen ermöglichen

---

# Grundsatz

Geheimnisse gehören niemals in:

* Git-Repositories
* Quellcode
* Unit Tests
* Dokumentationen
* README-Dateien

---

# Verbotene Inhalte

Folgende Daten dürfen niemals eingecheckt werden:

* Datenbank-Passwörter
* SMTP-Passwörter
* OAuth Secrets
* API Keys
* Azure Keys
* OpenAI Keys
* Zertifikate mit privaten Schlüsseln
* Produktive Connection Strings

---

# Secrets Management

Standarddatei:

```text
appsettings.Secrets.json
```

Beispiel:

```json
{
  "ConnectionStrings": {
    "MainDatabase": ""
  },
  "Smtp": {
    "User": "",
    "Password": ""
  }
}
```

---

# Git Ignore

Folgende Dateien müssen ignoriert werden:

```gitignore
appsettings.Secrets.json
*.pfx
*.snk
```

---

# Connection Strings

Nicht erlaubt:

```csharp
var connectionString =
    "Server=...;Password=...";
```

Erlaubt:

```csharp
_configuration.GetConnectionString("MainDatabase");
```

---

# Logging

Logs dürfen keine Geheimnisse enthalten.

Nicht loggen:

* Passwörter
* Tokens
* API Keys
* Connection Strings

Nicht erlaubt:

```csharp
_logger.LogInformation(
    "Password: {Password}",
    password);
```

---

# Benutzerdaten

Personenbezogene Daten dürfen nur geloggt werden, wenn dies fachlich erforderlich ist.

Besonders schützenswert:

* Passwörter
* Geburtsdaten
* Bankdaten
* Gesundheitsdaten

---

# Verschlüsselung

Für neue Projekte wird bevorzugt:

```text
TLS 1.2+
```

verwendet.

Unverschlüsselte Protokolle sind zu vermeiden.

---

# SMTP

SMTP-Verbindungen sollen TLS verwenden.

Passwörter werden ausschließlich über Konfiguration bereitgestellt.

---

# Datenbankzugriffe

Verbindungsdaten werden niemals hardcodiert.

Verwenden:

```text
appsettings.json
appsettings.Secrets.json
```

---

# SQL Injection

Alle SQL-Zugriffe werden parameterisiert.

Dapper-Parameter sind verpflichtend.

---

# NuGet Pakete

Nur vertrauenswürdige und gepflegte Pakete verwenden.

Neue Pakete müssen vor Aufnahme geprüft werden.

---

# Open Source

Vor Veröffentlichung prüfen:

* keine Secrets
* keine internen URLs
* keine Kundendaten
* keine Zugangsdaten

---

# Pull Request Checkliste

Vor jedem Merge prüfen:

* Enthält der Commit Geheimnisse?
* Enthält der Commit Zugangsdaten?
* Enthält der Commit produktive URLs?
* Enthält der Commit Kundendaten?
* Werden Secrets korrekt ausgelagert?
