# MyLibrary BPMN-Modellierungsstandard

## 1. Zweck

Dieser Standard definiert die Konventionen für die Dokumentation von Geschäftsprozessen innerhalb der MyLibrary-Umgebung mit BPMN 2.0.

Ziel ist es, Prozessmodelle zu erstellen, die:

* leicht verständlich,
* abteilungsübergreifend einheitlich,
* langfristig pflegbar,
* über Git versionierbar,
* unabhängig von einzelnen Mitarbeitern,
* als Grundlage für Prozessanalyse und Prozessoptimierung geeignet,
* und für eine spätere Veröffentlichung in zentralen Informationssystemen geeignet sind.

Als primäres Modellierungswerkzeug wird **Bizagi Modeler** verwendet.

Der Schwerpunkt dieses Standards liegt zunächst auf der Dokumentation, Analyse und Optimierung von Geschäftsprozessen. Eine technische Prozessautomatisierung ist nicht das primäre Ziel.

---

## 2. Modellierungsprinzip

Ein BPMN-Diagramm beschreibt einen **Geschäftsprozess**.

Das Modell soll insbesondere folgende Fragen beantworten:

* Was löst den Prozess aus?
* Welche Tätigkeiten werden ausgeführt?
* Wer ist für diese Tätigkeiten verantwortlich?
* Welche Entscheidungen werden getroffen?
* Welche externen Beteiligten wirken mit?
* Welches Ergebnis erzeugt der Prozess?

Technische Implementierungsdetails werden nur dann modelliert, wenn sie für das Verständnis des Geschäftsprozesses relevant sind.

Detaillierte Bedienhandlungen innerhalb einzelner Softwaremasken oder konkrete Quellcode-Logik sollen grundsätzlich nicht Bestandteil eines Geschäftsprozessmodells sein.

---

## 3. BPMN-Version

Die Modelle orientieren sich an **BPMN 2.0**.

Zu Beginn wird bewusst nur eine eingeschränkte Auswahl von BPMN-Elementen verwendet.

Bevorzugte Elemente sind:

* Startereignis
* Endereignis
* Aufgabe
* Teilprozess
* Exklusives Gateway (XOR)
* Pool
* Lane
* Sequenzfluss
* Nachrichtenfluss

Weitere BPMN-Elemente können verwendet werden, wenn sie für eine fachlich korrekte und verständliche Modellierung erforderlich sind.

Komplexe BPMN-Konstrukte sollen nicht allein deshalb verwendet werden, weil sie technisch verfügbar sind.

---

## 4. Benennung von Prozessen

Prozessnamen sollen den fachlichen Zweck eines Geschäftsprozesses beschreiben.

Beispiele:

* Rechnungen versenden
* Urlaubsantrag genehmigen
* Vermessungsdokumentation erstellen
* Kundenauftrag bearbeiten

Namen, die lediglich ein verwendetes System oder eine organisatorische Struktur beschreiben, sollen vermieden werden.

Ungünstige Beispiele:

* iOrga-Prozess
* Access-Workflow
* Buchhaltungsmaske

---

## 5. Benennung von Aktivitäten

Aktivitäten sollen grundsätzlich nach folgendem Schema benannt werden:

**Verb + Objekt**

Beispiele:

* Rechnung prüfen
* Urlaubsantrag genehmigen
* Vermessungsdokumentation erstellen
* Rechnung versenden
* Dokument archivieren

Die Benennung soll eine Tätigkeit und keinen Zustand ausdrücken.

Bevorzugt:

> Rechnung prüfen

anstatt:

> Rechnungsprüfung

---

## 6. Ereignisse

Jeder Prozess soll einen klar erkennbaren Start besitzen.

Soweit sinnvoll, soll der fachliche Auslöser bereits am Startereignis erkennbar sein.

Beispiele:

* Auftrag eingegangen
* Rechnung freigegeben
* Urlaubsantrag eingereicht

Ein Prozess soll ebenfalls mindestens ein fachlich sinnvolles Endereignis besitzen.

Das Endereignis soll das erreichte Prozessergebnis beschreiben, sofern dies das Verständnis verbessert.

Beispiele:

* Rechnung versendet
* Antrag genehmigt
* Auftrag abgelehnt

---

## 7. Pools

Pools repräsentieren voneinander unabhängige Prozessbeteiligte.

Typische Beispiele sind:

* intermetric
* Kunde
* Lieferant
* Deutsche Bahn
* Behörde

Unterschiedliche Organisationen sollen grundsätzlich in getrennten Pools dargestellt werden.

Sequenzflüsse dürfen Pool-Grenzen nicht überschreiten.

Die Kommunikation zwischen unterschiedlichen Pools wird über Nachrichtenflüsse dargestellt.

---

## 8. Lanes

Lanes repräsentieren Verantwortlichkeiten innerhalb eines Prozessbeteiligten.

Lanes sollen grundsätzlich verwendet werden für:

* Rollen,
* organisatorische Funktionen,
* Abteilungen.

Beispiele:

* Antragsteller
* Projektleitung
* Buchhaltung
* Abteilungsleitung

Einzelne Mitarbeiter sollen grundsätzlich nicht als Lane bezeichnet werden.

Bevorzugt:

> Projektleitung

anstatt:

> Max Muster

---

## 9. Sequenzflüsse

Sequenzflüsse beschreiben die zeitliche oder logische Reihenfolge innerhalb eines Pools.

Der normale Prozessablauf soll durch die Sequenzflüsse möglichst einfach erkennbar sein.

Unnötige Kreuzungen von Sequenzflüssen sollen vermieden werden.

---

## 10. Nachrichtenflüsse

Nachrichtenflüsse stellen die Kommunikation zwischen unterschiedlichen Prozessbeteiligten dar.

Beispiele:

* Kunde sendet Auftrag
* Buchhaltung sendet Rechnung
* Lieferant sendet Bestätigung

Nachrichtenflüsse dürfen nur zwischen unterschiedlichen Pools verwendet werden.

---

## 11. Gateways

Exklusive Gateways werden verwendet, wenn der weitere Prozessablauf von einer Bedingung abhängt.

Soweit sinnvoll, soll ein Gateway als Frage formuliert werden.

Beispiele:

* Rechnung vollständig?
* Genehmigung erteilt?
* Kundendaten vorhanden?

Ausgehende Pfade sollen eindeutig beschriftet werden.

Beispiele:

* Ja / Nein
* Genehmigt / Abgelehnt
* Vollständig / Unvollständig

Ein Gateway führt selbst keine Tätigkeit aus.

---

## 12. Teilprozesse

Ein Teilprozess soll verwendet werden, wenn ein Prozessabschnitt:

* aus mehreren Aktivitäten besteht,
* wiederverwendet wird,
* eine eigene fachlich sinnvolle Logik besitzt,
* oder das Hauptdiagramm unnötig komplex machen würde.

Der übergeordnete Prozess soll weiterhin verständlich bleiben, ohne sämtliche Details darstellen zu müssen.

---

## 13. Prozesskomplexität

Das Ziel besteht nicht darin, die gesamte Organisation in einem einzigen Diagramm abzubilden.

Ein Prozessmodell soll möglichst auf einem übersichtlichen Diagramm verständlich darstellbar sein.

Wird ein Modell unübersichtlich, soll der Prozess in Teilprozesse gegliedert werden.

Verständlichkeit hat Vorrang vor der Darstellung jedes theoretisch möglichen Sonderfalls.

---

## 14. Ausnahmefälle

Ausnahmefälle sollen nur dann modelliert werden, wenn sie relevant sind für:

* das Verständnis des Prozesses,
* Verantwortlichkeiten,
* rechtliche oder organisatorische Vorgaben,
* Qualitätssicherung,
* oder Prozessoptimierung.

Seltene technische Ausnahmefälle sollen grundsätzlich separat dokumentiert werden, wenn ihre Darstellung den Hauptprozess unnötig unübersichtlich machen würde.

---

## 15. Farben

Farben dürfen zur Verbesserung der Übersichtlichkeit verwendet werden.

Farben dürfen keine undokumentierte fachliche Bedeutung besitzen.

Ein Prozessmodell muss auch dann verständlich bleiben, wenn die Farbdarstellung nicht zur Verfügung steht.

---

## 16. Prozesskennzeichnung

Jeder dokumentierte Geschäftsprozess erhält eine eindeutige Prozess-ID.

Vorgesehenes Format:

`PRC-###`

Beispiele:

* PRC-001
* PRC-002
* PRC-003

Die Prozess-ID bleibt dauerhaft bestehen, auch wenn sich der Name eines Prozesses später ändert.

---

## 17. Prozessmetadaten

Jede Prozessdokumentation enthält mindestens folgende Angaben:

* Prozess-ID
* Prozessname
* Zweck
* Prozessverantwortlicher
* Auslöser
* Ergebnis
* Status

Soweit sinnvoll, sollen zusätzlich dokumentiert werden:

* Kategorie,
* beteiligte Rollen,
* beteiligte Organisationen,
* verwendete Systeme,
* zusammenhängende Prozesse,
* relevante Dokumente,
* relevante Richtlinien oder Vorgaben,
* Leseberechtigungen.

---

## 18. Prozessstatus

Für Geschäftsprozesse werden folgende Zustände verwendet:

* **Entwurf**
* **Prüfung**
* **Freigegeben**
* **Obsolet**

### Entwurf

Der Prozess wird erstellt oder überarbeitet.

### Prüfung

Das Modell ist fachlich vollständig und befindet sich in der Prüfung.

### Freigegeben

Der Prozess wurde geprüft und stellt den aktuell gültigen Geschäftsprozess dar.

### Obsolet

Der Prozess ist nicht mehr gültig, bleibt jedoch aus Gründen der Nachvollziehbarkeit in der Versionshistorie erhalten.

---

## 19. Repository-Prinzip

Das native Bizagi-Modell ist nicht die einzige Prozessdarstellung, die im Git-Repository gespeichert wird.

Soweit technisch möglich, soll ein Prozess folgende Bestandteile enthalten:

* das bearbeitbare Bizagi-Modell,
* einen BPMN-2.0-Export,
* eine visuelle Darstellung,
* eine Markdown-Dokumentation,
* maschinenlesbare Prozessmetadaten,
* und bei Bedarf eine veröffentlichbare Web-Dokumentation.

Die einzelnen Artefakte haben unterschiedliche Aufgaben:

| Artefakt       | Zweck                                              |
| -------------- | -------------------------------------------------- |
| `.bpm`         | Führendes, bearbeitbares Bizagi-Modell             |
| `.bpmn`        | Standardisiertes BPMN-2.0-Austauschformat          |
| `.svg`         | Schnelle visuelle Darstellung                      |
| `README.md`    | Lesbare fachliche Prozessdokumentation             |
| `process.json` | Maschinenlesbare Prozessmetadaten                  |
| `web/`         | Interaktive veröffentlichbare Bizagi-Dokumentation |
| `.pdf`         | Optionales Dokumentations- und Archivformat        |

Das BPMN-Modell beschreibt die Prozesslogik.

Die Markdown-Dokumentation enthält ergänzende Informationen und Metadaten, die sich nicht sinnvoll unmittelbar im Diagramm darstellen lassen.

---

## 20. Maschinenlesbare Prozessmetadaten

Jeder veröffentlichbare Prozess soll eine Datei `process.json` besitzen.

Diese Datei dient als maschinenlesbare Schnittstelle zwischen der Prozessdokumentation und Anwendungen wie iOrga.

Die Datei enthält mindestens:

* Prozess-ID,
* Prozessname,
* Kategorie,
* Prozessverantwortlichen,
* Status,
* Leseberechtigungen.

Beispiel:

```json
{
  "id": "PRC-001",
  "name": "Rechnungen versenden",
  "category": "Finanzen",
  "owner": "Buchhaltung",
  "status": "Freigegeben",
  "permissions": [
    "BusinessProcesses.Finance.Read"
  ]
}
```

Personenbezogene Benutzerkonten sollen nicht unmittelbar als Berechtigungen in `process.json` hinterlegt werden.

Berechtigungen sollen rollen- oder funktionsbezogen definiert werden.

Beispiele:

```text
BusinessProcesses.Read
BusinessProcesses.Finance.Read
BusinessProcesses.HR.Read
BusinessProcesses.Projects.Read
BusinessProcesses.Surveying.Read
```

Dadurch bleiben Prozessdefinitionen unabhängig von einzelnen Mitarbeitern.

---

## 21. Veröffentlichung von Geschäftsprozessen

Geschäftsprozesse sollen so dokumentiert und versioniert werden, dass eine spätere Veröffentlichung in zentralen Informationssystemen möglich ist.

Für die MyLibrary-Umgebung ist insbesondere eine Veröffentlichung innerhalb von **iOrga** vorgesehen.

Dabei gelten folgende Verantwortlichkeiten:

### Bizagi Modeler

Bizagi Modeler ist das primäre Werkzeug zur Erstellung und Pflege der BPMN-Prozessmodelle.

### Git

Das Git-Repository ist die versionierte Quelle der Prozessdokumentation.

Änderungen an Geschäftsprozessen müssen über die Git-Historie nachvollziehbar bleiben.

### iOrga

iOrga dient als lesendes Prozessportal für Anwender.

Die Bearbeitung der BPMN-Modelle erfolgt nicht innerhalb von iOrga.

Das grundsätzliche Veröffentlichungsmodell lautet:

```text
Bizagi Modeler
      ↓
MyLibrary.BusinessProcesses
      ↓
Deployment / Import
      ↓
iOrga
```

---

## 22. Darstellung in iOrga

iOrga soll Prozesse in einer zentralen Prozessbibliothek darstellen können.

Eine Prozessseite kann insbesondere enthalten:

* Prozess-ID,
* Prozessname,
* Status,
* Prozessverantwortlichen,
* Zweck,
* beteiligte Rollen,
* verwendete Systeme,
* verwandte Prozesse,
* BPMN-Diagramm,
* interaktive Prozessdokumentation,
* ergänzende Dokumente.

Die Darstellung in iOrga ist von der Modellierung in Bizagi getrennt.

iOrga ist kein BPMN-Editor.

---

## 23. Interaktive Prozessdokumentation

Für eine interaktive Darstellung kann die von Bizagi erzeugte Web-Dokumentation verwendet werden.

Diese kann insbesondere genutzt werden für:

* die Darstellung des Prozessdiagramms,
* Zoom und Navigation,
* die Anzeige dokumentierter BPMN-Elemente,
* die Navigation in Teilprozesse.

Die Web-Dokumentation ist ein Veröffentlichungsartefakt und nicht die führende Quelle des Prozesses.

Führend bleibt das versionierte Prozessmodell im Git-Repository.

---

## 24. Zugriffsschutz

Prozessdokumentationen können unterschiedliche Leseberechtigungen besitzen.

iOrga darf einem Benutzer nur diejenigen Prozesse anzeigen, für die der Benutzer die erforderlichen Berechtigungen besitzt.

Berechtigungen sollen fachlich und rollenbezogen definiert werden.

Beispiel:

```text
BusinessProcesses.Read
BusinessProcesses.Finance.Read
BusinessProcesses.HR.Read
```

Eine reine Ausblendung eines Links oder Menüpunktes ist kein ausreichender Zugriffsschutz.

Geschützte Prozessdateien dürfen nicht über einen öffentlich erreichbaren statischen Pfad bereitgestellt werden, wenn dadurch die Berechtigungsprüfung umgangen werden könnte.

Insbesondere sollen geschützte Veröffentlichungsdateien nicht ungeprüft aus einem öffentlichen `wwwroot` ausgeliefert werden.

Die Auslieferung geschützter Prozessinhalte muss serverseitig autorisiert werden.

---

## 25. Trennung von Modellierung und Veröffentlichung

Die Modellierung und Freigabe eines Prozesses erfolgt außerhalb von iOrga.

Der vorgesehene Ablauf lautet:

```text
Prozess in Bizagi bearbeiten
        ↓
Bizagi-Modell speichern
        ↓
BPMN-Export aktualisieren
        ↓
SVG / Web-Dokumentation aktualisieren
        ↓
README und process.json prüfen
        ↓
Änderungen in Git committen
        ↓
Änderungen veröffentlichen
        ↓
iOrga stellt freigegebenen Stand bereit
```

Damit bleiben Modellierung, Versionierung und Veröffentlichung klar voneinander getrennt.

---

## 26. Änderungsprinzip

Änderungen an freigegebenen Geschäftsprozessen werden über Git versioniert.

Ein Prozessmodell soll einen freigegebenen Geschäftsprozess nicht stillschweigend ersetzen, ohne dass die Änderung über die Repository-Historie nachvollziehbar ist.

Die Git-Commit-Historie dient als technische Änderungshistorie.

Wesentliche fachliche Änderungen sollen zusätzlich in der Prozessdokumentation beschrieben werden.

---

## 27. Modellierungsprioritäten

Wenn mehrere Modellierungsvarianten fachlich möglich sind, gelten folgende Prioritäten:

1. Fachliche Korrektheit
2. Verständlichkeit
3. Einheitlichkeit
4. Einfachheit
5. BPMN-Präzision
6. Optische Gestaltung

Ein einfaches, korrektes und gut verständliches Modell ist einem unnötig komplexen Modell mit vielen speziellen BPMN-Elementen vorzuziehen.

---

## 28. Weiterentwicklung des Standards

Dieser Standard beginnt bewusst mit einem eingeschränkten BPMN-Umfang.

Weitere Konventionen und BPMN-Elemente werden ergänzt, wenn sich bei der praktischen Modellierung zeigt, dass sie benötigt werden.

Der Standard soll sich anhand realer Geschäftsprozesse weiterentwickeln und nicht aufgrund theoretischer Vollständigkeit.
