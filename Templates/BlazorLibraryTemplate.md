# Blazor Library Template

Version: 1.0

Dieses Dokument beschreibt die Standardvorlage für wiederverwendbare Blazor-Komponentenbibliotheken der MyLibrary-Familie.

---

# Ziel

Eine Blazor-Bibliothek soll:

* wiederverwendbare Komponenten bereitstellen
* unabhängig von Anwendungen sein
* testbar sein
* konfigurierbar sein
* GitHub-Ready sein
* NuGet-Ready sein

---

# Projekttyp

Visual Studio:

```text
Razor Class Library
```

Projektname:

```text
MyLibrary.<Name>
```

Beispiele:

```text
MyLibrary.LinkListe
MyLibrary.WorkflowDesigner
MyLibrary.Reporting.Components
```

---

# Solution Struktur

```text
MyLibrary.<Name>.sln

├─ MyLibrary.<Name>
└─ MyLibrary.<Name>.Test
```

---

# Bibliotheksstruktur

```text
MyLibrary.<Name>

├─ Components
├─ Models
├─ Interfaces
├─ Services
├─ Extensions
├─ Configuration
├─ Exceptions
│
├─ wwwroot
│
└─ _Imports.razor
```

---

# Components

Jede Komponente besitzt:

```text
ComponentName.razor
```

Optional:

```text
ComponentName.razor.cs
```

Beispiele:

```text
LinkList.razor
WorkflowViewer.razor
ReportViewer.razor
```

---

# Code Behind

Bei umfangreicher Logik wird Code-Behind bevorzugt.

Beispiel:

```text
LinkList.razor
LinkList.razor.cs
```

Dadurch bleibt das Razor-Markup übersichtlich.

---

# Komponentenparameter

Alle Konfiguration erfolgt über Parameter.

Beispiel:

```razor
<LinkList JsonPath="helpdesk-links.json" />
```

---

# Nicht erlaubt

Projektspezifische Konfiguration:

```razor
<LinkList HelpdeskMode="true" />
```

```csharp
if(projectName == "Intermetric")
{
}
```

---

# Dependency Injection

Services werden über DI bereitgestellt.

Beispiel:

```csharp
builder.Services.AddMyLibraryLinkListe();
```

---

# Service Registrierung

Datei:

```text
Extensions
└─ ServiceCollectionExtensions.cs
```

Beispiel:

```csharp
public static IServiceCollection AddMyLibraryLinkListe(
    this IServiceCollection services)
{
    services.AddScoped<ILinkListService, LinkListService>();

    return services;
}
```

---

# Services

Geschäftslogik gehört in Services.

Beispiele:

```text
LinkListService
WorkflowService
ReportService
```

Nicht in:

```text
.razor Dateien
```

---

# Models

Modelklassen enthalten Datenstrukturen.

Beispiele:

```csharp
LinkItem
LinkCategory
WorkflowDefinition
```

---

# JSON Konfiguration

Komponenten werden bevorzugt über JSON-Dateien konfiguriert.

Beispiele:

```text
helpdesk-links.json
workflow-definitions.json
reports.json
```

Die JSON-Dateien liegen in der Host-Anwendung.

Nicht in der Bibliothek.

---

# HttpClient

Die Bibliothek registriert keinen eigenen HttpClient.

Der Host stellt den HttpClient bereit.

Beispiel:

```csharp
builder.Services.AddScoped(sp =>
{
    var navigationManager =
        sp.GetRequiredService<NavigationManager>();

    return new HttpClient
    {
        BaseAddress =
            new Uri(navigationManager.BaseUri)
    };
});
```

---

# Styling

Bootstrap wird bevorzugt.

Bootstrap Icons werden unterstützt.

Beispiel:

```html
<link rel="stylesheet"
      href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.min.css">
```

---

# Standard Icon Strategie

Komponenten sollen sinnvolle Defaults besitzen.

Beispiel:

```csharp
public string EffectiveIcon =>
    string.IsNullOrWhiteSpace(Icon)
        ? "bi-link-45deg"
        : Icon;
```

---

# wwwroot

Statische Ressourcen der Bibliothek werden unter

```text
wwwroot
```

abgelegt.

Beispiele:

```text
css
js
images
```

---

# JavaScript

JavaScript wird nur verwendet wenn Blazor alleine nicht ausreicht.

Bevorzugt:

```text
C#
Blazor
```

vor

```text
JavaScript
```

---

# Logging

Verwendet wird:

```csharp
ILogger<T>
```

Die Bibliothek konfiguriert Serilog nicht selbst.

---

# Testprojekt

```text
MyLibrary.<Name>.Test
```

Framework:

```text
xUnit
```

---

# Testbare Bestandteile

Zu testen:

* Services
* Models
* Validatoren

Nicht priorisiert:

* Razor-Markup
* CSS
* Bootstrap Layout

---

# README

Jede Bibliothek enthält:

```text
README.md
```

mit:

* Beschreibung
* Installation
* Dependency Injection
* Beispielcode
* Konfiguration

---

# NuGet Readiness

Die Bibliothek soll so aufgebaut sein, dass sie später als NuGet-Paket veröffentlicht werden kann.

Nicht erlaubt:

* Projektspezifische URLs
* Projektspezifische Kundennamen
* Projektspezifische Datenbankzugriffe

---

# Beispiel

Projekt:

```text
MyLibrary.LinkListe
```

Verwendung:

```razor
<LinkList JsonPath="helpdesk-links.json" />
```

JSON:

```json
[
  {
    "Category": "Tickets",
    "Order": 1,
    "Links": [
      {
        "Text": "Neues Ticket",
        "Url": "https://..."
      }
    ]
  }
]
```

---

# Erstellung einer neuen Blazor Bibliothek

1. Razor Class Library anlegen
2. xUnit Testprojekt anlegen
3. Projektreferenz setzen
4. Components Ordner anlegen
5. Models anlegen
6. Services anlegen
7. DI Extension anlegen
8. README erstellen
9. Tests erstellen
10. GitHub Repository anlegen

---

# Review Checkliste

Vor dem ersten Release prüfen:

* Ist die Komponente wiederverwendbar?
* Gibt es projektspezifische Namen?
* Ist die Konfiguration ausgelagert?
* Ist die Logik in Services?
* Existieren Tests?
* Existiert eine README?
* Ist die Bibliothek NuGet-fähig?
