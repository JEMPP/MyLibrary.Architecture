# Razor Class Library Standard

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
├── README.md
├── LICENSE
└── MyLibrary.<Name>.sln
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
