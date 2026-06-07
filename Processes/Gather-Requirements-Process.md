# Gather Requirements Process

Version: 1.0

Dieses Dokument beschreibt den Standardprozess zur Ermittlung von Anforderungen für neue Bibliotheken und Anwendungen.

---

# Ziel

Ziel ist die Erstellung eines vollständigen Requirements-Dokuments als Grundlage für Architektur und Implementierung.

---

# Referenzen

Primäre Referenz:

```text
Templates/RequirementsTemplate.md
```

Verwendeter Prompt:

```text
Prompts/Gather-Requirements-Prompt.md
```

---

# Wann wird dieser Prozess verwendet?

Immer wenn:

* eine neue Bibliothek entsteht
* eine neue Anwendung entsteht
* größere Erweiterungen geplant werden

---

# Start

Neuen Chat erstellen.

Beispiel:

```text
Requirements for MyLibrary.Email
```

---

# Requirements-Interview durchführen

Prompt verwenden:

```text
Prompts/Gather-Requirements-Prompt.md
```

Das Interview erfolgt schrittweise.

---

# Ergebnis dokumentieren

Ergebnis speichern als:

```text
Requirements/MyLibrary.<Name>.Requirements.md
```

Beispiel:

```text
Requirements/MyLibrary.Email.Requirements.md
```

---

# Review der Anforderungen

Prüfen:

* Sind die Ziele klar?
* Sind die Anwendungsfälle vollständig?
* Sind Nicht-Ziele definiert?
* Sind Sicherheitsanforderungen beschrieben?
* Sind Schnittstellen dokumentiert?

---

# Architektur erstellen

Nach Abschluss:

```text
Requirements
↓
Architecture
```

Die Anforderungen dienen als Input für:

```text
Prompts/Create-New-Library-Prompt.md
```

---

# Implementierung

Nach erfolgreicher Erstellung:

```text
Requirements
↓
Create
↓
Implement
```

---

# Versionierung

Requirements-Dokumente werden versioniert.

Änderungen an Anforderungen erfolgen über Git.

---

# Qualitätsziel

Die Anforderungen sollen:

* vollständig
* verständlich
* nachvollziehbar
* testbar

sein.

Die Anforderungen bilden die Grundlage für Architektur, Implementierung, Tests und Dokumentation.
