# .NET Repository Standard

Dieser Standard ist verbindlich für **neue** .NET-Repositories der MyLibrary-Familie:
Bibliotheken, Anwendungen, Services, Worker, APIs und Konsolenanwendungen.
Bestehende historische Strukturen und `.sln`-Dateien müssen nicht allein wegen
dieser Regel migriert werden. Historische Releaseinformationen bleiben erhalten.

## Repository, Solution und Projekte

```text
<RepositoryRoot>/
├── <AppName>.slnx
├── <AppName>/
│   ├── <AppName>.csproj
│   └── ...
├── <AppName>.Tests/
│   ├── <AppName>.Tests.csproj
│   └── ...
├── .gitignore
├── README.md
├── CHANGELOG.md
└── LICENSE
```

- Repository und Hauptanwendung heißen `<AppName>`, beispielsweise `GaebApp`.
- Die Solution liegt im Repository-Root und heißt `<AppName>.slnx`.
- Jedes Produktiv- und Testprojekt liegt in einem eigenen gleichnamigen Unterordner.
  Projektdateien liegen niemals direkt im Root eines neuen mehrprojektfähigen
  Application-Repositories. Zusätzliche Projekte folgen demselben Muster.
- Testprojekte heißen immer `<Produktivprojekt>.Tests`, beispielsweise
  `GaebApp.Tests`, `MyLibrary.Email.Tests` oder `MyLibrary.Email.Worker.Tests`.
  Sie referenzieren ihr Produktivprojekt über `ProjectReference` und stehen in der Solution.
- Bei Bibliotheken wird `<AppName>` durch `MyLibrary.<Name>` ersetzt. Die
  bestehenden typbezogenen Namen für Console, API und Worker bleiben möglich;
  sie ändern die Ablage- und Testregeln nicht.
- Repository-Dokumentation, `.gitignore` und Lizenz liegen im Root. Die Lizenz
  richtet sich nach dem [GitHub-Standard](GitHub-Standards.md).
- `bin/`, `obj/`, `.vs/`, Benutzerdateien und Secrets werden gemäß
  [GitIgnoreTemplate](../Templates/GitIgnoreTemplate.md) ausgeschlossen.
- `.editorconfig` und `Directory.Build.props` sind keine generellen Pflichtdateien.
  Sie werden bei einem konkreten Bedarf ergänzt.

## Solutionformat und Tooling

Für neue .NET-Repositories ist ausschließlich `.slnx` der Standard. Für dieselbe
neue Solution darf keine parallele `.sln` angelegt werden. SLNX verwendet kompaktes
XML und ermöglicht übersichtliche Versionskontrolldiffs.

Die Solutionbefehle benötigen ein SLNX-fähiges SDK (mindestens .NET SDK 9.0.200).
Das Target Framework der Anwendung wird davon unabhängig gewählt: Eine
`net8.0`-Anwendung kann mit einem neueren SDK gebaut werden.
Seit .NET 10 erzeugt `dotnet new sln` standardmäßig SLNX; Vorlagen geben das Format
zur Eindeutigkeit dennoch explizit an. Siehe
[Microsoft: SLNX-Standard ab .NET 10](https://learn.microsoft.com/en-us/dotnet/core/compatibility/sdk/10.0/dotnet-new-sln-slnx-default)
und [dotnet sln](https://learn.microsoft.com/en-us/dotnet/core/tools/dotnet-sln).

Beispiel im Repository-Root, nachdem die Projekte angelegt wurden:

```powershell
dotnet new sln --name GaebApp --format slnx
dotnet sln GaebApp.slnx add GaebApp/GaebApp.csproj GaebApp.Tests/GaebApp.Tests.csproj
dotnet add GaebApp.Tests/GaebApp.Tests.csproj reference GaebApp/GaebApp.csproj
```

Die Solutionliste anschließend kontrollieren: Manche SDK-Versionen nehmen beim
Hinzufügen auch referenzierte Projekte rekursiv auf. Projekte anderer Repositories
gehören nicht automatisch in die Anwendungssolution; gegebenenfalls mit
`dotnet sln <AppName>.slnx remove <externer-Projektpfad>` aus der Solution entfernen.
Der `ProjectReference` bleibt dabei bestehen. Bei solchen externen Referenzen
sicherstellen, dass die gewählte Buildkonfiguration auch für diese Projekte gilt.

## Tests und Blazor

Separate Testprojekte sind nicht auf Bibliotheken beschränkt. Für neue Anwendungen,
Services, Worker, APIs und vergleichbare Projekte mit testbarer Logik ist grundsätzlich
ein separates xUnit-Projekt vorzusehen. Geschäfts-, Zustands-, Mapping-, Berechnungs-,
Validierungs- und Anwendungslogik wird außerhalb der UI gehalten und dort geprüft.
Einzelne Razor-Darstellungen benötigen nicht jeweils isolierte Tests.
Details: [Testing Standards](Testing-Standards.md).

Nutzerseitige Blazor-Anwendungen folgen verbindlich dem
[Blazor-App-Template](../Templates/BlazorAppTemplate.md), einschließlich
`wwwroot/about.md`, `wwwroot/help.md`, `wwwroot/release-notes/v<Version>.md`
innerhalb des Produktivprojekts und einer über die Navigation erreichbaren
Informationsseite mit Beschreibung, Hilfe und Versionshistorie.

## Abschlussprüfung

Im Repository-Root ausführen; den Solutionnamen anpassen:

```powershell
dotnet format GaebApp.slnx --verify-no-changes
dotnet restore GaebApp.slnx
dotnet build GaebApp.slnx --configuration Release
dotnet test GaebApp.slnx --configuration Release
dotnet sln GaebApp.slnx list
git diff --check
git status --short
```

Nach notwendigen Formatkorrekturen Formatprüfung, Build und Tests erneut ausführen.
Zusätzlich prüfen: keine parallele `.sln`, keine Projektdatei im Root,
korrekte Projektverweise, Testprojekt in der Solution und keine versionierten
oder unignorierten Build-Ausgaben. Bei einem Repository ohne ersten Commit
auch die unversionierten Dateien prüfen; `git diff --check` erfasst diese nicht.
