# Create New Application Process

Dieser Prozess gilt für neue .NET-Anwendungen, Blazor-Apps, APIs, Worker, Services
und Konsolenanwendungen. Grundlage sind [Architecture AI Prompt](../Architecture-AI-Prompt.md),
[.NET Repository Standard](../Standards/DotNet-Repository-Standard.md),
[Naming Conventions](../Standards/Naming-Conventions.md) und
[Testing Standards](../Standards/Testing-Standards.md).

1. Anforderungen, App-Name, Target Framework und Hostingmodell bestimmen.
   Bereits getroffene Entscheidungen übernehmen.
2. Passendes Template wählen: [Blazor App](../Templates/BlazorAppTemplate.md),
   [Web API](../Templates/WebApiTemplate.md), [Worker](../Templates/WorkerServiceTemplate.md)
   oder [Console App](../Templates/ConsoleAppTemplate.md).
3. Git-Status und vorhandene Dateien prüfen. Benutzeränderungen erhalten.
   Ein neues lokales Repository verwendet `main`.
4. Im Repository-Root genau eine `<AppName>.slnx` erstellen.
   Produktivprojekt in `<AppName>/<AppName>.csproj` und xUnit-Testprojekt in
   `<AppName>.Tests/<AppName>.Tests.csproj` anlegen, beide zur Solution hinzufügen.
   Testprojekt auf das Produktivprojekt referenzieren. Bei einem Umbau vorhandene
   Projektdateien verschieben, Projektverweise anpassen und Doppelkopien vermeiden.
5. Root-Dateien `.gitignore`, `README.md`, `CHANGELOG.md` und `LICENSE` gemäß
   GitHub-Standard ergänzen. Keine Secrets oder Build-Ausgaben versionieren.
6. DI, Konfiguration und benötigte Bibliotheken einbinden. Logik außerhalb der UI
   implementieren und im separaten Testprojekt prüfen. Für einen Grundstand
   wenige aussagekräftige Smoke-/Integrationstests bereitstellen.
7. Bei nutzerseitigen Blazor-Apps das Informationsmuster aus dem Blazor-App-Template
   vollständig umsetzen: Beschreibung, Hilfe, versionierte Release Notes,
   Informationsseite, Navigation und konsistente Anwendungsmetadaten.
8. Formatprüfung, Restore, Release-Build, Tests, Solutionliste und Git-Prüfungen
   gemäß .NET Repository Standard ausführen. Informationsangebot im Host prüfen.
9. Änderungen, Testergebnisse und verbleibende Einschränkungen dokumentieren.
   Commit, Tag, Push und Veröffentlichung sind separate, ausdrücklich beauftragte Schritte.

Eine neue SLNX-Solution rechtfertigt keine ungefragte Migration historischer
Repositories oder Änderung referenzierter Bibliotheken.
