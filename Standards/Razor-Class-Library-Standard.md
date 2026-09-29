# Razor Class Library Standard

Für neue .NET-Repositories gilt verbindlich der
[.NET Repository Standard](../Standards/DotNet-Repository-Standard.md):
eine `.slnx` im Repository-Root, jedes Produktiv- und Testprojekt in einem eigenen
gleichnamigen Unterordner mit seiner `.csproj`, Repository-Dokumentation im Root.
Historische `.sln`-Dateien müssen nicht allein deshalb migriert
werden; für neue Solutions keine parallele `.sln` anlegen.


## Ziel

Wiederverwendbare Blazor-Komponenten werden in einer eigenen Razor Class Library (RCL) bereitgestellt.

## Standardstruktur

```text
MyLibrary.<Name>
│
├── MyLibrary.<Name>
├── MyLibrary.<Name>.Razor
├── MyLibrary.<Name>.Tests
│
├── .gitignore
├── README.md
├── CHANGELOG.md
├── LICENSE
└── MyLibrary.<Name>.slnx
```

## Verantwortlichkeiten

### `MyLibrary.<Name>`

* Fachlogik
* Services
* Models
* Options
* Abstraktionen

Keine UI-Komponenten.

### `MyLibrary.<Name>.Razor`

* Razor Components
* Blazor UI
* Formularseiten
* Dialoge
* Wiederverwendbare Oberflächen

Keine Fachlogik.

### `MyLibrary.<Name>.Tests`

* Unit Tests
* Integration Tests

## Routing

Razor-Komponenten mit `@page` müssen im Host registriert werden.

### `Routes.razor`

```razor
<Router
    AppAssembly="typeof(Program).Assembly"
    AdditionalAssemblies="new[]
    {
        typeof(MyLibrary.<Name>.Razor.SomeComponent).Assembly
    }">
```

### `Program.cs`

```csharp
app.MapRazorComponents<App>()
    .AddInteractiveServerRenderMode()
    .AddAdditionalAssemblies(
        typeof(MyLibrary.<Name>.Razor.SomeComponent).Assembly);
```

Beide Registrierungen sind erforderlich.
