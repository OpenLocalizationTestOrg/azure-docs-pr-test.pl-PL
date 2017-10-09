---
title: "Azure Cosmos DB: rozpoczęcie pracy z interfejsem API usługi DocumentDB na platformie .NET Core — samouczek | Microsoft Docs"
description: "Samouczek, który powoduje utworzenie bazy danych w trybie online i aplikacji konsolowej C# za pomocą hello Azure rozwiązania Cosmos bazy danych DocumentDB interfejsu API platformy .NET Core SDK."
services: cosmos-db
documentationcenter: .net
author: arramac
manager: jhubbard
editor: 
ms.assetid: 9f93e276-9936-4efb-a534-a9889fa7c7d2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 5e7efb327252e9e73e9b2a340820eeecc6937fa5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-getting-started-with-hello-documentdb-api-and-net-core"></a>Azure rozwiązania Cosmos bazy danych: Wprowadzenie do korzystania z hello interfejsu API usługi DocumentDB i .NET Core
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js dla MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Interfejs API usługi DocumentDB dla bazy danych rozwiązania Cosmos Azure Wprowadzenie — samouczek platformy .NET Core toohello Zapraszamy! W ramach tego samouczka zostanie utworzona aplikacja konsolowa, która tworzy zasoby usługi Azure Cosmos DB i wykonuje dla nich zapytania.

Omówione zostaną następujące czynności:

* Tworzenie i łączenie tooan konta bazy danych Azure rozwiązania Cosmos
* Konfigurowanie rozwiązania Visual Studio
* Tworzenie bazy danych w trybie online
* Tworzenie kolekcji
* Tworzenie dokumentów JSON
* Wykonywanie zapytania hello kolekcji
* Zastępowanie dokumentu
* Usuwanie dokumentu
* Usunięcie hello bazy danych

Nie masz czasu? Nie martw się! Witaj kompletne rozwiązanie jest dostępne na [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started). Przeskocz toohello [pobrać sekcji kompletnego rozwiązania hello](#GetSolution) Aby uzyskać krótkie instrukcje.

Mają toobuild Xamarin iOS, Android lub formularzy przy użyciu aplikacji hello interfejsu API usługi DocumentDB i .NET Core SDK? Zobacz [tworzenie aplikacji dla urządzeń przenośnych dzięki platformie Xamarin i usłudze Azure DB rozwiązania Cosmos](mobile-apps-with-xamarin.md).

> [!NOTE]
> Hello Azure rozwiązania Cosmos DB .NET Core SDK używany w tym samouczku nie jest jeszcze zgodne z aplikacjami systemu Windows platformy Uniwersalnej. Dla wersji preview hello .NET Core SDK, który obsługuje aplikacje platformy uniwersalnej systemu Windows, Wyślij wiadomość e-mail zbyt[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

Teraz do dzieła!

## <a name="prerequisites"></a>Wymagania wstępne
Upewnij się, że masz następujące hello:

* Aktywne konto platformy Azure. Jeśli go nie masz, możesz zarejestrować się w celu [utworzenia bezpłatnego konta](https://azure.microsoft.com/free/). 
    * Alternatywnie można użyć hello [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) w tym samouczku.
* [Visual Studio 2017](https://www.visualstudio.com/vs/) 
    * Jeśli pracujesz nad MacOS lub Linux, można tworzyć aplikacje .NET Core z wiersza polecenia hello instalując hello [.NET Core SDK](https://www.microsoft.com/net/core#macos) platformy hello wybranych przez użytkownika. 
    * Podczas pracy w systemie Windows, instalując hello można tworzyć aplikacje .NET Core z wiersza polecenia hello [.NET Core SDK](https://www.microsoft.com/net/core#windows). 
    * Możesz użyć własnego edytora lub pobrać bezpłatny program [Visual Studio Code](https://code.visualstudio.com/) działający na komputerach z systemem Windows, Linux i MacOS. 

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Krok 1. Tworzenie konta usługi Azure Cosmos DB
Utwórzmy konto usługi Azure Cosmos DB. Jeśli masz już konto ma toouse, możesz przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS). Jeśli używasz hello Azure rozwiązania Cosmos DB emulatora, należy wykonać czynności hello na [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) toosetup hello emulatora i przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a>Krok 2. Konfigurowanie rozwiązania programu Visual Studio
1. Otwórz program **Visual Studio 2017** na komputerze.
2. Na powitania **pliku** menu, wybierz opcję **nowy**, a następnie wybierz pozycję **projektu**.
3. W hello **nowy projekt** okno dialogowe, wybierz opcję **szablony** / **Visual C#** / **.NET Core** / **Aplikacji konsoli (.NET Core)**, nazwy projektu **DocumentDBGettingStarted**, a następnie kliknij przycisk **OK**.

   ![Zrzut ekranu okna nowy projekt hello](./media/documentdb-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. W hello **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **DocumentDBGettingStarted**.
5. Następnie bez opuszczania hello menu, kliknij przycisk **Zarządzaj pakietami NuGet...** .

   ![Zrzut ekranu przedstawiający hello prawo kliknięto element Menu hello projektu](./media/documentdb-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. W hello **NuGet** , kliknij pozycję **Przeglądaj** u góry okna hello i typ hello **usługa azure documentdb** w polu wyszukiwania hello.
7. W wynikach hello znaleźć **Microsoft.Azure.DocumentDB.Core** i kliknij przycisk **zainstalować**.
   Identyfikator pakietu Hello hello biblioteki klienta usługi DocumentDB dla platformy .NET Core jest [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core). Jeśli elementem docelowym jest wersja programu .NET Framework (na przykład net461), która nie jest obsługiwana przez ten pakiet .NET Core NuGet, użyj elementu [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) obsługującego wszystkie wersje programu .NET Framework, począwszy od wersji .NET Framework 4.5.
8. Na monitach hello Zaakceptuj instalacji pakietu NuGet hello hello umowy licencyjnej.

Wspaniale! Teraz, gdy zakończeniu hello instalacji, Zacznijmy pisanie kodu. Ukończony projekt kodu z tego samouczka można znaleźć w witrynie [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).

## <a id="Connect"></a>Krok 3: Łączenie tooan konta bazy danych Azure rozwiązania Cosmos
Najpierw dodaj te odwołania toohello początku aplikacji C#, w pliku Program.cs hello:

```csharp
using System;

// ADD THIS PART tooYOUR CODE
using System.Linq;
using System.Threading.Tasks;
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

> [!IMPORTANT]
> W kolejności toocomplete tego samouczka, upewnij się, że dodano zależności hello powyżej.

Dodaj teraz te dwie stałe i zmienną *client* poniżej klasy publicznej *Program*.

```csharp
class Program
{
    // ADD THIS PART tooYOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

Następnie przejdź toohello [Azure Portal](https://portal.azure.com) tooretrieve identyfikator URI i klucz podstawowy. Hello Azure rozwiązania Cosmos DB URI oraz primary key są niezbędne dla twojej aplikacji toounderstand gdzie tooconnect na oraz bazy danych Azure rozwiązania Cosmos tootrust połączeniu aplikacji.

W hello portalu Azure, przejdź do konta bazy danych Azure rozwiązania Cosmos tooyour, a następnie kliknij **klucze**.

Skopiuj hello identyfikatora URI z portalu hello i wklej ją do `<your endpoint URI>` w pliku program.cs hello. Następnie kopiowania hello klucza podstawowego z portalu hello i wklej ją do `<your key>`. Jeśli używasz hello Azure rozwiązania Cosmos DB emulatora, użyj `https://localhost:8081` jako punktu końcowego hello i hello autoryzacji dobrze zdefiniowany klucz z [jak przy użyciu toodevelop hello Azure rozwiązania Cosmos DB emulatora](local-emulator.md). Upewnij się, że hello tooremove < i >, ale pozostawić hello cudzysłowów wokół punktu końcowego, a klucz.

![Zrzut ekranu przedstawiający hello Portal Azure używany przez hello toocreate samouczka NoSQL aplikacji konsolowej C#. Pokazuje bazy danych Azure rozwiązania Cosmos konto, z wyróżnionym, AKTYWNYM Centrum hello hello przyciskiem KLUCZE wyróżnionym w bloku konta usługi Azure DB rozwiązania Cosmos hello i hello wartości identyfikatora URI, klucz podstawowy i klucz POMOCNICZY wyróżnionymi w hello bloku klucze][keys]

Zaczniemy aplikacji hello rozpoczynania pracy, tworząc nowe wystąpienie klasy hello **DocumentClient**.

Poniżej hello **Main** metody, dodaj to nowe zadanie asynchroniczne o nazwie **GetStartedDemo**, które zostaną nowe wystąpienie klasy **DocumentClient**.

```csharp
static void Main(string[] args)
{
}

// ADD THIS PART tooYOUR CODE
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);
}
```

Dodaj hello poniższy kod toorun zadania asynchronicznego z Twojej **Main** metody. Witaj **Main** metoda będzie przechwytywać wyjątki i zapisywać je toohello konsoli.

```csharp
static void Main(string[] args)
{
        // ADD THIS PART tooYOUR CODE
        try
        {
                Program p = new Program();
                p.GetStartedDemo().Wait();
        }
        catch (DocumentClientException de)
        {
                Exception baseException = de.GetBaseException();
                Console.WriteLine("{0} error occurred: {1}, Message: {2}", de.StatusCode, de.Message, baseException.Message);
        }
        catch (Exception e)
        {
                Exception baseException = e.GetBaseException();
                Console.WriteLine("Error: {0}, Message: {1}", e.Message, baseException.Message);
        }
        finally
        {
                Console.WriteLine("End of demo, press any key tooexit.");
                Console.ReadKey();
        }
```

Naciśnij klawisz hello **DocumentDBGettingStarted** przycisk toobuild i uruchamianie aplikacji hello.

Gratulacje! Pomyślnie nawiązano połączenie konto bazy danych Azure rozwiązania Cosmos tooan, teraz Spójrzmy w pracy z zasobami Azure DB rozwiązania Cosmos.  

## <a name="step-4-create-a-database"></a>Krok 4. Tworzenie bazy danych
Przed dodaniem hello kod służący do tworzenia bazy danych Dodaj metodę pomocnika na potrzeby zapisywania toohello konsoli.

Skopiuj i Wklej hello **WriteToConsoleAndPromptToContinue** poniżej hello **GetStartedDemo** metody.

```csharp
// ADD THIS PART tooYOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
}
```

Bazy danych programu Azure rozwiązania Cosmos [bazy danych](documentdb-resources.md#databases) można tworzyć przy użyciu hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) metody hello **DocumentClient** klasy. Baza danych jest hello kontenerem logicznym magazynu dokumentów JSON podzielonym na partycje w kolekcjach.

Kopiuj i wklej następujący hello kodu tooyour **GetStartedDemo** poniżej powitania klienta tworzenia metody. Spowoduje to utworzenie bazy danych o nazwie *FamilyDB*.

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

Naciśnij klawisz hello **DocumentDBGettingStarted** przycisk toorun aplikacji.

Gratulacje! Pomyślnie utworzono bazę danych usługi Azure Cosmos DB.  

## <a id="CreateColl"></a>Krok 5. Tworzenie kolekcji
> [!WARNING]
> Metoda **CreateDocumentCollectionAsync** utworzy nową kolekcję z zarezerwowaną przepływnością, co ma wpływ na cenę. Aby uzyskać więcej informacji, odwiedź naszą [stronę cennika](https://azure.microsoft.com/pricing/details/cosmos-db/).

A [kolekcji](documentdb-resources.md#collections) można tworzyć przy użyciu hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) metody hello **DocumentClient** klasy. Kolekcja jest kontenerem dokumentów JSON i skojarzonej logiki aplikacji JavaScript.

Kopiuj i wklej następujący hello kodu tooyour **GetStartedDemo** poniżej hello tworzenie bazy danych. Spowoduje to utworzenie kolekcji dokumentów o nazwie *FamilyCollection_oa*.

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

Naciśnij klawisz hello **DocumentDBGettingStarted** przycisk toorun aplikacji.

Gratulacje! Pomyślnie utworzono kolekcję dokumentów Azure Cosmos DB.  

## <a id="CreateDoc"></a>Krok 6. Tworzenie dokumentów JSON
A [dokumentu](documentdb-resources.md#documents) można tworzyć przy użyciu hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) metody hello **DocumentClient** klasy. Dokumenty są zawartością JSON zdefiniowaną przez użytkownika (dowolną). Można teraz wstawić jeden lub więcej dokumentów. Jeśli masz już dane, które chcesz toostore w bazie danych, możesz użyć Azure rozwiązania Cosmos DB [narzędzia migracji danych](import-data.md).

Najpierw należy toocreate **rodziny** klasy, która będzie reprezentowała obiekty przechowywane w usłudze Azure DB rozwiązania Cosmos w tym przykładzie. Zostaną również utworzone podklasy **Parent**, **Child**, **Pet** i **Address**, które są używane w ramach klasy **Family**. Należy pamiętać, że dokumenty muszą mieć właściwość **Id** serializowaną jako **id** w formacie JSON. Utwórz te klasy, dodając następujące podklasy wewnętrzne po hello hello **GetStartedDemo** metody.

Skopiuj i Wklej hello **rodziny**, **nadrzędnej**, **podrzędnych**, **Pet**, i **adres** poniżej Witaj **WriteToConsoleAndPromptToContinue** metody.

```csharp
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
    Console.WriteLine(format, args);
    Console.WriteLine("Press any key toocontinue ...");
    Console.ReadKey();
}

// ADD THIS PART tooYOUR CODE
public class Family
{
    [JsonProperty(PropertyName = "id")]
    public string Id { get; set; }
    public string LastName { get; set; }
    public Parent[] Parents { get; set; }
    public Child[] Children { get; set; }
    public Address Address { get; set; }
    public bool IsRegistered { get; set; }
    public override string ToString()
    {
            return JsonConvert.SerializeObject(this);
    }
}

public class Parent
{
    public string FamilyName { get; set; }
    public string FirstName { get; set; }
}

public class Child
{
    public string FamilyName { get; set; }
    public string FirstName { get; set; }
    public string Gender { get; set; }
    public int Grade { get; set; }
    public Pet[] Pets { get; set; }
}

public class Pet
{
    public string GivenName { get; set; }
}

public class Address
{
    public string State { get; set; }
    public string County { get; set; }
    public string City { get; set; }
}
```

Skopiuj i Wklej hello **CreateFamilyDocumentIfNotExists** poniżej metody z **CreateDocumentCollectionIfNotExists** metody.

```csharp
// ADD THIS PART tooYOUR CODE
private async Task CreateFamilyDocumentIfNotExists(string databaseName, string collectionName, Family family)
{
    try
    {
        await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, family.Id));
        this.WriteToConsoleAndPromptToContinue("Found {0}", family.Id);
    }
    catch (DocumentClientException de)
    {
        if (de.StatusCode == HttpStatusCode.NotFound)
        {
            await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), family);
            this.WriteToConsoleAndPromptToContinue("Created Family {0}", family.Id);
        }
        else
        {
            throw;
        }
    }
}
```

I Wstaw dwa dokumenty, jeden dla rodziny Andersen hello i hello rodziny Wakefield.

Skopiuj i Wklej kod hello, który następuje `// ADD THIS PART tooYOUR CODE` tooyour **GetStartedDemo** poniżej tworzenia kolekcji dokumentów hello metody.

```csharp
await this.CreateDatabaseIfNotExists("FamilyDB_oa");

await this.CreateDocumentCollectionIfNotExists("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooYOUR CODE
Family andersenFamily = new Family
{
        Id = "Andersen.1",
        LastName = "Andersen",
        Parents = new Parent[]
        {
                new Parent { FirstName = "Thomas" },
                new Parent { FirstName = "Mary Kay" }
        },
        Children = new Child[]
        {
                new Child
                {
                        FirstName = "Henriette Thaulow",
                        Gender = "female",
                        Grade = 5,
                        Pets = new Pet[]
                        {
                                new Pet { GivenName = "Fluffy" }
                        }
                }
        },
        Address = new Address { State = "WA", County = "King", City = "Seattle" },
        IsRegistered = true
};

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", andersenFamily);

Family wakefieldFamily = new Family
{
        Id = "Wakefield.7",
        LastName = "Wakefield",
        Parents = new Parent[]
        {
                new Parent { FamilyName = "Wakefield", FirstName = "Robin" },
                new Parent { FamilyName = "Miller", FirstName = "Ben" }
        },
        Children = new Child[]
        {
                new Child
                {
                        FamilyName = "Merriam",
                        FirstName = "Jesse",
                        Gender = "female",
                        Grade = 8,
                        Pets = new Pet[]
                        {
                                new Pet { GivenName = "Goofy" },
                                new Pet { GivenName = "Shadow" }
                        }
                },
                new Child
                {
                        FamilyName = "Miller",
                        FirstName = "Lisa",
                        Gender = "female",
                        Grade = 1
                }
        },
        Address = new Address { State = "NY", County = "Manhattan", City = "NY" },
        IsRegistered = false
};

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);
```

Naciśnij klawisz hello **DocumentDBGettingStarted** przycisk toorun aplikacji.

Gratulacje! Pomyślnie utworzono dwa dokumenty usługi Azure Cosmos DB.  

![Diagram ilustrujący hello hierarchiczną relację między hello konta, baza danych online hello hello kolekcji i hello dokumentami używanymi przez hello toocreate samouczka NoSQL aplikacji konsolowej C#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a>Krok 7. Wykonanie zapytania względem zasobów usługi Azure Cosmos DB
Usługa Azure Cosmos DB obsługuje zaawansowane [zapytania](documentdb-sql-query.md) względem dokumentów JSON przechowywanych w każdej kolekcji.  Witaj następujący przykładowy kod przedstawia różne zapytania — przy użyciu obu Azure rozwiązania Cosmos bazy danych SQL składnię, a także LINQ — które można uruchomić względem hello dokumenty, które firma Microsoft wstawione w poprzednim kroku hello.

Skopiuj i Wklej hello **ExecuteSimpleQuery** poniżej metody z **CreateFamilyDocumentIfNotExists** metody.

```csharp
// ADD THIS PART tooYOUR CODE
private void ExecuteSimpleQuery(string databaseName, string collectionName)
{
    // Set some common query options
    FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

        // Here we find hello Andersen family via its LastName
        IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                .Where(f => f.LastName == "Andersen");

        // hello query is executed synchronously here, but can also be executed asynchronously via hello IDocumentQuery<T> interface
        Console.WriteLine("Running LINQ query...");
        foreach (Family family in familyQuery)
        {
            Console.WriteLine("\tRead {0}", family);
        }

        // Now execute hello same query via direct SQL
        IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                queryOptions);

        Console.WriteLine("Running direct SQL query...");
        foreach (Family family in familyQueryInSql)
        {
                Console.WriteLine("\tRead {0}", family);
        }

        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
}
```

Kopiuj i wklej następujący hello kodu tooyour **GetStartedDemo** poniżej tworzenia drugiego dokumentu hello metody.

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART tooYOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

Naciśnij klawisz hello **DocumentDBGettingStarted** przycisk toorun aplikacji.

Gratulacje! Pomyślnie wykonano zapytanie względem kolekcji usługi Azure Cosmos DB.

Witaj poniższym diagramie przedstawiono sposób hello Azure rozwiązania Cosmos DB kwerend SQL składni jest wywoływana względem kolekcji hello utworzony i hello sama logika dotyczy również zapytania LINQ toohello.

![Diagram pokazujący hello zakres i znaczenie zapytania hello używane przez toocreate samouczka NoSQL hello aplikacji konsolowej C#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

Witaj [FROM](documentdb-sql-query.md#FromClause) — słowo kluczowe jest opcjonalna w hello zapytania, ponieważ zapytania bazy danych Azure rozwiązania Cosmos jest już tooa zakresie jednej kolekcji. W związku z tym klauzula "FROM Families f" może być zamieniona na "FROM root r" lub dowolną inną wybraną nazwę zmiennej. Usługa DocumentDB wywnioskuje rodziny, root lub nazwę zmiennej hello wybrane, odwołanie do bieżącej kolekcji hello domyślnie.

## <a id="ReplaceDocument"></a>Krok 8. Zastępowanie dokumentu JSON
Usługa Azure Cosmos DB obsługuje zastępowanie dokumentów JSON.  

Skopiuj i Wklej hello **ReplaceFamilyDocument** poniżej metody z **ExecuteSimpleQuery** metody.

```csharp
// ADD THIS PART tooYOUR CODE
private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
{
    try
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
        this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

Kopiuj i wklej następujący hello kodu tooyour **GetStartedDemo** poniżej hello wykonywania zapytania. Po zastąpieniu dokumentu hello, spowoduje to uruchomienie hello sam ponowne przesłanie zapytania tooview hello zmieniony dokument.

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooYOUR CODE
// Update hello Grade of hello Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

Naciśnij klawisz hello **DocumentDBGettingStarted** przycisk toorun aplikacji.

Gratulacje! Pomyślnie zastąpiono dokument usługi Azure Cosmos DB.

## <a id="DeleteDocument"></a>Krok 9. Usuwanie dokumentu JSON
Usługa Azure Cosmos DB obsługuje usuwanie dokumentów JSON.  

Skopiuj i Wklej hello **DeleteFamilyDocument** poniżej metody z **ReplaceFamilyDocument** metody.

```csharp
// ADD THIS PART tooYOUR CODE
private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
{
    try
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
        Console.WriteLine("Deleted Family {0}", documentName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

Kopiuj i wklej następujący hello kodu tooyour **GetStartedDemo** poniżej hello drugiego wykonywania zapytania.

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooCODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

Naciśnij klawisz hello **DocumentDBGettingStarted** przycisk toorun aplikacji.

Gratulacje! Pomyślnie usunięto dokument usługi Azure Cosmos DB.

## <a id="DeleteDatabase"></a>Krok 10: Usuwanie hello bazy danych
Trwa usuwanie hello utworzył bazę danych spowoduje usunięcie hello bazy danych i wszystkich zasobów podrzędnych (kolekcji, dokumentów itd.).

Kopiuj i wklej następujący hello kodu tooyour **GetStartedDemo** poniżej dokumentu hello usunąć toodelete hello całą bazę danych i wszystkie zasoby podrzędne.

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART tooCODE
// Clean up/delete hello database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

Naciśnij klawisz hello **DocumentDBGettingStarted** przycisk toorun aplikacji.

Gratulacje! Pomyślnie usunięto bazę danych usługi Azure Cosmos DB.

## <a id="Run"></a>Krok 11. Uruchamianie całej aplikacji konsolowej C#
Naciśnij klawisz hello **DocumentDBGettingStarted** przycisk w aplikacji hello toobuild programu Visual Studio w trybie debugowania.

Powinny pojawić się dane wyjściowe aplikacji rozpoczynania pracy w oknie konsoli hello hello. Witaj dane wyjściowe będą pokazywały wyniki hello hello dodanych zapytań i powinny odpowiadać tekstowi przykładu hello poniżej.

```
Created FamilyDB_oa
Press any key toocontinue ...
Created FamilyCollection_oa
Press any key toocontinue ...
Created Family Andersen.1
Press any key toocontinue ...
Created Family Wakefield.7
Press any key toocontinue ...
Running LINQ query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Running direct SQL query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Replaced Family Andersen.1
Press any key toocontinue ...
Running LINQ query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Running direct SQL query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Deleted Family Andersen.1
End of demo, press any key tooexit.
```

Gratulacje! Po ukończeniu samouczka hello i mieć pracy aplikacji konsolowej C#!

## <a id="GetSolution"></a>Pobierz hello kompletnego rozwiązania samouczka
rozwiązania GetStarted hello toobuild, który zawiera wszystkie przykłady hello w tym artykule, będą potrzebne następujące hello:

* Aktywne konto platformy Azure. Jeśli go nie masz, możesz zarejestrować się w celu [utworzenia bezpłatnego konta](https://azure.microsoft.com/free/).
* [Konta bazy danych Azure rozwiązania Cosmos][create-documentdb-dotnet.md#create-account].
* Witaj [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) rozwiązanie jest dostępne w witrynie GitHub.

toorestore hello odwołania toohello interfejsu API usługi DocumentDB dla platformy Azure rozwiązania Cosmos DB .NET Core SDK w programie Visual Studio, kliknij prawym przyciskiem myszy hello **GetStarted** rozwiązania w Eksploratorze rozwiązań, a następnie kliknij przycisk **Włącz Przywracanie pakietu NuGet**. Następnie w pliku Program.cs hello, zaktualizuj wartości EndpointUrl i AuthorizationKey hello zgodnie z opisem w [połączyć konto bazy danych Azure rozwiązania Cosmos tooan](#Connect).

## <a name="next-steps"></a>Następne kroki
* Potrzebujesz bardziej złożonego samouczka platformy ASP.NET MVC? Zobacz [samouczek programu ASP.NET MVC: opracowywanie aplikacji z bazy danych Azure rozwiązania Cosmos sieci Web](documentdb-dotnet-application.md).
* Mają toodevelop Xamarin iOS, Android lub formularzy przy użyciu aplikacji hello interfejsu API usługi DocumentDB dla platformy Azure rozwiązania Cosmos DB .NET Core SDK? Zobacz [tworzenie aplikacji dla urządzeń przenośnych dzięki platformie Xamarin i usłudze Azure DB rozwiązania Cosmos](mobile-apps-with-xamarin.md).
* Chcesz testowanie z bazy danych Azure rozwiązania Cosmos wydajności i skalowania tooperform? Zobacz [wydajności i skalowania testowania z bazy danych Azure rozwiązania Cosmos](performance-testing.md)
* Dowiedz się, jak za[żądań, użycia i magazynu bazy danych rozwiązania Cosmos Azure Monitor](monitor-accounts.md).
* Uruchom zapytania względem naszego przykładowego zestawu danych w hello [Plac zabaw dla zapytań](https://www.documentdb.com/sql/demo).
* Zobacz toolearn więcej informacji na temat modelu programowania hello [bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/).

[create-documentdb-dotnet.md#create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-dotnetcore-get-started/nosql-tutorial-keys.png
