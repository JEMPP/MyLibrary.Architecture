# Standard Library Structure

Version: 1.0

Dieses Dokument beschreibt die Standardstruktur einer MyLibrary-Bibliothek.

---

## Solution

```text
MyLibrary.<Name>.sln

├─ MyLibrary.<Name>
└─ MyLibrary.<Name>.Tests
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
