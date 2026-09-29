# Blazor Application Template

Verbindliche Vorlage für neue nutzerseitige Blazor-Anwendungen. Für wiederverwendbare
UI-Bibliotheken gilt stattdessen das [Blazor Library Template](BlazorLibraryTemplate.md).
Es gelten der [.NET Repository Standard](../Standards/DotNet-Repository-Standard.md),
die Entwicklungs-, Naming-, GitHub-, Sicherheits- und Teststandards.

## Struktur

```text
<AppName>/                         # Repository-Root
├── <AppName>.slnx
├── <AppName>/                     # Produktivprojekt
│   ├── <AppName>.csproj
│   ├── Program.cs
│   ├── appsettings.json
│   ├── Properties/
│   ├── Components/
│   │   ├── App.razor
│   │   ├── Routes.razor
│   │   ├── _Imports.razor
│   │   ├── Layout/
│   │   │   ├── MainLayout.razor
│   │   │   └── NavMenu.razor
│   │   └── Pages/
│   │       ├── Home.razor
│   │       ├── Info.razor
│   │       └── Error.razor
│   └── wwwroot/
│       ├── about.md
│       ├── help.md
│       └── release-notes/
│           └── v<Version>.md
├── <AppName>.Tests/
│   └── <AppName>.Tests.csproj
├── .gitignore
├── README.md
├── CHANGELOG.md
└── LICENSE
```

Services, Interfaces, Models, Configuration und weitere Ordner werden nach Bedarf
im Produktivprojekt ergänzt. Keine leeren Schichten oder fachlichen Platzhalter
erzeugen. Unbenötigte Blazor-Demoseiten wie Counter und Weather entfernen.

## Host und Logik

`Program.cs` enthält Host-Aufbau, DI und Middleware. Bei Interactive Server:

```csharp
builder.Services.AddRazorComponents().AddInteractiveServerComponents();
// Bibliotheken über ihre dokumentierten DI-Einstiegspunkte registrieren.
// ... builder.Build(), Middleware einschließlich statischer Dateien und Antiforgery ...
app.MapRazorComponents<App>().AddInteractiveServerRenderMode();
```

Geschäfts- und Anwendungslogik gehört in testbare Services außerhalb der Razor-UI.
Das separate xUnit-Projekt referenziert die Anwendung. Zu Beginn genügen sinnvolle
Smoke-/Integrationstests für Host, DI und Informationsangebot; spätere Fachlogik
wird gemäß [Testing Standards](../Standards/Testing-Standards.md) getestet.

## Anwendungsinformation, Hilfe und Versionshistorie

Referenz ist das bewährte Informationsmuster aus Urlaub:
`src/UrlaubApp/Urlaub/Components/Pages/Info.razor` und dessen Navigation.
Übernommen wird das Muster, keine Urlaub-Fachlogik oder Urlaub-Inhalte.

Die gemeinsame Komponente `ApplicationDocumentation` aus
`MyLibrary.Blazor.Components.Components` stellt Anwendung, Beschreibung, Hilfe
und Versionshistorie als aufklappbare Abschnitte dar.

1. `MyLibrary.Blazor.Components` referenzieren und in `Program.cs` registrieren:

   ```csharp
   using MyLibrary.Blazor.Components.DependencyInjection;

   builder.Services.AddMyLibraryBlazorComponents(builder.Configuration);
   ```

2. In `Components/_Imports.razor` den Namespace importieren:

   ```razor
   @using MyLibrary.Blazor.Components.Components
   ```

3. `Components/Pages/Info.razor` bereitstellen (`AppName` ersetzen):

   ```razor
   @page "/info"
   @rendermode InteractiveServer

   <PageTitle>Informationen – AppName</PageTitle>
   <h1>AppName</h1>
   <ApplicationDocumentation />
   ```

4. Sichtbarer Navigationseintrag mit `<NavLink href="info">Informationen</NavLink>`.
   Optional zeigt die Startseite zusätzlich `<ApplicationVersion />` mit Link zur Info-Seite.

5. In `appsettings.json` Metadaten hinterlegen:

   ```json
   {
     "Application": {
       "Name": "AppName",
       "Version": "0.1.0",
       "ReleaseDate": "2026-09-29"
     }
   }
   ```

6. `wwwroot/about.md` beschreibt Zweck und tatsächlich verfügbaren Umfang.
   `wwwroot/help.md` erklärt Einstieg und Bedienung. Jede Version erhält eine
   eigene Datei `wwwroot/release-notes/v<Version>.md`, deren erste Überschrift
   Version, Kurztitel und Datum nennt. `ApplicationDocumentation` liest diese
   Dateien aus dem Webroot; Release Notes werden automatisch aufgelistet.
   Statische Assets der Komponenten müssen auch im veröffentlichten Host erreichbar sein.

App-Name, Projektversion, Anwendungsmetadaten, Changelog und Release Notes müssen
übereinstimmen. Repository-Dokumentation bleibt im Root; die Markdown-Dateien
im Webroot sind nutzerseitige Inhalte und enthalten keine Secrets oder Betriebsdetails.
Release Notes folgen der [Release Checklist](../Standards/Release-Checklist.md).

## Prüfung

Die Abschlussprüfungen des .NET Repository Standards ausführen. Zusätzlich den Host
starten und Navigation, `/info`, Beschreibung, Hilfe, Versionsauswahl sowie
das Auf- und Zuklappen der Abschnitte prüfen. Fachoberflächen werden nur auf
Grundlage der konkreten Anwendungsanforderungen ergänzt.
