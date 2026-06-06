# Database Standards

Version: 1.0

Dieses Dokument definiert die Datenbankstandards für alle Projekte der MyLibrary-Familie.

---

# Ziele

Die Datenbankzugriffe sollen:

* testbar sein
* wartbar sein
* performant sein
* datenbankunabhängig sein
* sicher sein
* wiederverwendbar sein

---

# Unterstützte Datenbanksysteme

Aktuell werden unterstützt:

* Microsoft SQL Server
* Firebird SQL
* Microsoft Access

Weitere Datenbanksysteme können ergänzt werden.

---

# Datenzugriffsstrategie

## Standard

Für Datenbankzugriffe wird Dapper verwendet.

Begründung:

* Hohe Performance
* Volle SQL-Kontrolle
* Geringe Komplexität
* Gute Testbarkeit
* Keine versteckte SQL-Generierung

---

# Verwendete NuGet-Pakete

## SQL Server

```text id="z6emrl"
Microsoft.Data.SqlClient
Dapper
```

## Firebird

```text id="r6rq4p"
FirebirdSql.Data.FirebirdClient
Dapper
```

## Access

```text id="35sn8j"
System.Data.OleDb
Dapper
```

---

# Architektur

## Schichtenmodell

```text id="t5hpkq"
Services
↓
Repositories
↓
Connection Factory
↓
Datenbank
```

---

# Services

Services enthalten Geschäftslogik.

Services enthalten keine SQL-Statements.

Beispiel:

```csharp id="uxp1z9"
public class CustomerService
{
    private readonly ICustomerRepository _repository;
}
```

---

# Repositories

Repositories enthalten SQL-Zugriffe.

Beispiel:

```csharp id="fxjjdz"
ICustomerRepository
CustomerRepository
```

---

# Connection Factory

Datenbankverbindungen werden über Factories erstellt.

Beispiel:

```csharp id="ljrtu9"
IDbConnectionFactory
SqlConnectionFactory
FirebirdConnectionFactory
AccessConnectionFactory
```

---

# Verbindungsverwaltung

Connections werden möglichst kurz gehalten.

Beispiel:

```csharp id="wr0dwl"
using var connection =
    _connectionFactory.CreateConnection();
```

Connections werden nicht als Singleton gespeichert.

Nicht erlaubt:

```csharp id="a2j3iu"
private SqlConnection _connection;
```

---

# SQL

## SQL bleibt sichtbar

SQL darf als SQL geschrieben werden.

Erlaubt:

```sql id="13v64x"
SELECT *
FROM Customer
WHERE CustomerId = @CustomerId
```

Nicht erwünscht:

Versteckte SQL-Generierung.

---

# Parameterisierung

SQL-Parameter sind verpflichtend.

Erlaubt:

```csharp id="8u0v0c"
var sql =
    "SELECT * FROM Customer WHERE Id = @Id";

await connection.QueryAsync<Customer>(
    sql,
    new { Id = id });
```

Nicht erlaubt:

```csharp id="v7n8i4"
var sql =
    $"SELECT * FROM Customer WHERE Id = {id}";
```

---

# SQL Injection

Stringverkettungen für SQL sind verboten.

Jede Benutzereingabe wird parameterisiert.

---

# Async First

Datenbankzugriffe werden asynchron implementiert.

Erlaubt:

```csharp id="qnd7k2"
await connection.QueryAsync<T>();
```

```csharp id="mkj92t"
await connection.ExecuteAsync();
```

Nicht erlaubt:

```csharp id="8qod3o"
connection.Query<T>();
```

wenn keine besonderen Gründe vorliegen.

---

# Repository-Beispiel

```csharp id="t9gwyv"
public class CustomerRepository
    : ICustomerRepository
{
    private readonly IDbConnectionFactory _factory;

    public CustomerRepository(
        IDbConnectionFactory factory)
    {
        _factory = factory;
    }

    public async Task<Customer?> GetByIdAsync(int id)
    {
        using var connection =
            _factory.CreateConnection();

        const string sql =
            """
            SELECT *
            FROM Customer
            WHERE Id = @Id
            """;

        return await connection.QuerySingleOrDefaultAsync<Customer>(
            sql,
            new { Id = id });
    }
}
```

---

# SQL-Dateien

Für komplexe Abfragen dürfen externe SQL-Dateien verwendet werden.

Beispiel:

```text id="5iyub1"
Sql
├─ Customer
│  ├─ GetById.sql
│  ├─ Search.sql
│  └─ Update.sql
```

Empfohlen bei:

* langen Reports
* Firebird-Statements
* komplexen Joins
* Wartungsabfragen

---

# Transaktionen

Mehrere zusammengehörige Datenänderungen werden transaktional ausgeführt.

Beispiel:

```csharp id="5z94rk"
using var transaction =
    connection.BeginTransaction();
```

Commit:

```csharp id="6jlwmq"
transaction.Commit();
```

Rollback:

```csharp id="pd0wsm"
transaction.Rollback();
```

---

# Connection Strings

Connection Strings gehören niemals in den Code.

Nicht erlaubt:

```csharp id="bngll8"
var connectionString =
    "Server=...";
```

Erlaubt:

```json id="2u7s90"
{
  "ConnectionStrings": {
    "MainDatabase": ""
  }
}
```

---

# Geheimnisse

Produktive Credentials gehören in:

```text id="ffryy2"
appsettings.Secrets.json
```

Diese Datei wird nicht versioniert.

Beispiel:

```gitignore id="jzpd4f"
appsettings.Secrets.json
```

---

# SQL Server Standards

## Datentypen

Bevorzugt:

```sql id="3t4v8s"
nvarchar
datetime2
decimal
uniqueidentifier
```

Vermeiden:

```sql id="f5c6ig"
text
ntext
image
```

---

# Firebird Standards

## SQL Dialect

Verwendet wird:

```text id="pqvayl"
Dialect 3
```

---

## Datumswerte

Datumswerte werden parameterisiert.

Keine Stringkonvertierungen.

---

## Generatoren / Sequences

Bevorzugt:

```sql id="zdh5c7"
NEXT VALUE FOR
```

anstelle alter Generator-Syntax.

---

# Microsoft Access Standards

Access wird ausschließlich für:

* Legacy-Systeme
* Import/Export
* Reporting

verwendet.

Keine neuen Geschäftsanwendungen sollen auf Access basieren.

---

# Mapping

Dapper-Mappings erfolgen bevorzugt über:

```csharp id="8jy0uq"
Customer
Order
Invoice
```

und nicht über:

```csharp id="7xotnn"
dynamic
```

---

# Fehlerbehandlung

Datenbankfehler werden geloggt.

Beispiel:

```csharp id="j1spgu"
_logger.LogError(
    ex,
    "Fehler beim Lesen des Kunden {CustomerId}",
    id);
```

---

# Logging

Logging erfolgt über:

```csharp id="ib5v1w"
ILogger<T>
```

Die Anwendung verwendet standardmäßig Serilog.

Repositories verwenden niemals:

```csharp id="l98o7g"
Console.WriteLine(...)
```

---

# Unit Tests

Repositories werden möglichst über Interfaces abstrahiert.

Geschäftslogik wird gegen Mock-Repositories getestet.

Beispiel:

```csharp id="j7g8aq"
ICustomerRepository
```

---

# Review-Checkliste

Vor jedem Commit prüfen:

* Werden SQL-Parameter verwendet?
* Gibt es SQL-Injection-Risiken?
* Sind Connection Strings ausgelagert?
* Werden Transaktionen korrekt verwendet?
* Werden Connections sauber geschlossen?
* Wird Dapper verwendet?
* Werden Repository-Interfaces verwendet?
* Wird asynchron gearbeitet?
* Werden Datenbankfehler geloggt?
* Sind Geheimnisse ausgeschlossen?
