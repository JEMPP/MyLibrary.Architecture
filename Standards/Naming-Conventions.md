# Naming Conventions

Version: 1.0

Dieses Dokument definiert die Namenskonventionen für alle Projekte der MyLibrary-Familie.

---

# Ziele

Einheitliche Namen sorgen für:

* bessere Lesbarkeit
* bessere Wartbarkeit
* schnellere Orientierung
* konsistente Projektstrukturen
* einfachere Wiederverwendung
* bessere Auffindbarkeit in Visual Studio und GitHub

---

# Grundregel

Namen müssen fachlich aussagekräftig sein.

Nicht verwenden:

```text
Helper
Utils
Manager
Stuff
Common
Misc
```

Bevorzugt:

```text
EmailService
CustomerRepository
LinkListOptions
WorkflowValidator
```

---

# Projekt- und Solution-Namen

## Bibliotheken

Schema:

```text
MyLibrary.<Name>
```

Beispiele:

```text
MyLibrary.Email
MyLibrary.LinkListe
MyLibrary.Workflow
MyLibrary.Reporting
MyLibrary.Excel
```

## Testprojekte

Schema:

```text
MyLibrary.<Name>.Test
```

Beispiele:

```text
MyLibrary.Email.Test
MyLibrary.LinkListe.Test
MyLibrary.Workflow.Test
```

## Solution

Schema:

```text
MyLibrary.<Name>.sln
```

Beispiel:

```text
MyLibrary.Email.sln
```

---

# Namespaces

Namespaces folgen der Projektstruktur.

Beispiele:

```csharp
namespace MyLibrary.Email.Services;
namespace MyLibrary.Email.Models;
namespace MyLibrary.Email.Interfaces;
namespace MyLibrary.Email.Extensions;
namespace MyLibrary.Email.Configuration;
namespace MyLibrary.Email.Exceptions;
```

Für Testprojekte:

```csharp
namespace MyLibrary.Email.Test.Services;
namespace MyLibrary.Email.Test.Models;
```

---

# Ordnernamen

Standardordner:

```text
Models
Interfaces
Services
Extensions
Configuration
Exceptions
Components
Repositories
Infrastructure
Validators
Helpers
TestData
```

Ordnernamen sind im Plural.

Ausnahme:

```text
Configuration
Infrastructure
```

---

# Interfaces

Interfaces beginnen mit `I`.

Schema:

```text
I<Name>
```

Beispiele:

```csharp
IEmailService
ILinkListService
ICustomerRepository
IDbConnectionFactory
```

Nicht verwenden:

```csharp
EmailServiceInterface
InterfaceEmailService
```

---

# Services

Services enden mit `Service`.

Beispiele:

```csharp
EmailService
LinkListService
WorkflowService
ReportService
```

Passendes Interface:

```csharp
IEmailService
ILinkListService
IWorkflowService
IReportService
```

---

# Repositories

Repositories enden mit `Repository`.

Beispiele:

```csharp
CustomerRepository
EmailTemplateRepository
WorkflowRepository
```

Passendes Interface:

```csharp
ICustomerRepository
IEmailTemplateRepository
IWorkflowRepository
```

---

# Factories

Factories enden mit `Factory`.

Beispiele:

```csharp
DbConnectionFactory
SqlConnectionFactory
FirebirdConnectionFactory
AccessConnectionFactory
EmailMessageFactory
```

Passendes Interface:

```csharp
IDbConnectionFactory
IEmailMessageFactory
```

---

# Options / Configuration

Konfigurationsklassen enden mit `Options`.

Beispiele:

```csharp
EmailOptions
SmtpOptions
DatabaseOptions
LinkListOptions
```

Nicht bevorzugt:

```csharp
EmailSettings
Config
ConfigurationData
```

Hinweis:

Wenn externe JSON-Dateien bereits etablierte Begriffe wie `Settings` verwenden, dürfen diese beibehalten werden. Für neue Bibliotheken wird `Options` bevorzugt.

---

# Models

Models haben fachliche Namen.

Beispiele:

```csharp
EmailMessage
LinkItem
LinkCategory
Customer
Invoice
WorkflowDefinition
```

Nicht verwenden:

```csharp
Data
Item
Object
Result
```

außer mit fachlichem Kontext:

```csharp
ValidationResult
EmailResult
ImportResult
```

---

# DTOs

DTOs enden mit `Dto`.

Beispiele:

```csharp
CustomerDto
EmailMessageDto
WorkflowDto
```

DTOs werden nur verwendet, wenn eine klare Abgrenzung zu Domain Models notwendig ist.

---

# Results

Result-Klassen enden mit `Result`.

Beispiele:

```csharp
EmailSendResult
ValidationResult
ImportResult
ExportResult
```

---

# Requests und Responses

Für API- oder Service-Aufrufe:

```csharp
SendEmailRequest
SendEmailResponse
CreateCustomerRequest
CreateCustomerResponse
```

---

# Exceptions

Eigene Exceptions enden mit `Exception`.

Beispiele:

```csharp
EmailConfigurationException
DatabaseConnectionException
InvalidWorkflowDefinitionException
```

---

# Validatoren

Validatoren enden mit `Validator`.

Beispiele:

```csharp
EmailOptionsValidator
WorkflowDefinitionValidator
CustomerValidator
```

---

# Extension-Klassen

Extension-Klassen enden mit `Extensions`.

Beispiele:

```csharp
ServiceCollectionExtensions
StringExtensions
DateTimeExtensions
```

Die Dependency-Injection-Registrierung liegt immer in:

```text
Extensions/ServiceCollectionExtensions.cs
```

---

# Dependency-Injection-Methoden

Schema:

```csharp
AddMyLibrary<Name>()
```

Beispiele:

```csharp
AddMyLibraryEmail()
AddMyLibraryWorkflow()
AddMyLibraryReporting()
```

Bei kurzen, etablierten Namen ist auch erlaubt:

```csharp
AddLinkListe()
```

---

# Methoden

Methoden verwenden PascalCase.

Beispiele:

```csharp
SendAsync()
LoadAsync()
GetByIdAsync()
CreateConnection()
Validate()
```

Asynchrone Methoden enden mit `Async`.

Nicht erlaubt:

```csharp
send_email()
loadData()
GetByIdAsyncInternal()
```

---

# Variablen und Felder

Lokale Variablen verwenden camelCase.

Beispiele:

```csharp
emailMessage
connectionString
customerId
```

Private Felder verwenden `_camelCase`.

Beispiele:

```csharp
private readonly IEmailService _emailService;
private readonly ILogger<EmailService> _logger;
```

---

# Konstanten

Konstanten verwenden PascalCase.

Beispiel:

```csharp
public const string DefaultIcon = "bi-link-45deg";
```

---

# Properties

Properties verwenden PascalCase.

Beispiele:

```csharp
public string EmailAddress { get; set; } = "";
public int Order { get; set; }
public string EffectiveIcon { get; }
```

---

# Razor-Komponenten

Komponenten verwenden PascalCase.

Beispiele:

```text
LinkList.razor
EmailEditor.razor
WorkflowViewer.razor
```

Parameter verwenden PascalCase:

```razor
<LinkList JsonPath="helpdesk-links.json" />
```

Nicht verwenden:

```razor
<LinkList json-path="..." />
```

---

# JSON-Dateien

JSON-Dateien verwenden kebab-case.

Beispiele:

```text
helpdesk-links.json
email-settings.json
workflow-definitions.json
report-config.json
```

Nicht verwenden:

```text
HelpdeskLinks.json
emailSettings.json
WorkflowDefinitions.json
```

---

# appsettings

Standarddateien:

```text
appsettings.json
appsettings.Development.json
appsettings.Secrets.json
```

`appsettings.Secrets.json` wird niemals eingecheckt.

---

# SQL-Dateien

SQL-Dateien verwenden PascalCase oder fachliche Namen.

Beispiele:

```text
GetCustomerById.sql
SearchCustomers.sql
UpdateInvoiceStatus.sql
```

Ablage:

```text
Sql/Customer/GetCustomerById.sql
Sql/Invoice/UpdateInvoiceStatus.sql
```

---

# Testklassen

Testklassen enden mit `Tests`.

Beispiele:

```csharp
EmailServiceTests
LinkListServiceTests
CustomerRepositoryTests
```

---

# Testmethoden

Schema:

```text
MethodName_Should_ExpectedBehavior
```

Beispiele:

```csharp
SendAsync_Should_SendEmail_WhenConfigurationIsValid
LoadAsync_Should_ReturnEmptyList_WhenJsonPathIsEmpty
Validate_Should_ReturnError_WhenEmailAddressIsInvalid
```

---

# Git Branches

Standardbranch:

```text
main
```

Branch-Namen:

```text
feature/add-email-service
bugfix/fix-link-ordering
hotfix/fix-smtp-timeout
```

Nicht verwenden:

```text
master
FeatureEmail
BugFix1
```

---

# Commit Messages

Commit Messages sind kurz, fachlich und im Imperativ oder als Beschreibung formuliert.

Beispiele:

```text
Add email service
Add link list component
Fix sorting of link categories
Update database standards
```

Nicht verwenden:

```text
changes
update
fix
misc
```

---

# Review-Checkliste

Vor jedem Commit prüfen:

* Entspricht der Projektname dem Schema?
* Entspricht der Namespace dem Ordner?
* Beginnen Interfaces mit `I`?
* Enden Services mit `Service`?
* Enden Repositories mit `Repository`?
* Enden Optionen mit `Options`?
* Enden Exceptions mit `Exception`?
* Enden Tests mit `Tests`?
* Sind JSON-Dateien in kebab-case?
* Sind Namen fachlich aussagekräftig?
