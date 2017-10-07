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
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="c46a7-103">Rozpoczynanie pracy z magazynu tabel platformy Azure i programu Visual Studio połączone usługi (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="c46a7-103">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="c46a7-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="c46a7-104">Overview</span></span>

<span data-ttu-id="c46a7-105">Magazyn tabel Azure umożliwia toostore dużych ilości danych strukturalnych.</span><span class="sxs-lookup"><span data-stu-id="c46a7-105">Azure Table storage enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="c46a7-106">Usługa Hello jest magazynem danych NoSQL, który przyjmuje uwierzytelnione wywołania z wewnątrz, jak i poza hello chmury Azure.</span><span class="sxs-lookup"><span data-stu-id="c46a7-106">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="c46a7-107">Tabele Azure idealnie nadają się do przechowywania strukturalnych danych nierelacyjnych.</span><span class="sxs-lookup"><span data-stu-id="c46a7-107">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="c46a7-108">Ten samouczek pokazuje, jak kod toowrite ASP.NET dla niektórych typowych scenariuszy przy użyciu jednostek magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="c46a7-108">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure table storage entities.</span></span> <span data-ttu-id="c46a7-109">Te scenariusze obejmują tworzenie tabeli i dodanie, wyszukiwanie i usuwania jednostek tabeli.</span><span class="sxs-lookup"><span data-stu-id="c46a7-109">These scenarios include creating a table, and adding, querying, and deleting table entities.</span></span> 

##<a name="prerequisites"></a><span data-ttu-id="c46a7-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c46a7-110">Prerequisites</span></span>

* [<span data-ttu-id="c46a7-111">Program Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c46a7-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="c46a7-112">Konto usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c46a7-112">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="c46a7-113">Tworzenie kontrolera MVC</span><span class="sxs-lookup"><span data-stu-id="c46a7-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="c46a7-114">W hello **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **kontrolerów**i wybierz z menu kontekstowego hello **kontrolera -> Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-114">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![Dodaj tooan kontrolera aplikacji ASP.NET MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. <span data-ttu-id="c46a7-116">Na powitania **Dodawanie szkieletu** okno dialogowe, wybierz opcję **kontroler MVC 5 — pusty**i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-116">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Określ typ kontrolera MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. <span data-ttu-id="c46a7-118">Na powitania **Dodaj kontroler** okno dialogowe, nazwy kontrolera hello *TablesController*i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-118">On hello **Add Controller** dialog, name hello controller *TablesController*, and select **Add**.</span></span>

    ![Kontroler MVC hello nazwy](./media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. <span data-ttu-id="c46a7-120">Dodaj następujące hello *przy użyciu* toohello dyrektywy `TablesController.cs` pliku:</span><span class="sxs-lookup"><span data-stu-id="c46a7-120">Add hello following *using* directives toohello `TablesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a><span data-ttu-id="c46a7-121">Utwórz klasę modelu</span><span class="sxs-lookup"><span data-stu-id="c46a7-121">Create a model class</span></span>

<span data-ttu-id="c46a7-122">Wiele hello przykłady w tym artykule użyj **TableEntity**-klasy o nazwie **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-122">Many of hello examples in this article use a **TableEntity**-derived class called **CustomerEntity**.</span></span> <span data-ttu-id="c46a7-123">następujące kroki Hello informacje pomocne przy deklarowanie tę klasę jako klasę modelu:</span><span class="sxs-lookup"><span data-stu-id="c46a7-123">hello following steps guide you through declaring this class as a model class:</span></span>

1. <span data-ttu-id="c46a7-124">W hello **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **modele**i wybierz z menu kontekstowego hello **klasy -> Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-124">In hello **Solution Explorer**, right-click **Models**, and, from hello context menu, select **Add->Class**.</span></span>

1. <span data-ttu-id="c46a7-125">Na powitania **Dodaj nowy element** okno dialogowe, nazwa klasy hello, **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-125">On hello **Add New Item** dialog, name hello class, **CustomerEntity**.</span></span>

1. <span data-ttu-id="c46a7-126">Otwórz hello `CustomerEntity.cs` pliku, a następnie dodaj poniższe hello **przy użyciu** dyrektywy:</span><span class="sxs-lookup"><span data-stu-id="c46a7-126">Open hello `CustomerEntity.cs` file, and add hello following **using** directive:</span></span>

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. <span data-ttu-id="c46a7-127">Zmodyfikuj hello klasy, tak, aby po zakończeniu klasy hello jest zadeklarowana tak jak hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="c46a7-127">Modify hello class so that, when finished, hello class is declared as in hello following code.</span></span> <span data-ttu-id="c46a7-128">Klasa Hello deklaruje klasy jednostki o nazwie **CustomerEntity** imienia klienta jako hello klucz wiersza i nazwiska jako klucza partycji hello tekst hello zastosowań.</span><span class="sxs-lookup"><span data-stu-id="c46a7-128">hello class declares an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and last name as hello partition key.</span></span>

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

## <a name="create-a-table"></a><span data-ttu-id="c46a7-129">Tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="c46a7-129">Create a table</span></span>

<span data-ttu-id="c46a7-130">Witaj poniższe kroki przedstawiają sposób toocreate tabeli:</span><span class="sxs-lookup"><span data-stu-id="c46a7-130">hello following steps illustrate how toocreate a table:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="c46a7-131">W tej sekcji założono zostały wykonane kroki hello w [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="c46a7-131">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="c46a7-132">Otwórz hello `TablesController.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="c46a7-132">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="c46a7-133">Dodaj metodę o nazwie **CreateTable** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-133">Add a method called **CreateTable** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateTable()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="c46a7-134">W ramach hello **CreateTable** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="c46a7-134">Within hello **CreateTable** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="c46a7-135">Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)</span><span class="sxs-lookup"><span data-stu-id="c46a7-135">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="c46a7-136">Pobierz **CloudTableClient** obiekt reprezentuje klienta usługi tabel.</span><span class="sxs-lookup"><span data-stu-id="c46a7-136">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="c46a7-137">Pobierz **CloudTable** obiekt, który reprezentuje nazwę odwołania toohello żądanej tabeli.</span><span class="sxs-lookup"><span data-stu-id="c46a7-137">Get a **CloudTable** object that represents a reference toohello desired table name.</span></span> <span data-ttu-id="c46a7-138">Witaj **CloudTableClient.GetTableReference** — metoda nie powoduje żądanie magazyn tabel.</span><span class="sxs-lookup"><span data-stu-id="c46a7-138">hello **CloudTableClient.GetTableReference** method does not make a request against table storage.</span></span> <span data-ttu-id="c46a7-139">czy istnieje tabela hello, zwracane jest odwołanie Hello.</span><span class="sxs-lookup"><span data-stu-id="c46a7-139">hello reference is returned whether or not hello table exists.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="c46a7-140">Wywołaj hello **CloudTable.CreateIfNotExists** metody toocreate hello tabeli, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="c46a7-140">Call hello **CloudTable.CreateIfNotExists** method toocreate hello table if it does not yet exist.</span></span> <span data-ttu-id="c46a7-141">Witaj **CloudTable.CreateIfNotExists** metoda zwraca **true** Jeśli hello tabela nie istnieje i został utworzony pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="c46a7-141">hello **CloudTable.CreateIfNotExists** method returns **true** if hello table does not exist, and is successfully created.</span></span> <span data-ttu-id="c46a7-142">W przeciwnym razie **false** jest zwracany.</span><span class="sxs-lookup"><span data-stu-id="c46a7-142">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. <span data-ttu-id="c46a7-143">Aktualizacja hello **obiekt ViewBag** o nazwie hello hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="c46a7-143">Update hello **ViewBag** with hello name of hello table.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. <span data-ttu-id="c46a7-144">W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **tabel**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-144">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="c46a7-145">Na powitania **Dodaj widok** okna dialogowego, wprowadź **CreateTable** hello nazwy widoku i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-145">On hello **Add View** dialog, enter **CreateTable** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="c46a7-146">Otwórz `CreateTable.cshtml`i zmodyfikuj go, aby wygląda hello następującego fragmentu kodu:</span><span class="sxs-lookup"><span data-stu-id="c46a7-146">Open `CreateTable.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="c46a7-147">W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="c46a7-147">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="c46a7-148">Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="c46a7-148">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. <span data-ttu-id="c46a7-149">Uruchamianie aplikacji hello, a następnie wybierz **Utwórz tabelę** toosee wyniki podobne toohello po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="c46a7-149">Run hello application, and select **Create table** toosee results similar toohello following screen shot:</span></span>
  
    ![Tworzenie tabeli](./media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    <span data-ttu-id="c46a7-151">Jak wspomniano wcześniej, hello **CloudTable.CreateIfNotExists** metoda zwraca **true** tylko po tabeli hello nie istnieje i zostanie utworzony.</span><span class="sxs-lookup"><span data-stu-id="c46a7-151">As mentioned previously, hello **CloudTable.CreateIfNotExists** method returns **true** only when hello table doesn't exist and is created.</span></span> <span data-ttu-id="c46a7-152">W związku z tym po uruchomieniu aplikacji hello podczas hello tabela istnieje, metoda hello zwraca **false**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-152">Therefore, if you run hello app when hello table exists, hello method returns **false**.</span></span> <span data-ttu-id="c46a7-153">Aplikacja hello toorun wielokrotnie, należy usunąć tabeli hello przed ponownym uruchomieniem aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="c46a7-153">toorun hello app multiple times, you must delete hello table before running hello app again.</span></span> <span data-ttu-id="c46a7-154">Usuwanie tabeli hello może odbywać się za pośrednictwem hello **CloudTable.Delete** metody.</span><span class="sxs-lookup"><span data-stu-id="c46a7-154">Deleting hello table can be done via hello **CloudTable.Delete** method.</span></span> <span data-ttu-id="c46a7-155">Możesz także usunąć za pomocą hello tabeli hello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) lub hello [Eksploratora usługi Microsoft Azure Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="c46a7-155">You can also delete hello table using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="c46a7-156">Dodaj tabelę tooa jednostki</span><span class="sxs-lookup"><span data-stu-id="c46a7-156">Add an entity tooa table</span></span>

<span data-ttu-id="c46a7-157">*Jednostki* mapy tooC\# obiektów przy użyciu niestandardowej klasy pochodzące z **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-157">*Entities* map tooC\# objects by using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="c46a7-158">tooadd tabeli tooa jednostki, Utwórz klasę, która definiuje właściwości hello jednostki.</span><span class="sxs-lookup"><span data-stu-id="c46a7-158">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="c46a7-159">W tej sekcji zobaczysz, jak toodefine klasę jednostki, która używa hello imienia klienta jako hello klucz wiersza i nazwiska jako klucza partycji hello.</span><span class="sxs-lookup"><span data-stu-id="c46a7-159">In this section, you'll see how toodefine an entity class that uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="c46a7-160">Razem klucz partycji i klucz wiersza jednoznacznie zidentyfikować hello jednostki w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="c46a7-160">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="c46a7-161">Jednostki z tym samym kluczem partycji mogą być przeszukiwane szybciej niż jednostki o różnych kluczach partycji, niemniej użycie różnych kluczy partycji umożliwia zwiększenie skalowalności operacji równoległych.</span><span class="sxs-lookup"><span data-stu-id="c46a7-161">Entities with the same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="c46a7-162">Dla właściwości, które mają być przechowywane w usłudze tabel hello właściwość hello musi być właściwością publiczną obsługiwanego typu, która ujawnia zarówno ustawiania i pobierania wartości.</span><span class="sxs-lookup"><span data-stu-id="c46a7-162">For any property that should be stored in hello table service, hello property must be a public property of a supported type that exposes both setting and retrieving values.</span></span>
<span data-ttu-id="c46a7-163">Witaj klasy jednostka *musi* zadeklarować publicznego konstruktora bez parametrów.</span><span class="sxs-lookup"><span data-stu-id="c46a7-163">hello entity class *must* declare a public parameter-less constructor.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="c46a7-164">W tej sekcji założono zostały wykonane kroki hello w [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="c46a7-164">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="c46a7-165">Otwórz hello `TablesController.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="c46a7-165">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="c46a7-166">Dodaj następujące dyrektywy, które hello kodu w hello hello `TablesController.cs` pliku mogą uzyskiwać dostęp do hello **CustomerEntity** klasy:</span><span class="sxs-lookup"><span data-stu-id="c46a7-166">Add hello following directive so that hello code in hello `TablesController.cs` file can access hello **CustomerEntity** class:</span></span>

    ```csharp
    using StorageAspnet.Models;
    ```

1. <span data-ttu-id="c46a7-167">Dodaj metodę o nazwie **AddEntity** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-167">Add a method called **AddEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="c46a7-168">W ramach hello **AddEntity** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="c46a7-168">Within hello **AddEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="c46a7-169">Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)</span><span class="sxs-lookup"><span data-stu-id="c46a7-169">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="c46a7-170">Pobierz **CloudTableClient** obiekt reprezentuje klienta usługi tabel.</span><span class="sxs-lookup"><span data-stu-id="c46a7-170">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="c46a7-171">Pobierz **CloudTable** obiekt, który reprezentuje toowhich tabeli toohello odwołanie ma tooadd hello nowej jednostki.</span><span class="sxs-lookup"><span data-stu-id="c46a7-171">Get a **CloudTable** object that represents a reference toohello table toowhich you are going tooadd hello new entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="c46a7-172">Utwórz wystąpienie i zainicjować hello **CustomerEntity** klasy.</span><span class="sxs-lookup"><span data-stu-id="c46a7-172">Instantiate and initialize hello **CustomerEntity** class.</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. <span data-ttu-id="c46a7-173">Utwórz **TableOperation** obiekt, który wstawia powitania klienta jednostki.</span><span class="sxs-lookup"><span data-stu-id="c46a7-173">Create a **TableOperation** object that inserts hello customer entity.</span></span>

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. <span data-ttu-id="c46a7-174">Wykonanie operacji wstawiania hello przez wywołanie hello **CloudTable.Execute** metody.</span><span class="sxs-lookup"><span data-stu-id="c46a7-174">Execute hello insert operation by calling hello **CloudTable.Execute** method.</span></span> <span data-ttu-id="c46a7-175">Sprawdź hello wynik operacji hello, sprawdzając hello **TableResult.HttpStatusCode** właściwości.</span><span class="sxs-lookup"><span data-stu-id="c46a7-175">You can verify hello result of hello operation by inspecting hello **TableResult.HttpStatusCode** property.</span></span> <span data-ttu-id="c46a7-176">Kod stanu 2xx wskazuje, że akcja hello żądany przez klienta na powitania zostało przetworzone pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="c46a7-176">A status code of 2xx indicates hello action requested by hello client was processed successfully.</span></span> <span data-ttu-id="c46a7-177">Na przykład pomyślnie wstawienia nowych jednostek powoduje kod stanu HTTP 204, co oznacza, że pomyślnie przetworzono hello operacji i powitania serwera nie zwróciło żadnej zawartości.</span><span class="sxs-lookup"><span data-stu-id="c46a7-177">For example, successful insertions of new entities results in an HTTP status code of 204, meaning that hello operation was successfully processed and hello server did not return any content.</span></span>

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. <span data-ttu-id="c46a7-178">Aktualizacja hello **obiekt ViewBag** o nazwie tabeli hello i hello wyniki operacji insert hello.</span><span class="sxs-lookup"><span data-stu-id="c46a7-178">Update hello **ViewBag** with hello table name, and hello results of hello insert operation.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. <span data-ttu-id="c46a7-179">W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **tabel**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-179">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="c46a7-180">Na powitania **Dodaj widok** okna dialogowego, wprowadź **AddEntity** hello nazwy widoku i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-180">On hello **Add View** dialog, enter **AddEntity** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="c46a7-181">Otwórz `AddEntity.cshtml`i zmodyfikuj go, aby wygląda hello następującego fragmentu kodu:</span><span class="sxs-lookup"><span data-stu-id="c46a7-181">Open `AddEntity.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. <span data-ttu-id="c46a7-182">W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="c46a7-182">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="c46a7-183">Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="c46a7-183">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. <span data-ttu-id="c46a7-184">Uruchamianie aplikacji hello, a następnie wybierz **dodania jednostki** toosee wyniki podobne toohello po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="c46a7-184">Run hello application, and select **Add entity** toosee results similar toohello following screen shot:</span></span>
  
    ![Dodawanie jednostki](./media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    <span data-ttu-id="c46a7-186">Możesz sprawdzić, czy jednostki hello został dodany, wykonując kroki hello w sekcji hello [pobrać pojedynczą jednostką](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="c46a7-186">You can verify that hello entity was added by following hello steps in hello section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="c46a7-187">Można również użyć hello [Eksploratora usługi Microsoft Azure Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview hello wszystkie jednostki dla tabel.</span><span class="sxs-lookup"><span data-stu-id="c46a7-187">You can also use hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview all hello entities for your tables.</span></span>

## <a name="add-a-batch-of-entities-tooa-table"></a><span data-ttu-id="c46a7-188">Dodaj partii jednostek tooa tabeli</span><span class="sxs-lookup"><span data-stu-id="c46a7-188">Add a batch of entities tooa table</span></span>

<span data-ttu-id="c46a7-189">W stanie toobeing dodanie zbyt[Dodaj tabelę tooa jednostki, co w czasie](#add-an-entity-to-a-table), możesz także dodać jednostek w partii.</span><span class="sxs-lookup"><span data-stu-id="c46a7-189">In addition toobeing able too[add an entity tooa table one at a time](#add-an-entity-to-a-table), you can also add entities in batch.</span></span> <span data-ttu-id="c46a7-190">Dodawanie jednostek w partii zmniejsza hello częstotliwości przechodzenia między kod i hello usługi tabeli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c46a7-190">Adding entities in batch reduces hello number of round-trips between your code and hello Azure table service.</span></span> <span data-ttu-id="c46a7-191">Hello następujące kroki ilustrują sposób tooadd wiele jednostek tooa tabeli z operacją insert pojedynczego:</span><span class="sxs-lookup"><span data-stu-id="c46a7-191">hello following steps illustrate how tooadd multiple entities tooa table with a single insert operation:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="c46a7-192">W tej sekcji założono zostały wykonane kroki hello w [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="c46a7-192">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="c46a7-193">Otwórz hello `TablesController.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="c46a7-193">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="c46a7-194">Dodaj metodę o nazwie **AddEntities** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-194">Add a method called **AddEntities** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntities()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="c46a7-195">W ramach hello **AddEntities** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="c46a7-195">Within hello **AddEntities** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="c46a7-196">Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)</span><span class="sxs-lookup"><span data-stu-id="c46a7-196">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="c46a7-197">Pobierz **CloudTableClient** obiekt reprezentuje klienta usługi tabel.</span><span class="sxs-lookup"><span data-stu-id="c46a7-197">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="c46a7-198">Pobierz **CloudTable** obiekt, który reprezentuje toowhich tabeli toohello odwołania są będzie tooadd hello nowych jednostek.</span><span class="sxs-lookup"><span data-stu-id="c46a7-198">Get a **CloudTable** object that represents a reference toohello table toowhich you are going tooadd hello new entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="c46a7-199">Utworzenie wystąpienia niektórych obiektów klienta oparte na powitania **CustomerEntity** klasa przedstawione w sekcji hello modelu [Dodaj tabelę tooa jednostki](#add-an-entity-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="c46a7-199">Instantiate some customer objects based on hello **CustomerEntity** model class presented in hello section, [Add an entity tooa table](#add-an-entity-to-a-table).</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. <span data-ttu-id="c46a7-200">Pobierz **TableBatchOperation** obiektu.</span><span class="sxs-lookup"><span data-stu-id="c46a7-200">Get a **TableBatchOperation** object.</span></span>

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. <span data-ttu-id="c46a7-201">Dodaj obiekt operacji wstawiania wsadowego toohello jednostek.</span><span class="sxs-lookup"><span data-stu-id="c46a7-201">Add entities toohello batch insert operation object.</span></span>

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. <span data-ttu-id="c46a7-202">Wykonanie operacji wstawiania wsadowego hello przez wywołanie hello **CloudTable.ExecuteBatch** metody.</span><span class="sxs-lookup"><span data-stu-id="c46a7-202">Execute hello batch insert operation by calling hello **CloudTable.ExecuteBatch** method.</span></span>   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. <span data-ttu-id="c46a7-203">Witaj **CloudTable.ExecuteBatch** metoda zwraca listę **TableResult** obiektów gdzie każdy **TableResult** obiekt może być sprawdzone toodetermine hello powodzenie lub niepowodzenie poszczególnych działań.</span><span class="sxs-lookup"><span data-stu-id="c46a7-203">hello **CloudTable.ExecuteBatch** method returns a list of **TableResult** objects where each **TableResult** object can be examined toodetermine hello success or failure of each individual operation.</span></span> <span data-ttu-id="c46a7-204">Na przykład przekazać widoku tooa listy hello i pozwól widoku hello wyświetlać wyniki hello każdej operacji.</span><span class="sxs-lookup"><span data-stu-id="c46a7-204">For this example, pass hello list tooa view and let hello view display hello results of each operation.</span></span> 
 
    ```csharp
    return View(results);
    ```

1. <span data-ttu-id="c46a7-205">W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **tabel**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-205">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="c46a7-206">Na powitania **Dodaj widok** okna dialogowego, wprowadź **AddEntities** hello nazwy widoku i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-206">On hello **Add View** dialog, enter **AddEntities** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="c46a7-207">Otwórz `AddEntities.cshtml`i zmodyfikuj go, aby wygląda jak poniżej hello.</span><span class="sxs-lookup"><span data-stu-id="c46a7-207">Open `AddEntities.cshtml`, and modify it so that it looks like hello following.</span></span>

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

1. <span data-ttu-id="c46a7-208">W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="c46a7-208">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="c46a7-209">Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="c46a7-209">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. <span data-ttu-id="c46a7-210">Uruchamianie aplikacji hello, a następnie wybierz **Dodaj jednostki** toosee wyniki podobne toohello po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="c46a7-210">Run hello application, and select **Add entities** toosee results similar toohello following screen shot:</span></span>
  
    ![Dodawanie jednostek](./media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    <span data-ttu-id="c46a7-212">Możesz sprawdzić, czy jednostki hello został dodany, wykonując kroki hello w sekcji hello [pobrać pojedynczą jednostką](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="c46a7-212">You can verify that hello entity was added by following hello steps in hello section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="c46a7-213">Można również użyć hello [Eksploratora usługi Microsoft Azure Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview hello wszystkie jednostki dla tabel.</span><span class="sxs-lookup"><span data-stu-id="c46a7-213">You can also use hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview all hello entities for your tables.</span></span>

## <a name="get-a-single-entity"></a><span data-ttu-id="c46a7-214">Pobierz pojedynczy element</span><span class="sxs-lookup"><span data-stu-id="c46a7-214">Get a single entity</span></span>

<span data-ttu-id="c46a7-215">W tej części przedstawiono, jak tooget pojedyncza jednostka z tabeli za pomocą hello klucz wiersza jednostki i klucz partycji.</span><span class="sxs-lookup"><span data-stu-id="c46a7-215">This section illustrates how tooget a single entity from a table using hello entity's row key and partition key.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="c46a7-216">W tej sekcji założono zostały wykonane kroki hello w [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment)i korzysta z danych [dodać partii jednostek tooa tabeli](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="c46a7-216">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="c46a7-217">Otwórz hello `TablesController.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="c46a7-217">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="c46a7-218">Dodaj metodę o nazwie **GetSingle** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-218">Add a method called **GetSingle** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetSingle()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="c46a7-219">W ramach hello **GetSingle** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="c46a7-219">Within hello **GetSingle** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="c46a7-220">Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)</span><span class="sxs-lookup"><span data-stu-id="c46a7-220">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="c46a7-221">Pobierz **CloudTableClient** obiekt reprezentuje klienta usługi tabel.</span><span class="sxs-lookup"><span data-stu-id="c46a7-221">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="c46a7-222">Pobierz **CloudTable** obiekt, który reprezentuje tabelę toohello odwołanie, z którego są pobierane hello jednostki.</span><span class="sxs-lookup"><span data-stu-id="c46a7-222">Get a **CloudTable** object that represents a reference toohello table from which you are retrieving hello entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="c46a7-223">Utwórz obiekt operacji pobierania, który przyjmuje do obiektu jednostki pochodne **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-223">Create a retrieve operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="c46a7-224">pierwszy parametr Hello jest hello *partitionKey*, a drugi parametr hello jest hello *rowKey*.</span><span class="sxs-lookup"><span data-stu-id="c46a7-224">hello first parameter is hello *partitionKey*, and hello second parameter is hello *rowKey*.</span></span> <span data-ttu-id="c46a7-225">Przy użyciu hello **CustomerEntity** klasy i dane podane w sekcji hello [dodać partii jednostek tabeli tooa](#add-a-batch-of-entities-to-a-table), hello następujący kod fragment zapytania hello tabeli **CustomerEntity** jednostki o *partitionKey* wartość "Smith" i *rowKey* wartość "Ben":</span><span class="sxs-lookup"><span data-stu-id="c46a7-225">Using hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table), hello following code snippet queries hello table for a **CustomerEntity** entity with a *partitionKey* value of "Smith" and a *rowKey* value of "Ben":</span></span>

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. <span data-ttu-id="c46a7-226">Wykonanie operacji pobierania hello.</span><span class="sxs-lookup"><span data-stu-id="c46a7-226">Execute hello retrieve operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. <span data-ttu-id="c46a7-227">Przekaż hello widok toohello wyników do wyświetlenia.</span><span class="sxs-lookup"><span data-stu-id="c46a7-227">Pass hello result toohello view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="c46a7-228">W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **tabel**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-228">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="c46a7-229">Na powitania **Dodaj widok** okna dialogowego, wprowadź **GetSingle** hello nazwy widoku i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-229">On hello **Add View** dialog, enter **GetSingle** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="c46a7-230">Otwórz `GetSingle.cshtml`i zmodyfikuj go, aby wygląda hello następującego fragmentu kodu:</span><span class="sxs-lookup"><span data-stu-id="c46a7-230">Open `GetSingle.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

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

1. <span data-ttu-id="c46a7-231">W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="c46a7-231">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="c46a7-232">Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="c46a7-232">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. <span data-ttu-id="c46a7-233">Uruchamianie aplikacji hello, a następnie wybierz **Pobierz pojedynczy** toosee wyniki podobne toohello po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="c46a7-233">Run hello application, and select **Get Single** toosee results similar toohello following screen shot:</span></span>
  
    ![Pobierz pojedynczy](./media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a><span data-ttu-id="c46a7-235">Pobieranie wszystkich jednostek w partycji</span><span class="sxs-lookup"><span data-stu-id="c46a7-235">Get all entities in a partition</span></span>

<span data-ttu-id="c46a7-236">Jak wspomniano w sekcji hello [Dodaj tabelę tooa jednostki](#add-an-entity-to-a-table), kombinację hello partycji i klucz wiersza jednoznacznie identyfikują jednostkę w tabeli.</span><span class="sxs-lookup"><span data-stu-id="c46a7-236">As mentioned in hello section, [Add an entity tooa table](#add-an-entity-to-a-table), hello combination of a partition and a row key uniquely identify an entity in a table.</span></span> <span data-ttu-id="c46a7-237">Jednostki z tym samym kluczem partycji mogą być przeszukiwane szybciej niż jednostki o różnych kluczach partycji.</span><span class="sxs-lookup"><span data-stu-id="c46a7-237">Entities with the same partition key can be queried faster than entities with different partition keys.</span></span> <span data-ttu-id="c46a7-238">W tej części przedstawiono sposób tooquery tabeli dla wszystkich jednostek hello z określonej partycji.</span><span class="sxs-lookup"><span data-stu-id="c46a7-238">This section illustrates how tooquery a table for all hello entities from a specified partition.</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="c46a7-239">W tej sekcji założono zostały wykonane kroki hello w [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment)i korzysta z danych [dodać partii jednostek tooa tabeli](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="c46a7-239">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="c46a7-240">Otwórz hello `TablesController.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="c46a7-240">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="c46a7-241">Dodaj metodę o nazwie **GetPartition** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-241">Add a method called **GetPartition** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetPartition()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="c46a7-242">W ramach hello **GetPartition** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="c46a7-242">Within hello **GetPartition** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="c46a7-243">Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)</span><span class="sxs-lookup"><span data-stu-id="c46a7-243">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="c46a7-244">Pobierz **CloudTableClient** obiekt reprezentuje klienta usługi tabel.</span><span class="sxs-lookup"><span data-stu-id="c46a7-244">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="c46a7-245">Pobierz **CloudTable** obiekt, który reprezentuje tabeli toohello odwołań, z którego są pobierane hello jednostek.</span><span class="sxs-lookup"><span data-stu-id="c46a7-245">Get a **CloudTable** object that represents a reference toohello table from which you are retrieving hello entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="c46a7-246">Utwórz wystąpienie **TableQuery** obiektu określenie hello zapytania w hello **gdzie** klauzuli.</span><span class="sxs-lookup"><span data-stu-id="c46a7-246">Instantiate a **TableQuery** object specifying hello query in hello **Where** clause.</span></span> <span data-ttu-id="c46a7-247">Przy użyciu hello **CustomerEntity** klasy i dane podane w sekcji hello [dodać partii jednostek tabeli tooa](#add-a-batch-of-entities-to-a-table), hello poniższy kod fragment zapytania hello tabeli dla wszystkich jednostek, gdzie hello  **PartitionKey** (nazwiska) ma wartość "Smith":</span><span class="sxs-lookup"><span data-stu-id="c46a7-247">Using hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table), hello following code snippet queries hello table for a all entities where hello **PartitionKey** (customer's last name) has a value of "Smith":</span></span>

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. <span data-ttu-id="c46a7-248">W pętli, wywołaj hello **CloudTable.ExecuteQuerySegmented** metoda przekazywania można utworzyć wystąpienia obiektu query hello hello poprzedniego kroku.</span><span class="sxs-lookup"><span data-stu-id="c46a7-248">Within a loop, call hello **CloudTable.ExecuteQuerySegmented** method passing hello query object you instantiated in hello previous step.</span></span>  <span data-ttu-id="c46a7-249">Hello **CloudTable.ExecuteQuerySegmented** metoda zwraca **TableContinuationToken** obiekt – podczas **null** — wskazuje, że nie ma żadnych kolejnych jednostek tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="c46a7-249">hello **CloudTable.ExecuteQuerySegmented** method returns a **TableContinuationToken** object that - when **null** - indicates that there are no more entities tooretrieve.</span></span> <span data-ttu-id="c46a7-250">W pętli hello należy użyć innego tooiterate pętli za pośrednictwem hello zwracane jednostki.</span><span class="sxs-lookup"><span data-stu-id="c46a7-250">Within hello loop, use another loop tooiterate over hello returned entities.</span></span> <span data-ttu-id="c46a7-251">W hello poniższy przykład kodu każdy zwrócony obiekt jest dodawany tooa listy.</span><span class="sxs-lookup"><span data-stu-id="c46a7-251">In hello following code example, each returned entity is added tooa list.</span></span> <span data-ttu-id="c46a7-252">Raz hello kończy pętlę, hello listy jest przekazywany tooa widoku do wyświetlenia:</span><span class="sxs-lookup"><span data-stu-id="c46a7-252">Once hello loop ends, hello list is passed tooa view for display:</span></span> 

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

1. <span data-ttu-id="c46a7-253">W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **tabel**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-253">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="c46a7-254">Na powitania **Dodaj widok** okna dialogowego, wprowadź **GetPartition** hello nazwy widoku i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-254">On hello **Add View** dialog, enter **GetPartition** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="c46a7-255">Otwórz `GetPartition.cshtml`i zmodyfikuj go, aby wygląda hello następującego fragmentu kodu:</span><span class="sxs-lookup"><span data-stu-id="c46a7-255">Open `GetPartition.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

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

1. <span data-ttu-id="c46a7-256">W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="c46a7-256">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="c46a7-257">Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="c46a7-257">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. <span data-ttu-id="c46a7-258">Uruchamianie aplikacji hello, a następnie wybierz **pobrać partycji** toosee wyniki podobne toohello po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="c46a7-258">Run hello application, and select **Get Partition** toosee results similar toohello following screen shot:</span></span>
  
    ![Pobierz partycji](./media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a><span data-ttu-id="c46a7-260">Usuwanie jednostki</span><span class="sxs-lookup"><span data-stu-id="c46a7-260">Delete an entity</span></span>

<span data-ttu-id="c46a7-261">W tej części przedstawiono sposób toodelete jednostki z tabeli.</span><span class="sxs-lookup"><span data-stu-id="c46a7-261">This section illustrates how toodelete an entity from a table.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="c46a7-262">W tej sekcji założono zostały wykonane kroki hello w [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment)i korzysta z danych [dodać partii jednostek tooa tabeli](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="c46a7-262">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="c46a7-263">Otwórz hello `TablesController.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="c46a7-263">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="c46a7-264">Dodaj metodę o nazwie **DeleteEntity** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-264">Add a method called **DeleteEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="c46a7-265">W ramach hello **DeleteEntity** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="c46a7-265">Within hello **DeleteEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="c46a7-266">Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)</span><span class="sxs-lookup"><span data-stu-id="c46a7-266">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="c46a7-267">Pobierz **CloudTableClient** obiekt reprezentuje klienta usługi tabel.</span><span class="sxs-lookup"><span data-stu-id="c46a7-267">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="c46a7-268">Pobierz **CloudTable** obiekt, który reprezentuje odwołanie do tabeli toohello, z której po usunięciu jednostki hello.</span><span class="sxs-lookup"><span data-stu-id="c46a7-268">Get a **CloudTable** object that represents a reference toohello table from which you are deleting hello entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="c46a7-269">Utwórz obiekt operacji delete, który przyjmuje do obiektu jednostki pochodne **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-269">Create a delete operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="c46a7-270">W takim przypadku stosujemy hello **CustomerEntity** klasy i dane podane w sekcji hello [dodać partii jednostek tooa tabeli](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="c46a7-270">In this case, we use hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> <span data-ttu-id="c46a7-271">Witaj jednostki **ETag** należy wybrać prawidłową wartość tooa.</span><span class="sxs-lookup"><span data-stu-id="c46a7-271">hello entity's **ETag** must be set tooa valid value.</span></span>  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. <span data-ttu-id="c46a7-272">Wykonanie operacji usuwania hello.</span><span class="sxs-lookup"><span data-stu-id="c46a7-272">Execute hello delete operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. <span data-ttu-id="c46a7-273">Przekaż hello widok toohello wyników do wyświetlenia.</span><span class="sxs-lookup"><span data-stu-id="c46a7-273">Pass hello result toohello view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="c46a7-274">W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **tabel**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-274">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="c46a7-275">Na powitania **Dodaj widok** okna dialogowego, wprowadź **DeleteEntity** hello nazwy widoku i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-275">On hello **Add View** dialog, enter **DeleteEntity** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="c46a7-276">Otwórz `DeleteEntity.cshtml`i zmodyfikuj go, aby wygląda hello następującego fragmentu kodu:</span><span class="sxs-lookup"><span data-stu-id="c46a7-276">Open `DeleteEntity.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

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

1. <span data-ttu-id="c46a7-277">W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="c46a7-277">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="c46a7-278">Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="c46a7-278">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. <span data-ttu-id="c46a7-279">Uruchamianie aplikacji hello, a następnie wybierz **usuwanie jednostek** toosee wyniki podobne toohello po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="c46a7-279">Run hello application, and select **Delete entity** toosee results similar toohello following screen shot:</span></span>
  
    ![Pobierz pojedynczy](./media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a><span data-ttu-id="c46a7-281">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c46a7-281">Next steps</span></span>
<span data-ttu-id="c46a7-282">Wyświetl więcej funkcji toolearn przewodników o dodatkowych opcjach przechowywania danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c46a7-282">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="c46a7-283">Wprowadzenie do magazynu obiektów blob platformy Azure i programu Visual Studio połączone usługi (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="c46a7-283">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="c46a7-284">Rozpoczynanie pracy z magazynem kolejek Azure i programu Visual Studio połączone usługi (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="c46a7-284">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-queues.md)
