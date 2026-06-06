# Testing Standards

Version: 1.0

Dieses Dokument definiert die Teststandards für alle Projekte der MyLibrary-Familie.

---

# Ziele

Tests sollen:

* Fehler früh erkennen
* Refactorings absichern
* Regressionen vermeiden
* Architekturregeln absichern
* Dokumentation des Verhaltens liefern

---

# Grundsatz

Jede Bibliothek erhält ein eigenes Testprojekt.

Beispiel:

```text
MyLibrary.Email
MyLibrary.Email.Test
```

```text
MyLibrary.LinkListe
MyLibrary.LinkListe.Test
```

```text
MyLibrary.Workflow
MyLibrary.Workflow.Test
```

---

# Test Framework

Standard:

```text
xUnit
```

Verwendete Pakete:

```text
xunit
xunit.runner.visualstudio
Microsoft.NET.Test.Sdk
```

Optional:

```text
Moq
FluentAssertions
```

---

# Projektstruktur

```text
MyLibrary.Email.Test

├─ Services
├─ Models
├─ Validators
├─ Helpers
└─ TestData
```

Beispiel:

```text
Services
├─ EmailServiceTests.cs

Models
├─ EmailSettingsTests.cs
```

---

# Benennung von Testklassen

Schema:

```text
<ClassName>Tests
```

Beispiele:

```text
EmailServiceTests
LinkListServiceTests
CustomerRepositoryTests
```

Nicht verwenden:

```text
TestEmail
EmailTest
Tests
```

---

# Benennung von Testmethoden

Standard:

```text
MethodName_Should_ExpectedBehavior
```

Beispiele:

```csharp
SendAsync_Should_SendEmail_WhenConfigurationIsValid
```

```csharp
LoadAsync_Should_ReturnEmptyList_WhenFileDoesNotExist
```

```csharp
GetByIdAsync_Should_ReturnCustomer_WhenCustomerExists
```

---

# Testaufbau

Schema:

```text
Arrange
Act
Assert
```

Beispiel:

```csharp
[Fact]
public async Task LoadAsync_Should_ReturnLinks()
{
    // Arrange

    // Act

    // Assert
}
```

---

# Was muss getestet werden?

## Services

Geschäftslogik wird getestet.

Beispiele:

* Berechnungen
* Validierungen
* Konvertierungen
* Mapping
* Fehlerbehandlung

---

## Models

Modelklassen werden getestet, wenn sie Logik enthalten.

Beispiel:

```csharp
public string EffectiveIcon
```

---

## Validatoren

Alle Validatoren müssen getestet werden.

Beispiele:

```text
EmailValidator
CustomerValidator
```

---

## Repositories

Repository-Logik wird getestet.

Insbesondere:

* SQL-Aufbau
* Mapping
* Fehlerbehandlung

---

# Was wird nicht getestet?

Nicht priorisiert:

* Razor-Markup
* CSS
* Layouts
* Bootstrap-Klassen

Diese werden manuell geprüft.

---

# Mocking

Externe Abhängigkeiten werden gemockt.

Beispiele:

```text
Repositorys
HttpClient
SMTP
Dateisystem
```

---

# Interfaces verwenden

Beispiel:

```csharp
IEmailRepository
```

statt:

```csharp
EmailRepository
```

direkt zu instanziieren.

---

# FluentAssertions

Empfohlen:

```csharp
result.Should().NotBeNull();
```

```csharp
result.Count.Should().Be(5);
```

statt:

```csharp
Assert.NotNull(result);
Assert.Equal(5, result.Count);
```

---

# Testdaten

Testdaten werden zentral abgelegt.

Ordner:

```text
TestData
```

Beispiele:

```text
helpdesk-links.json
customers.json
workflow.json
```

---

# Keine produktiven Daten

Nicht verwenden:

* Produktive Datenbanken
* Produktive SMTP-Server
* Produktive APIs

Tests müssen unabhängig ausführbar sein.

---

# Datenbanktests

Repositorys werden bevorzugt gegen Testdatenbanken getestet.

Alternativ:

* Mock-Repositories
* In-Memory-Datenbanken

---

# HTTP-Tests

HTTP-Zugriffe werden nicht gegen echte Systeme getestet.

Verwenden:

```text
MockHttpMessageHandler
```

oder entsprechende Test-Doubles.

---

# Exception Tests

Fehlerfälle müssen getestet werden.

Beispiel:

```csharp
[Fact]
public async Task SendAsync_Should_ThrowException_WhenConfigurationMissing()
{
}
```

---

# Randfälle

Zu testen:

* Null-Werte
* Leere Listen
* Leere Strings
* Ungültige Konfigurationen
* Fehlende Dateien
* Zeitüberschreitungen

---

# Coverage

Es wird keine starre Coverage-Vorgabe definiert.

Erwartung:

* Kritische Businesslogik: sehr hohe Testabdeckung
* Infrastruktur: angemessene Testabdeckung
* DTOs ohne Logik: keine Tests erforderlich

---

# Logging testen

Logging wird normalerweise nicht direkt getestet.

Ausnahme:

Wenn Logging Teil der Fachlichkeit ist.

---

# Testbarkeit als Architekturziel

Neue Komponenten werden so entwickelt, dass sie testbar sind.

Vermeiden:

```csharp
new SqlConnection(...)
```

innerhalb der Geschäftslogik.

Bevorzugen:

```csharp
IDbConnectionFactory
```

---

# Continuous Integration

Jeder Pull Request sollte folgende Schritte erfolgreich durchlaufen:

```bash
dotnet restore
dotnet build
dotnet test
```

---

# Review-Checkliste

Vor jedem Commit prüfen:

* Existieren Tests für neue Businesslogik?
* Sind Fehlerfälle getestet?
* Sind Randfälle getestet?
* Werden Abhängigkeiten gemockt?
* Sind Tests unabhängig ausführbar?
* Sind Testnamen aussagekräftig?
* Ist Arrange / Act / Assert eingehalten?
* Werden keine produktiven Systeme verwendet?
* Sind die Tests verständlich lesbar?
