# Web API Template

Version: 1.0

Dieses Dokument beschreibt die Standardvorlage für ASP.NET Core Web APIs der MyLibrary-Familie.

---

# Ziel

Web APIs werden verwendet für:

* Integrationen
* REST-Schnittstellen
* Backend Services
* Mobile Anwendungen
* Blazor Anwendungen
* Externe Systeme
* Workflow APIs

---

# Projekttyp

Visual Studio:

```text
ASP.NET Core Web API
```

Projektname:

```text
MyLibrary.<Name>.Api
```

Beispiele:

```text
MyLibrary.Email.Api
MyLibrary.Workflow.Api
MyLibrary.Reporting.Api
MyLibrary.Customer.Api
```

---

# Solution Struktur

```text
MyLibrary.<Name>.Api.sln

├─ MyLibrary.<Name>
├─ MyLibrary.<Name>.Api
└─ MyLibrary.<Name>.Api.Test
```

---

# Architektur

Die API enthält möglichst wenig Businesslogik.

Erlaubt:

```text
Controller
↓
Service
↓
Repository
↓
Datenbank
```

Nicht erlaubt:

```text
Controller
↓
SQL
```

---

# Projektstruktur

```text
MyLibrary.<Name>.Api

├─ Controllers
├─ Contracts
├─ Configuration
├─ Middleware
├─ Filters
├─ Extensions
└─ Program.cs
```

Optional:

```text
Authentication
Authorization
Swagger
```

---

# Controller

Controller enthalten ausschließlich:

* Routing
* Request Mapping
* Response Mapping
* Validierung
* Aufruf von Services

Keine Businesslogik.

---

# Controller Benennung

Schema:

```text
<Name>Controller
```

Beispiele:

```text
EmailController
WorkflowController
CustomerController
```

---

# Routing

Standard:

```csharp
[ApiController]
[Route("api/[controller]")]
```

Beispiel:

```csharp
[ApiController]
[Route("api/[controller]")]
public class CustomerController : ControllerBase
{
}
```

---

# Contracts

DTOs werden im Ordner

```text
Contracts
```

abgelegt.

Beispiele:

```text
CustomerDto
CreateCustomerRequest
CreateCustomerResponse
```

---

# Businesslogik

Businesslogik gehört in:

```text
MyLibrary.<Name>
```

nicht in die API.

Die API verwendet Bibliotheken.

Beispiel:

```csharp
private readonly ICustomerService _customerService;
```

---

# Dependency Injection

Registrierung über:

```csharp
builder.Services.AddMyLibraryCustomer();
```

---

# Program.cs

Program.cs enthält ausschließlich:

* Service Registrierung
* Middleware Registrierung
* Swagger
* Authentifizierung
* Logging

Keine Businesslogik.

---

# Logging

Standard:

```text
Serilog
```

Program.cs:

```csharp
builder.Host.UseSerilog();
```

Im Code:

```csharp
ILogger<T>
```

---

# Konfiguration

Dateien:

```text
appsettings.json
appsettings.Development.json
appsettings.Secrets.json
```

---

# Secrets

Geheimnisse gehören ausschließlich in:

```text
appsettings.Secrets.json
```

Diese Datei wird nicht versioniert.

---

# Authentifizierung

## Standard

Für interne Anwendungen wird bevorzugt Windows Authentication verwendet.

Begründung:

* Integration mit On-Premises Active Directory
* Single Sign-On (SSO)
* keine zusätzliche Anmeldung für Benutzer
* Arbeiten im Benutzerkontext
* gute Integration in interne Windows- und Intranet-Umgebungen

---

## Ziel

Benutzer sollen sich nicht erneut anmelden müssen.

Die Anwendung soll den aktuellen Windows-/Domänenbenutzer verwenden.

Beispiel:

```
User.Identity?.Name
```

Typisches Ergebnis:

```
DOMAIN\username
```

---

## Windows Authentication

Windows Authentication ist bevorzugt für:

* interne Web APIs
* Blazor Server Anwendungen
* Intranet-Anwendungen
* interne Admin-Tools
* interne Reporting-Systeme

---

## Program.cs Beispiel

```csharp
builder.Services.AddAuthentication(
    Microsoft.AspNetCore.Server.IISIntegration.IISDefaults.AuthenticationScheme);

builder.Services.AddAuthorization();

var app = builder.Build();

app.UseAuthentication();
app.UseAuthorization();
```

Controller:

```csharp
[Authorize]
[ApiController]
[Route("api/[controller]")]
public class CustomerController : ControllerBase
{
}
```

---

## IIS / Hosting

Bei Hosting unter IIS muss Windows Authentication aktiviert werden.

Anonymous Authentication soll für geschützte Anwendungen deaktiviert werden.

```text
Windows Authentication: Enabled
Anonymous Authentication: Disabled
```

---

## Benutzerkontext

Der angemeldete Benutzer wird bevorzugt über einen eigenen Service abstrahiert.

Beispiel:

```csharp
ICurrentUserService
CurrentUserService
```

Beispielzugriff:

```csharp
var userName = _currentUserService.UserName;
```

Nicht empfohlen:

```csharp
HttpContext.User.Identity.Name
```

direkt überall im Code zu verwenden.

---

## Migration zu Entra ID

Da mittelfristig eine Umstellung auf Microsoft Entra ID geplant ist, muss die Authentifizierung austauschbar aufgebaut werden.

Die Anwendung darf nicht fest an Windows Authentication gekoppelt werden.

Deshalb gilt:

* Authentifizierung wird über Standards von ASP.NET Core eingebunden
* Benutzerinformationen werden über `ICurrentUserService` abstrahiert
* Rollen und Claims werden nicht hart im Code verteilt
* Autorisierung erfolgt über Policies
* Neue APIs sollen so aufgebaut sein, dass später Entra ID / OpenID Connect ergänzt werden kann

---

## Entra ID Vorbereitung

Für zukünftige Entra-ID-Unterstützung sollen Claims berücksichtigt werden.

Beispiele:

```text
name
preferred_username
upn
email
groups
roles
```

Die Anwendung soll intern nicht davon ausgehen, dass Benutzer immer im Format

```text
DOMAIN\username
```

vorliegen.

---

## Autorisierung

Autorisierung erfolgt bevorzugt über Policies.

Beispiel:

```csharp
builder.Services.AddAuthorization(options =>
{
    options.AddPolicy("CanViewReports", policy =>
        policy.RequireRole("ReportsUser"));
});
```

Controller:

```csharp
[Authorize(Policy = "CanViewReports")]
```

---

## Nicht erlaubt

Nicht empfohlen:

```csharp
if (User.Identity.Name == "DOMAIN\\user")
{
}
```

Besser:

```csharp
[Authorize(Policy = "CanViewReports")]
```

oder Prüfung über einen fachlichen Berechtigungsservice.

---

## Alternative Authentifizierung

Für externe APIs oder cloudbasierte Szenarien kann verwendet werden:

* Microsoft Entra ID
* OpenID Connect
* OAuth2
* JWT Bearer

Diese Verfahren sind nicht Standard für interne On-Premises-Anwendungen, sollen aber architektonisch vorbereitet werden.

---

# Swagger

Swagger ist standardmäßig aktiviert.

Pakete:

```text
Swashbuckle.AspNetCore
```

Program.cs:

```csharp
builder.Services.AddEndpointsApiExplorer();

builder.Services.AddSwaggerGen();
```

---

# Versionierung

Neue APIs sollen API-Versionierung unterstützen.

Beispiel:

```text
/api/v1/customer
/api/v2/customer
```

---

# Fehlerbehandlung

Globale Fehlerbehandlung über Middleware.

Beispiel:

```text
ExceptionHandlingMiddleware
```

Nicht erlaubt:

```csharp
try/catch
```

in jedem Controller.

---

# Standard HTTP Codes

Erfolgreich:

```text
200 OK
201 Created
204 No Content
```

Fehler:

```text
400 Bad Request
401 Unauthorized
403 Forbidden
404 Not Found
500 Internal Server Error
```

---

# Datenbankzugriffe

Datenbankzugriffe erfolgen ausschließlich über:

```text
Repository
```

Die Regeln aus:

```text
Database-Standards.md
```

gelten vollständig.

---

# Asynchronität

Controller verwenden ausschließlich Async-Methoden.

Beispiel:

```csharp
public async Task<ActionResult<CustomerDto>>
```

Nicht erlaubt:

```csharp
public ActionResult<CustomerDto>
```

für Datenbank- oder HTTP-Zugriffe.

---

# DTOs

Responses verwenden DTOs.

Nicht direkt zurückgeben:

```csharp
CustomerEntity
```

Bevorzugt:

```csharp
CustomerDto
```

---

# Validierung

Validierung erfolgt:

* Model Validation
* FluentValidation (optional)

Beispiel:

```csharp
[Required]
public string Name { get; set; }
```

---

# CORS

CORS wird explizit konfiguriert.

Keine Wildcard-Konfiguration in produktiven Systemen.

Nicht empfohlen:

```csharp
AllowAnyOrigin()
```

---

# Health Checks

Health Checks werden empfohlen.

Pakete:

```text
Microsoft.Extensions.Diagnostics.HealthChecks
```

Endpoint:

```text
/health
```

---

# Monitoring

Optional:

```text
Serilog
Seq
Application Insights
```

---

# Tests

Projekt:

```text
MyLibrary.<Name>.Api.Test
```

Framework:

```text
xUnit
```

Zu testen:

* Services
* Validatoren
* Middleware
* Mapping

Nicht primär:

* Swagger
* Routing Details

---

# Standardpakete

```text
Microsoft.AspNetCore.OpenApi
Swashbuckle.AspNetCore
Serilog.AspNetCore
```

Optional:

```text
FluentValidation.AspNetCore
```

---

# README

README enthält:

* Beschreibung
* Installation
* Konfiguration
* Authentifizierung
* Swagger URL
* Beispiel Requests
* Beispiel Responses
* Tests

---

# Beispiel Solution

```text
MyLibrary.Customer.Api.sln

├─ MyLibrary.Customer
├─ MyLibrary.Customer.Api
└─ MyLibrary.Customer.Api.Test
```

---

# Review Checkliste

Vor dem ersten Release prüfen:

* Enthält Program.cs keine Businesslogik?
* Liegt Businesslogik in Services?
* Sind Controller schlank?
* Wird Serilog verwendet?
* Ist Swagger aktiviert?
* Sind Secrets ausgelagert?
* Wird Authentifizierung unterstützt?
* Werden DTOs verwendet?
* Sind Health Checks vorhanden?
* Existiert ein README?
* Existieren Tests?
* Wird ausschließlich async gearbeitet?
