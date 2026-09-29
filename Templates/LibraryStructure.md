# Standard Library Structure

Für neue .NET-Repositories gilt verbindlich der
[.NET Repository Standard](../Standards/DotNet-Repository-Standard.md):
eine `.slnx` im Repository-Root, jedes Produktiv- und Testprojekt in einem eigenen
gleichnamigen Unterordner mit seiner `.csproj`, Repository-Dokumentation im Root.
Historische `.sln`-Dateien müssen nicht allein deshalb migriert
werden; für neue Solutions keine parallele `.sln` anlegen.

Version: 1.0

Dieses Dokument beschreibt die Standardstruktur einer MyLibrary-Bibliothek.

---

## Solution

```text
MyLibrary.<Name>/  # Repository-Root
├── MyLibrary.<Name>.slnx
├── MyLibrary.<Name>/
│   └── MyLibrary.<Name>.csproj
├── MyLibrary.<Name>.Tests/
│   └── MyLibrary.<Name>.Tests.csproj
├── .gitignore
├── README.md
├── CHANGELOG.md
└── LICENSE
```

---

## Bibliothek

```text
MyLibrary.<Name>

├─ Models
├─ Interfaces
├─ Services
├─ Extensions
├─ Configuration
├─ Exceptions
│
├─ Repositories
├─ Validators
├─ Infrastructure
│
└─ Components
```

---

## Testprojekt

```text
MyLibrary.<Name>.Tests

├─ Services
├─ Models
├─ Repositories
├─ Validators
└─ TestData
```

---

## Pflichtdateien

```text
README.md
CHANGELOG.md
LICENSE
.gitignore
```

---

## Extensions

```text
Extensions
└─ ServiceCollectionExtensions.cs
```

---

## Dependency Injection

```csharp
builder.Services.Add<Name>();
```

---

## Namespace Struktur

```text
MyLibrary.<Name>.Models
MyLibrary.<Name>.Interfaces
MyLibrary.<Name>.Services
MyLibrary.<Name>.Extensions
MyLibrary.<Name>.Configuration
MyLibrary.<Name>.Exceptions
```

---

## Beispiel

```text
MyLibrary.Email

├─ Models
├─ Interfaces
├─ Services
├─ Extensions
├─ Configuration
├─ Exceptions
├─ Repositories
├─ Validators
└─ Infrastructure
```
