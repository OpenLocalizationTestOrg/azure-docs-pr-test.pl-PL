---
title: "aaaGet wprowadzenie do magazynu tabel platformy Azure i programu Visual Studio połączone usługi (ASP.NET) | Dokumentacja firmy Microsoft"
description: "Jak tooget uruchamiane przy użyciu magazynu tabel platformy Azure w projekcie platformy ASP.NET w programie Visual Studio po połączeniu tooa konto magazynu przy użyciu programu Visual Studio usługami"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: af81a326-18f4-4449-bc0d-e96fba27c1f8
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: kraigb
ms.openlocfilehash: 04f79db7aad60ca51c3c866da1f4b01d9e11ac52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a>Rozpoczynanie pracy z magazynu tabel platformy Azure i programu Visual Studio połączone usługi (ASP.NET)
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Omówienie

Magazyn tabel Azure umożliwia toostore dużych ilości danych strukturalnych. Usługa Hello jest magazynem danych NoSQL, który przyjmuje uwierzytelnione wywołania z wewnątrz, jak i poza hello chmury Azure. Tabele Azure idealnie nadają się do przechowywania strukturalnych danych nierelacyjnych.

Ten samouczek pokazuje, jak kod toowrite ASP.NET dla niektórych typowych scenariuszy przy użyciu jednostek magazynu tabel Azure. Te scenariusze obejmują tworzenie tabeli i dodanie, wyszukiwanie i usuwania jednostek tabeli. 

##<a name="prerequisites"></a>Wymagania wstępne

* [Program Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Konto usługi Azure Storage](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>Tworzenie kontrolera MVC 

1. W hello **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **kontrolerów**i wybierz z menu kontekstowego hello **kontrolera -> Dodaj**.

    ![Dodaj tooan kontrolera aplikacji ASP.NET MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. Na powitania **Dodawanie szkieletu** okno dialogowe, wybierz opcję **kontroler MVC 5 — pusty**i wybierz **Dodaj**.

    ![Określ typ kontrolera MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. Na powitania **Dodaj kontroler** okno dialogowe, nazwy kontrolera hello *TablesController*i wybierz **Dodaj**.

    ![Kontroler MVC hello nazwy](./media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. Dodaj następujące hello *przy użyciu* toohello dyrektywy `TablesController.cs` pliku:

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a>Utwórz klasę modelu

Wiele hello przykłady w tym artykule użyj **TableEntity**-klasy o nazwie **CustomerEntity**. następujące kroki Hello informacje pomocne przy deklarowanie tę klasę jako klasę modelu:

1. W hello **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **modele**i wybierz z menu kontekstowego hello **klasy -> Dodaj**.

1. Na powitania **Dodaj nowy element** okno dialogowe, nazwa klasy hello, **CustomerEntity**.

1. Otwórz hello `CustomerEntity.cs` pliku, a następnie dodaj poniższe hello **przy użyciu** dyrektywy:

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. Zmodyfikuj hello klasy, tak, aby po zakończeniu klasy hello jest zadeklarowana tak jak hello następującego kodu. Klasa Hello deklaruje klasy jednostki o nazwie **CustomerEntity** imienia klienta jako hello klucz wiersza i nazwiska jako klucza partycji hello tekst hello zastosowań.

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
    }
    ```

## <a name="create-a-table"></a>Tworzenie tabeli

Witaj poniższe kroki przedstawiają sposób toocreate tabeli:

> [!NOTE]
> 
> W tej sekcji założono zostały wykonane kroki hello w [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment). 

1. Otwórz hello `TablesController.cs` pliku.

1. Dodaj metodę o nazwie **CreateTable** zwracającą **ActionResult**.

    ```csharp
    public ActionResult CreateTable()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. W ramach hello **CreateTable** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu. Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Pobierz **CloudTableClient** obiekt reprezentuje klienta usługi tabel.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Pobierz **CloudTable** obiekt, który reprezentuje nazwę odwołania toohello żądanej tabeli. Witaj **CloudTableClient.GetTableReference** — metoda nie powoduje żądanie magazyn tabel. czy istnieje tabela hello, zwracane jest odwołanie Hello. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Wywołaj hello **CloudTable.CreateIfNotExists** metody toocreate hello tabeli, jeśli jeszcze nie istnieje. Witaj **CloudTable.CreateIfNotExists** metoda zwraca **true** Jeśli hello tabela nie istnieje i został utworzony pomyślnie. W przeciwnym razie **false** jest zwracany.    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. Aktualizacja hello **obiekt ViewBag** o nazwie hello hello tabeli.

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **tabel**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.

1. Na powitania **Dodaj widok** okna dialogowego, wprowadź **CreateTable** hello nazwy widoku i wybierz **Dodaj**.

1. Otwórz `CreateTable.cshtml`i zmodyfikuj go, aby wygląda hello następującego fragmentu kodu:

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.

1. Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. Uruchamianie aplikacji hello, a następnie wybierz **Utwórz tabelę** toosee wyniki podobne toohello po zrzut ekranu:
  
    ![Tworzenie tabeli](./media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    Jak wspomniano wcześniej, hello **CloudTable.CreateIfNotExists** metoda zwraca **true** tylko po tabeli hello nie istnieje i zostanie utworzony. W związku z tym po uruchomieniu aplikacji hello podczas hello tabela istnieje, metoda hello zwraca **false**. Aplikacja hello toorun wielokrotnie, należy usunąć tabeli hello przed ponownym uruchomieniem aplikacji hello. Usuwanie tabeli hello może odbywać się za pośrednictwem hello **CloudTable.Delete** metody. Możesz także usunąć za pomocą hello tabeli hello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) lub hello [Eksploratora usługi Microsoft Azure Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md).  

## <a name="add-an-entity-tooa-table"></a>Dodaj tabelę tooa jednostki

*Jednostki* mapy tooC\# obiektów przy użyciu niestandardowej klasy pochodzące z **TableEntity**. tooadd tabeli tooa jednostki, Utwórz klasę, która definiuje właściwości hello jednostki. W tej sekcji zobaczysz, jak toodefine klasę jednostki, która używa hello imienia klienta jako hello klucz wiersza i nazwiska jako klucza partycji hello. Razem klucz partycji i klucz wiersza jednoznacznie zidentyfikować hello jednostki w tabeli hello. Jednostki z tym samym kluczem partycji mogą być przeszukiwane szybciej niż jednostki o różnych kluczach partycji, niemniej użycie różnych kluczy partycji umożliwia zwiększenie skalowalności operacji równoległych. Dla właściwości, które mają być przechowywane w usłudze tabel hello właściwość hello musi być właściwością publiczną obsługiwanego typu, która ujawnia zarówno ustawiania i pobierania wartości.
Witaj klasy jednostka *musi* zadeklarować publicznego konstruktora bez parametrów.

> [!NOTE]
> 
> W tej sekcji założono zostały wykonane kroki hello w [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment).

1. Otwórz hello `TablesController.cs` pliku.

1. Dodaj następujące dyrektywy, które hello kodu w hello hello `TablesController.cs` pliku mogą uzyskiwać dostęp do hello **CustomerEntity** klasy:

    ```csharp
    using StorageAspnet.Models;
    ```

1. Dodaj metodę o nazwie **AddEntity** zwracającą **ActionResult**.

    ```csharp
    public ActionResult AddEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. W ramach hello **AddEntity** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu. Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Pobierz **CloudTableClient** obiekt reprezentuje klienta usługi tabel.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Pobierz **CloudTable** obiekt, który reprezentuje toowhich tabeli toohello odwołanie ma tooadd hello nowej jednostki. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Utwórz wystąpienie i zainicjować hello **CustomerEntity** klasy.

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. Utwórz **TableOperation** obiekt, który wstawia powitania klienta jednostki.

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. Wykonanie operacji wstawiania hello przez wywołanie hello **CloudTable.Execute** metody. Sprawdź hello wynik operacji hello, sprawdzając hello **TableResult.HttpStatusCode** właściwości. Kod stanu 2xx wskazuje, że akcja hello żądany przez klienta na powitania zostało przetworzone pomyślnie. Na przykład pomyślnie wstawienia nowych jednostek powoduje kod stanu HTTP 204, co oznacza, że pomyślnie przetworzono hello operacji i powitania serwera nie zwróciło żadnej zawartości.

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. Aktualizacja hello **obiekt ViewBag** o nazwie tabeli hello i hello wyniki operacji insert hello.

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **tabel**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.

1. Na powitania **Dodaj widok** okna dialogowego, wprowadź **AddEntity** hello nazwy widoku i wybierz **Dodaj**.

1. Otwórz `AddEntity.cshtml`i zmodyfikuj go, aby wygląda hello następującego fragmentu kodu:

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.

1. Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. Uruchamianie aplikacji hello, a następnie wybierz **dodania jednostki** toosee wyniki podobne toohello po zrzut ekranu:
  
    ![Dodawanie jednostki](./media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    Możesz sprawdzić, czy jednostki hello został dodany, wykonując kroki hello w sekcji hello [pobrać pojedynczą jednostką](#get-a-single-entity). Można również użyć hello [Eksploratora usługi Microsoft Azure Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview hello wszystkie jednostki dla tabel.

## <a name="add-a-batch-of-entities-tooa-table"></a>Dodaj partii jednostek tooa tabeli

W stanie toobeing dodanie zbyt[Dodaj tabelę tooa jednostki, co w czasie](#add-an-entity-to-a-table), możesz także dodać jednostek w partii. Dodawanie jednostek w partii zmniejsza hello częstotliwości przechodzenia między kod i hello usługi tabeli platformy Azure. Hello następujące kroki ilustrują sposób tooadd wiele jednostek tooa tabeli z operacją insert pojedynczego:

> [!NOTE]
> 
> W tej sekcji założono zostały wykonane kroki hello w [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment).

1. Otwórz hello `TablesController.cs` pliku.

1. Dodaj metodę o nazwie **AddEntities** zwracającą **ActionResult**.

    ```csharp
    public ActionResult AddEntities()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. W ramach hello **AddEntities** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu. Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Pobierz **CloudTableClient** obiekt reprezentuje klienta usługi tabel.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Pobierz **CloudTable** obiekt, który reprezentuje toowhich tabeli toohello odwołania są będzie tooadd hello nowych jednostek. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Utworzenie wystąpienia niektórych obiektów klienta oparte na powitania **CustomerEntity** klasa przedstawione w sekcji hello modelu [Dodaj tabelę tooa jednostki](#add-an-entity-to-a-table).

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. Pobierz **TableBatchOperation** obiektu.

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. Dodaj obiekt operacji wstawiania wsadowego toohello jednostek.

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. Wykonanie operacji wstawiania wsadowego hello przez wywołanie hello **CloudTable.ExecuteBatch** metody.   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. Witaj **CloudTable.ExecuteBatch** metoda zwraca listę **TableResult** obiektów gdzie każdy **TableResult** obiekt może być sprawdzone toodetermine hello powodzenie lub niepowodzenie poszczególnych działań. Na przykład przekazać widoku tooa listy hello i pozwól widoku hello wyświetlać wyniki hello każdej operacji. 
 
    ```csharp
    return View(results);
    ```

1. W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **tabel**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.

1. Na powitania **Dodaj widok** okna dialogowego, wprowadź **AddEntities** hello nazwy widoku i wybierz **Dodaj**.

1. Otwórz `AddEntities.cshtml`i zmodyfikuj go, aby wygląda jak poniżej hello.

    ```csharp
    @model IEnumerable<Microsoft.WindowsAzure.Storage.Table.TableResult>
    @{
        ViewBag.Title = "AddEntities";
    }
    
    <h2>Add-entities results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>HTTP result</th>
        </tr>
        @foreach (var result in Model)
        {
        <tr>
            <td>@((result.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((result.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@result.HttpStatusCode</td>
        </tr>
        }
    </table>
    ```

1. W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.

1. Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. Uruchamianie aplikacji hello, a następnie wybierz **Dodaj jednostki** toosee wyniki podobne toohello po zrzut ekranu:
  
    ![Dodawanie jednostek](./media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    Możesz sprawdzić, czy jednostki hello został dodany, wykonując kroki hello w sekcji hello [pobrać pojedynczą jednostką](#get-a-single-entity). Można również użyć hello [Eksploratora usługi Microsoft Azure Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview hello wszystkie jednostki dla tabel.

## <a name="get-a-single-entity"></a>Pobierz pojedynczy element

W tej części przedstawiono, jak tooget pojedyncza jednostka z tabeli za pomocą hello klucz wiersza jednostki i klucz partycji. 

> [!NOTE]
> 
> W tej sekcji założono zostały wykonane kroki hello w [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment)i korzysta z danych [dodać partii jednostek tooa tabeli](#add-a-batch-of-entities-to-a-table). 

1. Otwórz hello `TablesController.cs` pliku.

1. Dodaj metodę o nazwie **GetSingle** zwracającą **ActionResult**.

    ```csharp
    public ActionResult GetSingle()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. W ramach hello **GetSingle** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu. Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Pobierz **CloudTableClient** obiekt reprezentuje klienta usługi tabel.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Pobierz **CloudTable** obiekt, który reprezentuje tabelę toohello odwołanie, z którego są pobierane hello jednostki. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Utwórz obiekt operacji pobierania, który przyjmuje do obiektu jednostki pochodne **TableEntity**. pierwszy parametr Hello jest hello *partitionKey*, a drugi parametr hello jest hello *rowKey*. Przy użyciu hello **CustomerEntity** klasy i dane podane w sekcji hello [dodać partii jednostek tabeli tooa](#add-a-batch-of-entities-to-a-table), hello następujący kod fragment zapytania hello tabeli **CustomerEntity** jednostki o *partitionKey* wartość "Smith" i *rowKey* wartość "Ben":

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. Wykonanie operacji pobierania hello.   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. Przekaż hello widok toohello wyników do wyświetlenia.

    ```csharp
    return View(result);
    ```

1. W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **tabel**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.

1. Na powitania **Dodaj widok** okna dialogowego, wprowadź **GetSingle** hello nazwy widoku i wybierz **Dodaj**.

1. Otwórz `GetSingle.cshtml`i zmodyfikuj go, aby wygląda hello następującego fragmentu kodu:

    ```csharp
    @model Microsoft.WindowsAzure.Storage.Table.TableResult
    @{
        ViewBag.Title = "GetSingle";
    }
    
    <h2>Get Single results</h2>
    
    <table border="1">
        <tr>
            <th>HTTP result</th>
            <th>First name</th>
            <th>Last name</th>
            <th>Email</th>
        </tr>
        <tr>
            <td>@Model.HttpStatusCode</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).Email)</td>
        </tr>
    </table>
    ```

1. W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.

1. Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. Uruchamianie aplikacji hello, a następnie wybierz **Pobierz pojedynczy** toosee wyniki podobne toohello po zrzut ekranu:
  
    ![Pobierz pojedynczy](./media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a>Pobieranie wszystkich jednostek w partycji

Jak wspomniano w sekcji hello [Dodaj tabelę tooa jednostki](#add-an-entity-to-a-table), kombinację hello partycji i klucz wiersza jednoznacznie identyfikują jednostkę w tabeli. Jednostki z tym samym kluczem partycji mogą być przeszukiwane szybciej niż jednostki o różnych kluczach partycji. W tej części przedstawiono sposób tooquery tabeli dla wszystkich jednostek hello z określonej partycji.  

> [!NOTE]
> 
> W tej sekcji założono zostały wykonane kroki hello w [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment)i korzysta z danych [dodać partii jednostek tooa tabeli](#add-a-batch-of-entities-to-a-table). 

1. Otwórz hello `TablesController.cs` pliku.

1. Dodaj metodę o nazwie **GetPartition** zwracającą **ActionResult**.

    ```csharp
    public ActionResult GetPartition()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. W ramach hello **GetPartition** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu. Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Pobierz **CloudTableClient** obiekt reprezentuje klienta usługi tabel.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Pobierz **CloudTable** obiekt, który reprezentuje tabeli toohello odwołań, z którego są pobierane hello jednostek. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Utwórz wystąpienie **TableQuery** obiektu określenie hello zapytania w hello **gdzie** klauzuli. Przy użyciu hello **CustomerEntity** klasy i dane podane w sekcji hello [dodać partii jednostek tabeli tooa](#add-a-batch-of-entities-to-a-table), hello poniższy kod fragment zapytania hello tabeli dla wszystkich jednostek, gdzie hello  **PartitionKey** (nazwiska) ma wartość "Smith":

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. W pętli, wywołaj hello **CloudTable.ExecuteQuerySegmented** metoda przekazywania można utworzyć wystąpienia obiektu query hello hello poprzedniego kroku.  Hello **CloudTable.ExecuteQuerySegmented** metoda zwraca **TableContinuationToken** obiekt – podczas **null** — wskazuje, że nie ma żadnych kolejnych jednostek tooretrieve. W pętli hello należy użyć innego tooiterate pętli za pośrednictwem hello zwracane jednostki. W hello poniższy przykład kodu każdy zwrócony obiekt jest dodawany tooa listy. Raz hello kończy pętlę, hello listy jest przekazywany tooa widoku do wyświetlenia: 

    ```csharp
    List<CustomerEntity> customers = new List<CustomerEntity>();
    TableContinuationToken token = null;
    do
    {
        TableQuerySegment<CustomerEntity> resultSegment = table.ExecuteQuerySegmented(query, token);
        token = resultSegment.ContinuationToken;

        foreach (CustomerEntity customer in resultSegment.Results)
        {
            customers.Add(customer);
        }
    } while (token != null);

    return View(customers);
    ```

1. W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **tabel**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.

1. Na powitania **Dodaj widok** okna dialogowego, wprowadź **GetPartition** hello nazwy widoku i wybierz **Dodaj**.

1. Otwórz `GetPartition.cshtml`i zmodyfikuj go, aby wygląda hello następującego fragmentu kodu:

    ```csharp
    @model IEnumerable<StorageAspnet.Models.CustomerEntity>
    @{
        ViewBag.Title = "GetPartition";
    }
    
    <h2>Get Partition results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>Email</th>
        </tr>
        @foreach (var customer in Model)
        {
        <tr>
            <td>@(customer.RowKey)</td>
            <td>@(customer.PartitionKey)</td>
            <td>@(customer.Email)</td>
        </tr>
        }
    </table>
    ```

1. W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.

1. Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. Uruchamianie aplikacji hello, a następnie wybierz **pobrać partycji** toosee wyniki podobne toohello po zrzut ekranu:
  
    ![Pobierz partycji](./media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a>Usuwanie jednostki

W tej części przedstawiono sposób toodelete jednostki z tabeli.

> [!NOTE]
> 
> W tej sekcji założono zostały wykonane kroki hello w [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment)i korzysta z danych [dodać partii jednostek tooa tabeli](#add-a-batch-of-entities-to-a-table). 

1. Otwórz hello `TablesController.cs` pliku.

1. Dodaj metodę o nazwie **DeleteEntity** zwracającą **ActionResult**.

    ```csharp
    public ActionResult DeleteEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. W ramach hello **DeleteEntity** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu. Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Pobierz **CloudTableClient** obiekt reprezentuje klienta usługi tabel.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Pobierz **CloudTable** obiekt, który reprezentuje odwołanie do tabeli toohello, z której po usunięciu jednostki hello. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Utwórz obiekt operacji delete, który przyjmuje do obiektu jednostki pochodne **TableEntity**. W takim przypadku stosujemy hello **CustomerEntity** klasy i dane podane w sekcji hello [dodać partii jednostek tooa tabeli](#add-a-batch-of-entities-to-a-table). Witaj jednostki **ETag** należy wybrać prawidłową wartość tooa.  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. Wykonanie operacji usuwania hello.   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. Przekaż hello widok toohello wyników do wyświetlenia.

    ```csharp
    return View(result);
    ```

1. W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **tabel**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.

1. Na powitania **Dodaj widok** okna dialogowego, wprowadź **DeleteEntity** hello nazwy widoku i wybierz **Dodaj**.

1. Otwórz `DeleteEntity.cshtml`i zmodyfikuj go, aby wygląda hello następującego fragmentu kodu:

    ```csharp
    @model Microsoft.WindowsAzure.Storage.Table.TableResult
    @{
        ViewBag.Title = "DeleteEntity";
    }
    
    <h2>Delete Entity results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>HTTP result</th>
        </tr>
        <tr>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@Model.HttpStatusCode</td>
        </tr>
    </table>

    ```

1. W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.

1. Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. Uruchamianie aplikacji hello, a następnie wybierz **usuwanie jednostek** toosee wyniki podobne toohello po zrzut ekranu:
  
    ![Pobierz pojedynczy](./media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a>Następne kroki
Wyświetl więcej funkcji toolearn przewodników o dodatkowych opcjach przechowywania danych na platformie Azure.

  * [Wprowadzenie do magazynu obiektów blob platformy Azure i programu Visual Studio połączone usługi (ASP.NET)](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [Rozpoczynanie pracy z magazynem kolejek Azure i programu Visual Studio połączone usługi (ASP.NET)](../storage/vs-storage-aspnet-getting-started-queues.md)
