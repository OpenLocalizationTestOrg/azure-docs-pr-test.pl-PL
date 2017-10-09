---
title: "Azure Cosmos DB: rozpoczęcie pracy z interfejsem API usługi DocumentDB — samouczek | Microsoft Docs"
description: "Samouczek, który powoduje utworzenie bazy danych w trybie online i aplikacji konsolowej C# za pomocą hello interfejsu API usługi DocumentDB."
keywords: samouczek nosql, baza danych online, aplikacja konsolowa c#
services: cosmos-db
documentationcenter: .net
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: bf08e031-718a-4a2a-89d6-91e12ff8797d
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2017
ms.author: anhoh
ms.openlocfilehash: 65a181f715a670987492ad7815ef2ec94498e84d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-api-getting-started-tutorial"></a>Azure Cosmos DB: rozpoczęcie pracy z interfejsem API usługi DocumentDB — samouczek
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js dla MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Zapraszamy toohello interfejsu API Azure rozwiązania Cosmos bazy danych DocumentDB Samouczek wprowadzający! W ramach tego samouczka zostanie utworzona aplikacja konsolowa, która tworzy zasoby usługi Azure Cosmos DB i wykonuje dla nich zapytania.

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

Nie masz czasu? Nie martw się! Witaj kompletne rozwiązanie jest dostępne na [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started). Przeskocz toohello [pobrać pełną sekcji rozwiązania samouczka NoSQL hello](#GetSolution) Aby uzyskać krótkie instrukcje.

Później należy głosowania hello użyj przycisków na powitania góry lub u dołu tej strony toogive nam opinii. Jeśli chcesz nam toocontact bezpośrednio, uważasz, że tooinclude wolnego adresu e-mail w komentarzach.

Teraz do dzieła!

## <a name="prerequisites"></a>Wymagania wstępne
Upewnij się, że masz następujące hello:

* Aktywne konto platformy Azure. Jeśli go nie masz, możesz zarejestrować się w celu [utworzenia bezpłatnego konta](https://azure.microsoft.com/free/). 
    * Alternatywnie można użyć hello [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) w tym samouczku.
* [Visual Studio Community 2017](http://www.visualstudio.com/).

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Krok 1. Tworzenie konta usługi Azure Cosmos DB
Utwórzmy konto usługi Azure Cosmos DB. Jeśli masz już konto ma toouse, możesz przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS). Jeśli używasz hello Azure rozwiązania Cosmos DB emulatora, należy wykonać czynności hello na [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) toosetup hello emulatora i przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS).

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a>Krok 2. Konfigurowanie rozwiązania programu Visual Studio
1. Otwórz program **Visual Studio 2017** na komputerze.
2. Na powitania **pliku** menu, wybierz opcję **nowy**, a następnie wybierz pozycję **projektu**.
3. W hello **nowy projekt** okno dialogowe, wybierz opcję **szablony** / **Visual C#** / **aplikacji konsoli**, nazwa Projekt, a następnie kliknij przycisk **OK**.
   ![Zrzut ekranu okna nowy projekt hello](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)
4. W hello **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy nową aplikację konsolową, która znajduje się w obrębie rozwiązania Visual Studio, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...**
    
    ![Zrzut ekranu przedstawiający hello prawo kliknięto element Menu hello projektu](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. W hello **Nuget** , kliknij pozycję **Przeglądaj**i wpisz **usługa azure documentdb** hello pola wyszukiwania.
6. W wynikach hello znaleźć **Microsoft.Azure.DocumentDB** i kliknij przycisk **zainstalować**.
   Identyfikator pakietu Hello hello biblioteki klienta interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB jest [Biblioteka kliencka usługi Microsoft Azure DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).
   ![Zrzut ekranu przedstawiający hello Nuget Menu do znajdowania zestawu SDK klienta usługi Azure rozwiązania Cosmos bazy danych](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)

    Jeśli komunikaty o przegląd zmian toohello rozwiązania, kliknij przycisk **OK**. Jeśli wyświetlany jest komunikat o akceptacji licencji, kliknij pozycję **Akceptuję**.

Wspaniale! Teraz, gdy zakończeniu hello instalacji, Zacznijmy pisanie kodu. Ukończony projekt kodu z tego samouczka można znaleźć w witrynie [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).

## <a id="Connect"></a>Krok 3: Łączenie tooan konta bazy danych Azure rozwiązania Cosmos
Najpierw dodaj te odwołania toohello początku aplikacji C#, w pliku Program.cs hello:

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART tooYOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> W samouczku hello toocomplete kolejności upewnij się, że możesz dodać hello zależności powyżej.
> 
> 

Dodaj teraz te dwie stałe i zmienną *client* poniżej klasy publicznej *Program*.

    public class Program
    {
        // ADD THIS PART tooYOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

Następnie head kopii toohello [Azure Portal](https://portal.azure.com) tooretrieve Twojego adresu URL punktu końcowego i klucz podstawowy. adres URL punktu końcowego Hello i klucza podstawowego są niezbędne do Twojej aplikacji toounderstand gdzie tooconnect na oraz bazy danych Azure rozwiązania Cosmos tootrust połączeniu aplikacji.

W hello portalu Azure, przejdź do konta bazy danych Azure rozwiązania Cosmos tooyour, a następnie kliknij **klucze**.

Skopiuj hello identyfikatora URI z portalu hello i wklej ją do `<your endpoint URL>` w pliku program.cs hello. Następnie kopiowania hello klucza podstawowego z portalu hello i wklej ją do `<your primary key>`.

![Zrzut ekranu przedstawiający hello Portal Azure używany przez hello toocreate samouczka NoSQL aplikacji konsolowej C#. Pokazuje bazy danych Azure rozwiązania Cosmos konto, z wyróżnionym, AKTYWNYM Centrum hello hello przyciskiem KLUCZE wyróżnionym w bloku konta usługi Azure DB rozwiązania Cosmos hello i hello wartości identyfikatora URI, klucz podstawowy i klucz POMOCNICZY wyróżnionymi w hello bloku klucze][keys]

Następnie Zaczniemy aplikacji hello, tworząc nowe wystąpienie klasy hello **DocumentClient**.

Poniżej hello **Main** metody, dodaj to nowe zadanie asynchroniczne o nazwie **GetStartedDemo**, które zostaną nowe wystąpienie klasy **DocumentClient**.

    static void Main(string[] args)
    {
    }

    // ADD THIS PART tooYOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

Dodaj hello poniższy kod toorun zadania asynchronicznego z Twojej **Main** metody. Witaj **Main** metoda będzie przechwytywać wyjątki i zapisywać je toohello konsoli.

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

Naciśnij klawisz **F5** toorun aplikacji. dane wyjściowe z okna konsoli Hello wyświetla wiadomość hello `End of demo, press any key tooexit.` potwierdzenie, że nawiązano połączenie hello.  Następnie możesz zamknąć hello okna konsoli. 

Gratulacje! Pomyślnie nawiązano połączenie konto bazy danych Azure rozwiązania Cosmos tooan, teraz Spójrzmy w pracy z zasobami Azure DB rozwiązania Cosmos.  

## <a name="step-4-create-a-database"></a>Krok 4. Tworzenie bazy danych
Przed dodaniem hello kod służący do tworzenia bazy danych Dodaj metodę pomocnika na potrzeby zapisywania toohello konsoli.

Skopiuj i Wklej hello **WriteToConsoleAndPromptToContinue** metody po hello **GetStartedDemo** metody.

    // ADD THIS PART tooYOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

Bazy danych programu Azure rozwiązania Cosmos [bazy danych](documentdb-resources.md#databases) można tworzyć przy użyciu hello [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) metody hello **DocumentClient** klasy. Baza danych jest hello kontenerem logicznym magazynu dokumentów JSON podzielonym na partycje w kolekcjach.

Kopiuj i wklej następujący hello kodu tooyour **GetStartedDemo** metody utworzoną powitania klienta. Spowoduje to utworzenie bazy danych o nazwie *FamilyDB*.

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART tooYOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

Naciśnij klawisz **F5** toorun aplikacji.

Gratulacje! Pomyślnie utworzono bazę danych usługi Azure Cosmos DB.  

## <a id="CreateColl"></a>Krok 5. Tworzenie kolekcji
> [!WARNING]
> Za pomocą metody **CreateDocumentCollectionIfNotExistsAsync** zostanie utworzona nowa kolekcja z zarezerwowaną przepływnością, co ma wpływ na cenę. Aby uzyskać więcej informacji, odwiedź naszą [stronę cennika](https://azure.microsoft.com/pricing/details/cosmos-db/).
> 
> 

A [kolekcji](documentdb-resources.md#collections) można tworzyć przy użyciu hello [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) metody hello **DocumentClient** klasy. Kolekcja jest kontenerem dokumentów JSON i skojarzonej logiki aplikacji JavaScript.

Kopiuj i wklej następujący hello kodu tooyour **GetStartedDemo** metody po utworzeniu bazy danych hello. Spowoduje to utworzenie kolekcji dokumentów o nazwie *FamilyCollection*.

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART tooYOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

Naciśnij klawisz **F5** toorun aplikacji.

Gratulacje! Pomyślnie utworzono kolekcję dokumentów Azure Cosmos DB.  

## <a id="CreateDoc"></a>Krok 6. Tworzenie dokumentów JSON
A [dokumentu](documentdb-resources.md#documents) można tworzyć przy użyciu hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) metody hello **DocumentClient** klasy. Dokumenty są zawartością JSON zdefiniowaną przez użytkownika (dowolną). Można teraz wstawić jeden lub więcej dokumentów. Jeśli masz już dane, które chcesz toostore w bazie danych, możesz użyć hello Azure DB rozwiązania Cosmos [narzędzia migracji danych](import-data.md) tooimport hello danych do bazy danych.

Najpierw należy toocreate **rodziny** klasy, która będzie reprezentowała obiekty przechowywane w usłudze Azure DB rozwiązania Cosmos w tym przykładzie. Zostaną również utworzone podklasy **Parent**, **Child**, **Pet** i **Address**, które są używane w ramach klasy **Family**. Należy pamiętać, że dokumenty muszą mieć właściwość **Id** serializowaną jako **id** w formacie JSON. Utwórz te klasy, dodając następujące podklasy wewnętrzne po hello hello **GetStartedDemo** metody.

Skopiuj i Wklej hello **rodziny**, **nadrzędnej**, **podrzędnych**, **Pet**, i **adres** klasy po hello **WriteToConsoleAndPromptToContinue** metody.

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

Skopiuj i Wklej hello **CreateFamilyDocumentIfNotExists** poniżej metody z **adres** klasy.

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

I Wstaw dwa dokumenty, jeden dla rodziny Andersen hello i hello rodziny Wakefield.

Kopiuj i wklej następujący hello kodu tooyour **GetStartedDemo** metody po utworzeniu kolekcji dokumentów hello.

    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });
    
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });


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

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", andersenFamily);

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

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

Naciśnij klawisz **F5** toorun aplikacji.

Gratulacje! Pomyślnie utworzono dwa dokumenty usługi Azure Cosmos DB.  

![Diagram ilustrujący hello hierarchiczną relację między hello konta, baza danych online hello hello kolekcji i hello dokumentami używanymi przez hello toocreate samouczka NoSQL aplikacji konsolowej C#](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a>Krok 7. Wykonanie zapytania względem zasobów usługi Azure Cosmos DB
Usługa Azure Cosmos DB obsługuje zaawansowane [zapytania](documentdb-sql-query.md) względem dokumentów JSON przechowywanych w każdej kolekcji.  Witaj następujący przykładowy kod przedstawia różne zapytania — przy użyciu obu Azure rozwiązania Cosmos bazy danych SQL składnię, a także LINQ — które można uruchomić względem hello dokumenty, które firma Microsoft wstawione w poprzednim kroku hello.

Skopiuj i Wklej hello **ExecuteSimpleQuery** metody po Twoje **CreateFamilyDocumentIfNotExists** metody.

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

Kopiuj i wklej następujący hello kodu tooyour **GetStartedDemo** metody po tworzenia drugiego dokumentu hello.

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART tooYOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

Naciśnij klawisz **F5** toorun aplikacji.

Gratulacje! Pomyślnie wykonano zapytanie względem kolekcji usługi Azure Cosmos DB.

Witaj poniższym diagramie przedstawiono sposób hello Azure rozwiązania Cosmos DB kwerend SQL składni jest wywoływana względem kolekcji hello utworzony i hello sama logika dotyczy również zapytania LINQ toohello.

![Diagram pokazujący hello zakres i znaczenie zapytania hello używane przez toocreate samouczka NoSQL hello aplikacji konsolowej C#](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

Witaj [FROM](documentdb-sql-query.md#FromClause) — słowo kluczowe jest opcjonalna w hello zapytania, ponieważ zapytania bazy danych Azure rozwiązania Cosmos jest już tooa zakresie jednej kolekcji. W związku z tym klauzula "FROM Families f" może być zamieniona na "FROM root r" lub dowolną inną wybraną nazwę zmiennej. Azure DB rozwiązania Cosmos wywnioskuje rodziny, root lub nazwę zmiennej hello wybrane, odwołanie do bieżącej kolekcji hello domyślnie.

## <a id="ReplaceDocument"></a>Krok 8. Zastępowanie dokumentu JSON
Usługa Azure Cosmos DB obsługuje zastępowanie dokumentów JSON.  

Skopiuj i Wklej hello **ReplaceFamilyDocument** metody po Twoje **ExecuteSimpleQuery** metody.

    // ADD THIS PART tooYOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

Kopiuj i wklej następujący hello kodu tooyour **GetStartedDemo** metody po wykonaniu zapytania hello na końcu hello hello metody. Po zastąpieniu dokumentu hello, spowoduje to uruchomienie hello sam ponowne przesłanie zapytania tooview hello zmieniony dokument.

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART tooYOUR CODE
    // Update hello Grade of hello Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

Naciśnij klawisz **F5** toorun aplikacji.

Gratulacje! Pomyślnie zastąpiono dokument usługi Azure Cosmos DB.

## <a id="DeleteDocument"></a>Krok 9. Usuwanie dokumentu JSON
Usługa Azure Cosmos DB obsługuje usuwanie dokumentów JSON.  

Skopiuj i Wklej hello **DeleteFamilyDocument** metody po Twoje **ReplaceFamilyDocument** metody.

    // ADD THIS PART tooYOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

Kopiuj i wklej następujący hello kodu tooyour **GetStartedDemo** metody po hello drugiego wykonywania zapytania, na końcu hello hello metody.

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART tooCODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

Naciśnij klawisz **F5** toorun aplikacji.

Gratulacje! Pomyślnie usunięto dokument usługi Azure Cosmos DB.

## <a id="DeleteDatabase"></a>Krok 10: Usuwanie hello bazy danych
Trwa usuwanie hello utworzył bazę danych spowoduje usunięcie hello bazy danych i wszystkich zasobów podrzędnych (kolekcji, dokumentów itd.).

Kopiuj i wklej następujący hello kodu tooyour **GetStartedDemo** metody po dokumentu hello usunąć toodelete hello całą bazę danych i wszystkie zasoby podrzędne.

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART tooCODE
    // Clean up/delete hello database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

Naciśnij klawisz **F5** toorun aplikacji.

Gratulacje! Pomyślnie usunięto bazę danych usługi Azure Cosmos DB.

## <a id="Run"></a>Krok 11. Uruchamianie całej aplikacji konsolowej C#
Naciśnij klawisz F5 w programie Visual Studio toobuild hello aplikacji w trybie debugowania.

Powinny pojawić się hello dane wyjściowe aplikacji rozpoczynania pracy w oknie konsoli. Witaj dane wyjściowe będą pokazywały wyniki hello hello dodanych zapytań i powinny odpowiadać tekstowi przykładu hello poniżej.

    Created FamilyDB
    Press any key toocontinue ...
    Created FamilyCollection
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

Gratulacje! Po ukończeniu samouczka hello i mieć pracy aplikacji konsolowej C#!

## <a id="GetSolution"></a>Pobierz hello kompletnego rozwiązania samouczka
Jeśli nie masz czasu toocomplete hello kroków w tym samouczku lub po prostu chcesz toodownload hello przykłady kodu, możesz pobrać go z [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started). 

rozwiązania GetStarted hello toobuild, potrzebne są następujące hello:

* Aktywne konto platformy Azure. Jeśli go nie masz, możesz zarejestrować się w celu [utworzenia bezpłatnego konta](https://azure.microsoft.com/free/).
* [Konta bazy danych Azure rozwiązania Cosmos][cosmos-db-create-account].
* Witaj [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) rozwiązanie jest dostępne w witrynie GitHub.

toorestore hello odwołania toohello zestawu SDK .NET DB rozwiązania Cosmos Azure w programie Visual Studio, kliknij prawym przyciskiem myszy hello **GetStarted** rozwiązania w Eksploratorze rozwiązań, a następnie kliknij przycisk **Włącz Przywracanie pakietu NuGet**. Następnie w pliku App.config hello, zaktualizuj wartości EndpointUrl i AuthorizationKey hello zgodnie z opisem w [połączyć konto bazy danych Azure rozwiązania Cosmos tooan](#Connect).

To wszystko — skompiluj projekt i gotowe!


## <a name="next-steps"></a>Następne kroki
* Potrzebujesz bardziej złożonego samouczka platformy ASP.NET MVC? Zobacz [samouczek programu ASP.NET MVC: opracowywanie aplikacji z bazy danych Azure rozwiązania Cosmos sieci Web](documentdb-dotnet-application.md).
* Chcesz testowanie z bazy danych Azure rozwiązania Cosmos wydajności i skalowania tooperform? Zobacz [wydajności i skalowania testowania z bazy danych Azure rozwiązania Cosmos](performance-testing.md)
* Dowiedz się, jak za[monitorowanie żądań, użycia i magazynu bazy danych Azure rozwiązania Cosmos](monitor-accounts.md).
* Uruchom zapytania względem naszego przykładowego zestawu danych w hello [Plac zabaw dla zapytań](https://www.documentdb.com/sql/demo).
* toolearn więcej informacji na temat bazy danych rozwiązania Cosmos platformy Azure, zobacz [Witamy tooAzure DB rozwiązania Cosmos](https://docs.microsoft.com/azure/cosmos-db/introduction).

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-documentdb-dotnet.md#create-account
