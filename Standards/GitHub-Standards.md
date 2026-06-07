# GitHub Standards

Version: 1.0

Dieses Dokument definiert die Git- und GitHub-Standards für alle Projekte der MyLibrary-Familie.

---

# Ziele

Alle Repositories sollen:

* konsistent aufgebaut sein
* leicht wartbar sein
* nachvollziehbar versioniert sein
* GitHub-Ready sein

---

# Repository Naming

Bibliotheken:

```text
MyLibrary.Email
MyLibrary.LinkListe
MyLibrary.Workflow
MyLibrary.Reporting
```

Architekturrepository:

```text
MyLibrary.Architecture
```

---

# Standardstruktur

Jedes Repository enthält mindestens:

```text
README.md
LICENSE
.gitignore
```

Optional:

```text
docs/
samples/
```

---

# Branch Strategie

Standardbranch:

```text
main
```

Der Branch:

```text
master
```

wird nicht verwendet.

---

# Git Konfiguration

Jeder Entwickler sollte setzen:

```bash
git config --global init.defaultBranch main
```

---

# Branch Typen

Feature:

```text
feature/add-email-service
feature/add-workflow-engine
```

Bugfix:

```text
bugfix/fix-smtp-timeout
bugfix/fix-firebird-connection
```

Hotfix:

```text
hotfix/fix-production-error
```

---

# Commit Messages

Commit Messages sollen fachlich aussagekräftig sein.

Gut:

```text
Add email service
Add link list component
Fix sorting of link categories
Update architecture standards
```

Nicht erwünscht:

```text
fix
update
changes
misc
```

---

# Pull Requests

Jeder Pull Request sollte:

* bauen
* Tests bestehen
* dokumentiert sein

---

# Build Validierung

Vor Push:

```bash
dotnet restore
dotnet build
dotnet test
```

---

# README Standard

Jedes Repository enthält:

* Beschreibung
* Installation
* Verwendung
* Konfiguration
* Beispielcode
* Tests

---

# Lizenz

Standardlizenz:

```text
MIT License
```

Abweichungen müssen dokumentiert werden.

---

# Releases

Versionierung nach Semantic Versioning.

Schema:

```text
MAJOR.MINOR.PATCH
```

Beispiele:

```text
1.0.0
1.1.0
1.1.1
2.0.0
```

---

# Tags

Releases werden getaggt.

Beispiel:

```text
v1.0.0
v1.1.0
v2.0.0
```

---

# .gitignore

Visual Studio Projekte verwenden eine standardisierte `.gitignore`.

Zusätzlich:

```gitignore
# Secrets
appsettings.Secrets.json

# Archives
*.zip
*.7z
*.rar
*.tar
*.tar.gz

# Export files
*.bak
*.tmp
*.temp
*.orig

# Generated packages
*.nupkg
*.snupkg

# Visual Studio

.vs/

# Build

bin/
obj/
```

---

# Repository Checkliste

Vor Veröffentlichung prüfen:

* README vorhanden
* LICENSE vorhanden
* .gitignore vorhanden
* Tests vorhanden
* Keine Secrets enthalten
* Standardbranch = main
* Build erfolgreich
* Tests erfolgreich

---

# Architekturkonformität

Neue Projekte sollen den Standards aus dem Repository

```text
MyLibrary.Architecture
```

folgen.

Insbesondere:

* Development Standard
* Database Standard
* Security Standard
* Testing Standard
* Naming Conventions
