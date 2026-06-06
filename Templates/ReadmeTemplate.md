# MyLibrary.<Name>

Kurzbeschreibung der Bibliothek.

## Ziel

Beschreibe in wenigen Sätzen den Zweck der Bibliothek.

Beispiel:

Diese Bibliothek stellt Funktionen zum Versand von E-Mails bereit.

---

## Features

* Feature 1
* Feature 2
* Feature 3

---

## Installation

### Projekt-Referenz

```xml
<ProjectReference Include="..\MyLibrary.<Name>\MyLibrary.<Name>.csproj" />
```

### NuGet

```powershell
Install-Package MyLibrary.<Name>
```

---

## Dependency Injection

```csharp
builder.Services.AddMyLibrary<Name>();
```

---

## Konfiguration

Beispiel:

```json
{
  "<Name>": {
    "Option1": "",
    "Option2": ""
  }
}
```

---

## Verwendung

```csharp
public class ExampleService
{
    private readonly I<Name>Service _service;

    public ExampleService(
        I<Name>Service service)
    {
        _service = service;
    }
}
```

---

## Architektur

Die Bibliothek folgt den Standards aus:

```text
MyLibrary.Architecture
```

---

## Tests

Testprojekt:

```text
MyLibrary.<Name>.Test
```

Tests ausführen:

```bash
dotnet test
```

---

## Versionierung

Semantic Versioning:

```text
MAJOR.MINOR.PATCH
```

Beispiel:

```text
1.0.0
```

---

## Lizenz

MIT License
