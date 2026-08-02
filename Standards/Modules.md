# Module

## Ziel

Jede fachlich zusammengehörige Funktionalität wird als eigenes Modul organisiert.

Ein Modul kapselt:

- UI
- Fachlogik
- Konfiguration
- Dependency Injection
- Modelle

Ein Modul soll möglichst unabhängig von anderen Modulen entwickelt, getestet und erweitert werden können.

---

# Standardstruktur

Ein Modul besitzt folgende Struktur:

```text
<Modulname>/
│
├── Components/
├── Configuration/
├── Models/
├── Services/
├── Templates/                 (optional)
├── Resources/                 (optional)
├── _Imports.razor             (optional)
└── ServiceCollectionExtensions.cs
```

Nicht jedes Verzeichnis ist zwingend erforderlich.

Es sollen jedoch keine Komponenten oder Services anderer Module enthalten sein.

---

# Komponenten

Alle Razor-Komponenten eines Moduls liegen innerhalb des Moduls.

Beispiel:

```text
TagebuchAuswertungen/
    Components/
        TagebuchAuswertungen.razor
        TagebuchDetails.razor
        ...
```

Dadurch bleibt die Projektstruktur nach Fachlichkeiten gegliedert.

---

# Models

Alle ausschließlich vom Modul verwendeten Modelle liegen im Unterordner

```
Models
```

Dazu gehören beispielsweise

- ViewModels
- Ergebnisobjekte
- Statusmodelle
- DTOs des Moduls

---

# Services

Alle Fachservices eines Moduls liegen unter

```
Services
```

Services enthalten ausschließlich Fachlogik.

---

# Configuration

Konfigurationsklassen liegen unter

```
Configuration
```

Jede Options-Klasse besitzt eine SectionName-Konstante.

Beispiel

```csharp
public sealed class MyModuleOptions
{
    public const string SectionName = "MyModule";
}
```

---

# ServiceCollectionExtensions

Jedes Modul besitzt genau eine Datei

```
ServiceCollectionExtensions.cs
```

Diese enthält ausschließlich die Registrierung des Moduls.

Beispiel

```csharp
builder.Services.AddMyModule(builder.Configuration);
```

Die Datei registriert

- Options
- Options-Validierung
- Services
- interne Infrastruktur

---

# Program.cs

Program.cs kennt keine internen Services eines Moduls.

Nicht:

```csharp
builder.Services.AddScoped<IMailService, MailService>();
builder.Services.AddScoped<IMyRepository, MyRepository>();
```

Sondern ausschließlich

```csharp
builder.Services.AddMyModule(builder.Configuration);
```

Dadurch bleibt Program.cs übersichtlich.

---

# Options

Options werden innerhalb des Moduls registriert.

Bevorzugt wird

```csharp
services
    .AddOptions<MyOptions>()
    .Bind(...)
    .Validate(...)
    .ValidateOnStart();
```

---

# _Imports.razor

Verwendet ein Modul viele Razor-Komponenten, kann ein eigener

```
_Imports.razor
```

verwendet werden.

Dadurch werden unnötige @using-Direktiven in den Komponenten vermieden.

---

# Ziel

Ein Modul soll

- leicht verständlich
- unabhängig
- wiederverwendbar
- testbar
- einfach registrierbar

sein.

Idealerweise genügt zur Integration eines Moduls eine einzige Zeile:

```csharp
builder.Services.AddMyModule(builder.Configuration);
```