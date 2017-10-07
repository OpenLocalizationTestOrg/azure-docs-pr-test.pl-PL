---
title: "Azure DB rozwiązania Cosmos: Opracowywania hello tabeli interfejs API .NET | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodevelop z interfejsem API tabeli DB rozwiązania Cosmos Azure przy użyciu platformy .NET"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 4b22cb49-8ea2-483d-bc95-1172cd009498
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: mvc
ms.openlocfilehash: 70c6985a1dffdbcdb07e377f8ad10355bb97712a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-table-api-in-net"></a>Azure DB rozwiązania Cosmos: Opracowywania hello tabeli interfejs API .NET

Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft. Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos.

Ten samouczek obejmuje hello następujące zadania: 

> [!div class="checklist"] 
> * Tworzenie konta usługi Azure Cosmos DB 
> * Włączanie funkcji w pliku app.config hello 
> * Utwórz tabelę przy użyciu hello [API tabeli](table-introduction.md) (wersja zapoznawcza)
> * Dodaj tabelę tooa jednostki 
> * Zbiorcze wstawianie jednostek 
> * Pobieranie pojedynczej jednostki 
> * Przy użyciu automatycznego indeksów pomocniczych podmiotów zapytania 
> * Zastępowanie jednostki 
> * Usuwanie jednostki 
> * Usuwanie tabeli
 
## <a name="tables-in-azure-cosmos-db"></a>Tabele Azure rozwiązania Cosmos bazy danych 

Azure DB rozwiązania Cosmos zapewnia hello [API tabeli](table-introduction.md) (wersja zapoznawcza) dla aplikacji, które muszą magazyn kluczy i wartości, z projektem bez schematu. [Magazyn tabel Azure](../storage/common/storage-introduction.md) zestawy SDK i interfejsów API REST mogą być używane toowork z bazy danych Azure rozwiązania Cosmos. Wymagania wysokiej przepływności, mogą używać bazy danych Azure rozwiązania Cosmos toocreate tabel. Usługa Azure Cosmos DB obsługuje tabele o zoptymalizowanej przepływności (nazywane nieformalnie „tabelami premium”), dostępne obecnie w publicznej wersji zapoznawczej. 

Można kontynuować toouse magazynu tabel Azure dla tabel z magazynu wysokiej i niższe wymagania przepływności. Azure DB rozwiązania Cosmos wprowadzi pomocy technicznej dla tabel zoptymalizowanych pod kątem pamięci masowej w przyszłej aktualizacji, i istniejących i nowych tabel Azure, konta magazynu będzie można bezproblemowo uaktualnić tooAzure DB rozwiązania Cosmos.

Jeśli obecnie używasz magazynu tabel Azure, uzyskasz następujące korzyści z wersji zapoznawczej "Tabela premium" hello hello:

- Gotowe [globalne dystrybucji](distribute-data-globally.md) z wielu i [automatycznej i ręcznej pracy awaryjnej.](regional-failover.md)
- Obsługa automatycznego schematu niezwiązane z żadnym indeksowania względem wszystkich właściwości ("indeksów pomocniczych") i szybkie zapytań 
- Obsługa [niezależne skalowanie pamięci masowej i przepływność](partition-data.md), przez dowolną liczbę regionów
- Obsługa [dedykowanych przepływności na tabelę](request-units.md) mogą być skalowane z setkami toomillions żądań na sekundę
- Obsługa [pięć dostosowywalne poziomy spójności](consistency-levels.md) tootrade poza dostępności, opóźnienia i spójności w oparciu wymagań aplikacji
- dostępność 99,99% w pojedynczym regionie i możliwości tooadd więcej regionów potrzeby wyższej dostępności i [SLA kompleksowe branży](https://azure.microsoft.com/support/legal/sla/cosmos-db/) w ogólnodostępnej
- Praca z istniejącego magazynu Azure hello zestawu .NET SDK i żadna aplikacja tooyour zmiany kodu

Witaj wersji zapoznawczej obsługuje bazy danych Azure rozwiązania Cosmos hello tabeli interfejsu API przy użyciu zestawu .NET SDK hello. Możesz pobrać hello [zestawu SDK w wersji zapoznawczej usługi Magazyn Azure](https://aka.ms/premiumtablenuget) z pakietu NuGet, która ma hello tej samej klasy i metody podpisy jako hello [zestawu SDK usługi Magazyn Azure](https://www.nuget.org/packages/WindowsAzure.Storage), ale także podłączyć tooAzure DB rozwiązania Cosmos kont przy użyciu hello Tabela interfejsu API.

toolearn więcej informacji na temat skomplikowanych zadaniach magazynu tabel Azure, zobacz:

* [Wprowadzenie tooAzure DB rozwiązania Cosmos: Tabela interfejsu API](table-introduction.md)
* Witaj dokumentację referencyjną usługi tabel, aby uzyskać szczegółowe informacje o dostępnych interfejsach API [biblioteki klienta usługi Storage dla platformy .NET odwołania](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)

### <a name="about-this-tutorial"></a>Informacje o tym samouczku
W tym samouczku jest dla deweloperów, którzy są zaznajomieni z programem hello magazynu tabel Azure SDK i chcesz toouse hello premium funkcje dostępne przy użyciu bazy danych Azure rozwiązania Cosmos. Jest on oparty na [Rozpoczynanie pracy z magazynem tabel Azure przy użyciu platformy .NET](table-storage-how-to-use-dotnet.md) i pokazuje, jak tootake korzystać z dodatkowych funkcji, takich jak indeksów pomocniczych, udostępnionej przepływności i wielu. Firma Microsoft opisano, jak toouse hello Azure toocreate portalu konta usługi Azure DB rozwiązania Cosmos, a następnie tworzenie i wdrażanie aplikacji tabeli. Przeprowadzenie możemy również przykłady .NET do tworzenia i usuwania tabeli, wstawianie, aktualizowanie, usuwanie i przeszukiwaniem danych w tabeli. 

Jeśli nie masz jeszcze programu Visual Studio 2017 r zainstalowany, możesz pobrać i użyć hello **wolnego** [programu Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/). Upewnij się, że możesz włączyć **Azure programowanie** podczas instalacji programu Visual Studio hello.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Tworzenie konta bazy danych

Zacznijmy od utworzenia konta Azure DB rozwiązania Cosmos w hello portalu Azure.  

> [!TIP]
> * Masz już konto bazy danych rozwiązania Cosmos Azure? Jeśli tak, przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS).
> * Czy miał konto usługi Azure DocumentDB? Jeśli tak, Twoje konto jest kontem bazy danych Azure rozwiązania Cosmos i możesz przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS).  
> * Jeśli używasz hello Azure rozwiązania Cosmos DB emulatora, należy wykonać czynności hello na [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) toosetup hello emulatora i przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS).
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting tooany location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-hello-sample-application"></a>Klonowanie hello przykładowej aplikacji

Teraz załóżmy sklonować aplikacji przez tabelę z serwisu github, Ustaw ciąg połączenia hello i uruchom go.

1. Otwórz okno terminala git, np. git bash, i `cd` tooa katalog roboczy.  

2. Hello uruchom następujące polecenie tooclone hello próbki repozytorium. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. Następnie otwórz plik rozwiązania hello w programie Visual Studio.

## <a name="update-your-connection-string"></a>Aktualizowanie parametrów połączenia

Teraz przejdź wstecz toohello Azure tooget portalu użytkownika informacje o parametrach połączenia i skopiuj go do aplikacji hello.

1. W hello [portalu Azure](http://portal.azure.com/), w Azure rozwiązania Cosmos DB konta, na powitania lewy pasek nawigacyjny kliknij **klucze**, a następnie kliknij przycisk **odczytu i zapisu kluczy**. Użyjesz przyciski Kopia hello po prawej stronie powitania ciąg hello ekranu toocopy hello połączenia w pliku app.config hello hello następnego kroku.

2. W programie Visual Studio Otwórz plik app.config hello. 

3. Skopiuj wartość identyfikatora URI z portalu hello (przy użyciu przycisku Kopiuj hello) i przydzielić mu hello wartość klucz konta hello w pliku app.config. Użyj nazwy konta hello utworzony wcześniej dla nazwy konta w pliku app.config.
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> toouse tę aplikację z magazynem tabel Azure standardowe, należy w ciągu połączenia hello toochange `app.config file`. Użyj nazwy konta hello jako nazwa tabeli konta i klucz jako klucz podstawowy magazyn Azure. <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-hello-app"></a>Tworzenie i wdrażanie aplikacji hello
1. W programie Visual Studio, kliknij prawym przyciskiem myszy projekt hello w **Eksploratora rozwiązań** , a następnie kliknij przycisk **Zarządzaj pakietami NuGet**. 

2. W hello NuGet **Przeglądaj** wpisz ***WindowsAzure.Storage PremiumTable***. Sprawdź **obejmują wersje wstępne**.

3. Wyniki hello zainstalować hello **WindowsAzure.Storage PremiumTable** i wybierz polecenie kompilacji w wersji zapoznawczej hello `0.0.1-preview`. Ta akcja instaluje pakiet magazynu tabel Azure hello oraz wszystkie zależności.

4. Kliknij polecenie CTRL + F5 toorun hello aplikacji. 

Teraz można wrócić do poprzedniej strony tooData Explorer i zobacz zapytania, modyfikowania i pracować z danymi w tej tabeli. 

> [!NOTE]
> toouse tę aplikację w emulatorze Azure rozwiązania Cosmos bazy danych, możesz po prostu wymagane w ciągu połączenia hello toochange `app.config file`. Użyj hello poniżej wartości dla emulatora. <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a>Możliwości platformy Azure DB rozwiązania Cosmos
Azure DB rozwiązania Cosmos obsługuje wiele funkcji, które nie są dostępne w hello magazynu tabel Azure interfejsu API. Witaj nową funkcję można włączyć za pomocą następujących hello `appSettings` wartości konfiguracji. Nie wprowadzeniu wszelkie nowe sygnatury przeciążenia toohello podglądu lub zestawu SDK usługi Magazyn Azure. Dzięki temu można tooconnect tooboth standard i premium tabel i pracy z innymi usługami Azure Storage, takich jak obiekty BLOB i kolejki. 


| Klucz | Opis |
| --- | --- |
| TableConnectionMode  | Azure DB rozwiązania Cosmos obsługuje dwa tryby łączności. W `Gateway` tryb, żądania są zawsze wykonywane toohello bazy danych Azure rozwiązania Cosmos bramy, który przekazuje on toohello odpowiednich danych partycji. W `Direct` tryb łączności powitania klienta pobiera mapowanie hello toopartitions tabel i żądań bezpośrednio przed partycji danych. Firma Microsoft zaleca `Direct`, hello domyślne.  |
| TableConnectionProtocol | Azure DB rozwiązania Cosmos obsługuje dwa protokoły połączenia - `Https` i `Tcp`. `Tcp`jest domyślną hello i zalecane, ponieważ jest bardziej lightweight. |
| TablePreferredLocations | Rozdzielaną przecinkami listę preferowanych (podłączonej do wielu sieci) lokalizacji odczytów. Każde konto bazy danych rozwiązania Cosmos Azure może być skojarzony z 1-30 + regionów. Każde wystąpienie klienta można określić podzbiór tych regionów hello preferowane aby odczyty małe opóźnienia. regiony Hello muszą nosić przy użyciu ich [wyświetlane nazwy](https://msdn.microsoft.com/library/azure/gg441293.aspx), na przykład `West US`. Zobacz też [wielu interfejsów API](tutorial-global-distribution-table.md).
| TableConsistencyLevel | Można kompromis między dostępności opóźnienia, spójność i wybierając pięć dobrze zdefiniowane poziomy spójności: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, i `Eventual`. Domyślnie jest `Session`. Wybór Hello poziomu spójności sprawia, że różnica znaczących wydajności w konfiguracji w przypadku. Zobacz [poziomy spójności](consistency-levels.md) szczegółowe informacje. |
| TableThroughput | Zarezerwowaną przepływnością dla tabeli hello wyrażona w jednostkach żądań (RU) na sekundę. Tabele pojedynczego może obsługiwać miliony 100s RU/s. Zobacz [jednostek żądania](request-units.md). Domyślnie`400` |
| TableIndexingPolicy | Spójne i automatyczne dodatkowej indeksowania wszystkie kolumny w tabeli | JSON ciąg zgodnych toohello indeksowania specyfikacji zasad. Zobacz [zasady indeksowania](indexing-policies.md) toosee sposób zmiany indeksowania zasad tooinclude/wykluczania określonych kolumn. | Automatyczne indeksowanie wszystkich właściwości (skrót ciągi), a zakres numerów |
| TableQueryMaxItemCount | Skonfiguruj maksymalną liczbę elementów zwróconych dla tabeli kwerendy w jednym cyklu hello. Domyślnie jest `-1`, który umożliwia Azure DB rozwiązania Cosmos dynamiczne określanie wartości hello w czasie wykonywania. |
| TableQueryEnableScan | Jeśli zapytanie hello nie można użyć hello indeksu dla dowolny filtr, uruchom ją mimo to za pomocą skanowania. Domyślnie jest `false`.|
| TableQueryMaxDegreeOfParallelism | Witaj stopień równoległości do wykonania zapytania różnych partycji. `0`jest szeregowe z nie pobierania, `1` jest szeregowe z pobierania i wyższe wartości wzrostu hello stopień równoległości. Domyślnie jest `-1`, który umożliwia Azure DB rozwiązania Cosmos dynamiczne określanie wartości hello w czasie wykonywania. |

Wartość domyślna hello toochange, otwórz hello `app.config` plików w Eksploratorze rozwiązań w programie Visual Studio. Dodaj zawartość hello hello `<appSettings>` widocznego poniżej. Zastąp `account-name` hello nazwą konta magazynu i `account-key` kluczem dostępu do konta. 

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
      <!-- Client options -->
      <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key; TableEndpoint=https://account-name.documents.azure.com" />
      <add key="TableConnectionMode" value="Direct"/>
      <add key="TableConnectionProtocol" value="Tcp"/>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>
      <add key="TableConsistencyLevel" value="Eventual"/>

      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
      <add key="TableIndexingPolicy" value="{""indexingMode"": ""Consistent""}"/>

      <!-- Table query options -->
      <add key="TableQueryMaxItemCount" value="-1"/>
      <add key="TableQueryEnableScan" value="false"/>
      <add key="TableQueryMaxDegreeOfParallelism" value="-1"/>
      <add key="TableQueryContinuationTokenLimitInKb" value="16"/>
            
    </appSettings>
</configuration>
```

Upewnijmy szybki przegląd działania wykonywane w aplikacji hello. Otwórz hello `Program.cs` plików i można znaleźć, te wiersze kodu utworzyć hello tabeli zasobów. 

## <a name="create-hello-table-client"></a>Utwórz powitania klienta tabeli
Możesz zainicjować `CloudTableClient` tooconnect toohello tabeli konta.

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
Ten klient został zainicjowany przy użyciu hello `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, i `TablePreferredLocations` wartości konfiguracji, jeśli określony w ustawieniach aplikacji hello.
    
## <a name="create-a-table"></a>Tworzenie tabeli
Następnie można utworzyć tabeli za pomocą `CloudTable`. Tabele w bazie danych rozwiązania Cosmos Azure mogą być skalowane niezależnie pod względem pamięci masowej i przepływność i podziału na partycje odbywa się automatycznie przez usługę hello. Azure DB rozwiązania Cosmos obsługuje zarówno o stałym rozmiarze i nieograniczoną liczbę tabel. Zobacz [partycjonowania w usłudze Azure DB rozwiązania Cosmos](partition-data.md) szczegółowe informacje. 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

Brak istotną różnicą w sposób tworzenia tabel. Azure DB rozwiązania Cosmos rezerwuje przepływności, w przeciwieństwie do magazynu Azure na podstawie zużycia modelu dla transakcji. model rezerwacji Hello ma dwie kluczowe korzyści:

* Przepustowość sieci jest w wersji dedykowanej/zarezerwowana, więc można nigdy nie pobrać ograniczany Jeśli częstotliwość żądania jest poziomie lub poniżej z udostępnionej przepływności
* model rezerwacji Hello jest więcej [ekonomiczne w przypadku obciążeń intensywnie przepływności](key-value-store-cost.md)

Można skonfigurować przepływności domyślne hello przez skonfigurowanie ustawienia hello dla `TableThroughput` pod względem RU (jednostki żądania) na sekundę. 

Odczyt jednostki 1 KB jest znormalizowany jako 1 RU i inne operacje są znormalizowane tooa stałej wartości RU oparte na ich użycie procesora CPU, pamięci i IOPS. Dowiedz się więcej o [jednostek w usłudze Azure DB rozwiązania Cosmos żądania](request-units.md).

> [!NOTE]
> Podczas gdy magazyn tabel zestawu SDK nie obsługuje obecnie modyfikowanie przepływności, można zmienić przepływności hello natychmiast w dowolnym momencie przy użyciu hello portalu Azure lub interfejsu wiersza polecenia platformy Azure.

Następnie możemy przeprowadzenie odczytu prostego powitania i zapisu (CRUD) przy użyciu magazynu tabel Azure hello zestawu SDK. W tym samouczku przedstawiono przewidywalną niski milisekund jednocyfrowej opóźnienia i szybkie zapytania pochodzącymi z bazy danych Azure rozwiązania Cosmos.

## <a name="add-an-entity-tooa-table"></a>Dodaj tabelę tooa jednostki
Jednostki w magazynie tabel Azure rozszerza z hello `TableEntity` klasy i musi mieć `PartitionKey` i `RowKey` właściwości. Oto przykład definicji jednostki klienta.

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

powitania po fragment kodu przedstawia, jak tooinsert jednostki z hello magazynu Azure SDK. Azure DB rozwiązania Cosmos jest przeznaczona dla gwarantowane małe opóźnienia w dowolnej skali między hello world.

Ukończenie operacji zapisu < 15 ms p99 i ms ~ 6 w p50 aplikacji uruchomionych na hello tego samego regionu hello konta bazy danych Azure rozwiązania Cosmos. I ten czas trwania kont faktu hello, który zapisuje są wstecz toohello klienta dopiero po ich są synchronicznie replikowane, trwale zatwierdzone, i całą jego zawartość jest indeksowana.

Witaj API tabeli dla bazy danych Azure rozwiązania Cosmos jest w wersji zapoznawczej. Ogólnie gwarancje opóźnienia p99 hello bazują na umów SLA, takich jak innych interfejsów API Azure rozwiązania Cosmos bazy danych. 

```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a>Zbiorcze wstawianie jednostek
Azure tabeli magazynu obsługuje interfejs API operacji partii, który umożliwia łączenie aktualizowanie i usuwanie, i wstawia w hello tego samego pojedynczej operacji zbiorczej. Azure DB rozwiązania Cosmos nie ma niektórych ograniczeń hello na interfejsu API partii hello jako magazynu tabel Azure. Na przykład można wykonywać wielu odczytów w partii, można wykonywać wiele toohello zapisy tej samej jednostki w partii, a nie ma żadnego limitu na 100 operacje na partię. 

```csharp
// Create hello batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it toohello table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it toohello table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities toohello batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute hello batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a>Pobieranie pojedynczej jednostki
Pobiera (pobiera) w usłudze Azure DB rozwiązania Cosmos pełną < 10 ms p99 i ~ 1 ms na p50 w hello tego samego regionu systemu Azure. Dodaj tyle konta tooyour regiony dla odczytów małe opóźnienia i wdrożyć aplikacje tooread z ich lokalnego regionu ("wieloadresowej") przez ustawienie `TablePreferredLocations`. 

Można pobrać pojedynczą jednostką przy użyciu następującego fragmentu hello:

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> Dowiedz się więcej o wielu interfejsów API w [programowania z użyciem wielu regionów](tutorial-global-distribution-table.md)
>

## <a name="query-entities-using-automatic-secondary-indexes"></a>Przy użyciu automatycznego indeksów pomocniczych podmiotów zapytania
Tabele mogą być przeszukiwane przy użyciu hello `TableQuery` klasy. Azure DB rozwiązania Cosmos ma aparat zoptymalizowanych pod kątem zapisu bazy danych, który automatycznie indeksuje wszystkie kolumny w tabeli. Indeksowanie w usłudze Azure DB rozwiązania Cosmos jest niezależny tooschema. W związku z tym nawet jeśli schemat różni się od wierszy lub schematu hello rozwoju wraz z upływem czasu, jest automatycznie indeksowane. Ponieważ bazy danych rozwiązania Cosmos Azure obsługuje automatyczne indeksów pomocniczych, zapytań dotyczących dowolnej właściwości można użyć indeksu hello i obsłużona wydajnie.

```csharp
CloudTable table = tableClient.GetTableReference("people");

// Filter against a property that's not partition key or row key
TableQuery<CustomerEntity> emailQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.GenerateFilterCondition("Email", QueryComparisons.Equal, "Ben@contoso.com"));

foreach (CustomerEntity entity in table.ExecuteQuery(emailQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

Podgląd bazy danych rozwiązania Cosmos Azure obsługuje hello zapytania takie same funkcje co magazyn tabel Azure dla hello tabeli interfejsu API. Azure DB rozwiązania Cosmos obsługuje również sortowanie, agregacje, dane geograficzne zapytania hierarchii i szeroki zakres funkcji wbudowanych. dodatkowe funkcje Hello zostanie podany w hello tabeli interfejsu API w przyszłej aktualizacji. Zobacz [kwerendy bazy danych Azure rozwiązania Cosmos](documentdb-sql-query.md) omówienie tych funkcji. 

## <a name="replace-an-entity"></a>Zastępowanie jednostki
tooupdate jednostki, pobrać hello usługi tabel, zmodyfikuj obiekt jednostki hello i następnie zapisz zmiany hello ponownie toohello usługi tabel. Witaj poniższy kod zmienia numer telefonu istniejącego klienta. 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
Podobnie można wykonywać `InsertOrMerge` lub `Merge` operacji.  

## <a name="delete-an-entity"></a>Usuwanie jednostki
Można z łatwością usunąć jednostkę po jej pobraniu przy użyciu hello tego samego wzorca co w przypadku aktualizowania jednostki. powitania po kod umożliwia pobranie i usunięcie jednostki klienta.

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a>Usuwanie tabeli
Na koniec hello poniższy przykład kodu usuwa tabelę z konta magazynu. Możesz usunąć i ponownie utwórz tabelę bezpośrednio z bazy danych Azure rozwiązania Cosmos.

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a>Oczyszczanie zasobów 

Jeśli nie będzie toocontinue toouse tej aplikacji, użyj hello następujące kroki toodelete wszystkie zasoby są tworzone w tym samouczku w hello portalu Azure.   

1. Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello zasobu hello został utworzony.  
2. Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**. 

## <a name="next-steps"></a>Następne kroki

W tym samouczku objętych firma Microsoft, jak tooget uruchamiane przy użyciu bazy danych Azure rozwiązania Cosmos z hello tabeli interfejsu API i wykonaniu następujących hello: 

> [!div class="checklist"] 
> * Utworzone konto bazy danych Azure rozwiązania Cosmos 
> * Funkcje włączone w pliku app.config hello 
> * Utworzyć tabelę 
> * Dodano tabelę tooa jednostki 
> * Wstawić partię jednostek 
> * Pobrać pojedynczą jednostką 
> * Jednostki, którego dotyczy kwerenda przy użyciu automatycznego indeksów pomocniczych 
> * Zastąpione jednostki 
> * Usunięte jednostki 
> * Usunięto tabelę  

Można teraz kontynuować toohello następny samouczek i Dowiedz się więcej o przeszukiwaniem danych w tabeli. 

> [!div class="nextstepaction"]
> [Zapytanie z hello tabeli interfejsu API](tutorial-query-table.md)
